---
seo-title: 處理Adobe Primetime DRM要求
title: 處理Adobe Primetime DRM要求
uuid: ee10504d-84f0-472a-b58a-2a87fdeedfc1
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# 處理Adobe Primetime DRM要求 {#process-adobe-primetime-drm-requests}

管理請求的一般方法是建立處理常式、剖析請求、設定回應資料或錯誤碼，並關閉處理常式。

用於處理單個請求／響應交互的基類為 `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`。 類的實例用 `HandlerConfiguration` 於初始化處理程式。 `HandlerConfiguration` 儲存伺服器配置資訊，包括傳輸憑據、時間戳容限、策略更新清單和撤銷清單。處理程式讀取請求資料並將請求解析為實例 `RequestMessageBase`。 呼叫者可以檢查請求中的資訊並決定是返回錯誤還是成功響應(子類 `RequestMessageBase` 提供設定響應資料的方法)。

如果請求成功，請設定響應資料；否則，在失 `RequestMessageBase.setErrorData()` 敗時調用。 一律以叫用方法來結 `close()` 束實作(建議在 `close()` 陳述式的 `finally` 區塊中呼叫 `try` )。 如需如 `MessageHandlerBase` 何叫用處理常式的範例，請參閱API參考檔案。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>HTTP狀態碼200(OK)應會針對處理常式處理的所有要求而傳送。 如果由於伺服器錯誤而無法建立處理常式，伺服器可能會以其他狀態碼(例如500（內部伺服器錯誤）)回應。

用戶端會使用封裝時指定的授權伺服器URL，做為傳送至授權伺服器的所有要求的基本URL。 例如，如果伺服器URL指定為&lt;[!DNL ht<span></span>tps://licenseserver.com/path]>，則用戶端會傳送要求至&lt;[!DNL ht<span></span>tps://licenseserver.com/path/flashaccess/...]>，請參閱下列章節以取得用於每種請求類型之特定路徑的詳細資訊。 實作授權伺服器時，請確定伺服器回應每種請求類型所需的路徑。

授權要求可包含驗證Token。 如果使用使用者名稱／密碼驗證，則請求可能包含 `AuthenticationToken` 由所產生的 `AuthenticationHandler`，而SDK將在核發授權前確保Token有效。

## 使用機器識別碼 {#use-machine-identifiers}

所有Adobe Primetime DRM請求（支援FMRMS相容性的請求除外）都包含在個人化期間發送給用戶端之機器Token的相關資訊。 機器Token包含機器ID，此為在個人化期間指派的識別碼。 您可以使用此識別碼來計算使用者要求授權或加入網域的電腦數目。

您可以使用以下識別碼：

* 該方 `getUniqueId()` 法返回在個人化期間指派給裝置的字串。 您可以將字串儲存在資料庫中，並依識別碼進行搜尋。 不過，如果使用者重新格式化硬碟並再次個人化，此識別碼會變更。 此識別碼在相同機器上，Adobe AIR和Adobe Flash Player在不同瀏覽器上的值也不同。
* 如果您想要更精確地電腦，可以使 `getBytes()` 用儲存整個標識符。 若要判斷之前是否已檢視過電腦，請取得使用者名稱的所有識別碼，並呼叫以 `matches()` 檢查是否相符。 由於必 `matches()` 須使用方法來比較傳回的值，因此 `MachineId.getBytes`，只有少數值可供比較時，此選項才實用；例如，與特定用戶關聯的電腦。

## 使用者驗證 {#user-authentication}

Adobe Primetime DRM要求可包含驗證Token。

如果使用使用者名稱／密碼驗證，則請求可能包含 `AuthenticationToken` 由產生的 `AuthenticationHandler`。 如果您想要存取並驗證Token，則需使用 `RequestMessageBase.getAuthenticationToken()`。 若要在用戶端上起始使用者名稱／密碼要求，請使 `DRMManager.authenticate()` 用ActionScript或iOS API。

如果用戶端和伺服器使用自訂驗證機制，用戶端會透過其他通道取得驗證Token，並使用 `DRMManager.setAuthenticationToken` ActionScript 3.0 API設定自訂驗證Token。 使用 `RequestMessageBase.getRawAuthenticationToken()` 取得自訂驗證Token。 伺服器實作會判斷自訂驗證Token是否有效。

## 重放保護 {#replay-protection}

對於重放保護，您可能希望通過調用來檢查最近是否看到消息標識符 `RequestMessageBase.getMessageId()`。 如果是，攻擊者可能會嘗試重播請求，但請求應被拒絕。 為了檢測重放嘗試，伺服器可以儲存最近看到的消息ID的清單，並根據快取的清單檢查每個傳入的請求。 要限制消息標識符需要儲存的時間，請調用 `HandlerConfiguration.setTimestampTolerance()`。 若已設定此屬性，SDK會拒絕任何攜帶時間戳記超過伺服器時間指定秒數的請求。

## 回滾檢測 {#rollback-detection}

對於回滾檢測，某些使用規則要求客戶端維護狀態資訊以執行權限。 例如，為了強制播放視窗使用規則，用戶端會儲存使用者首次檢視內容的日期和時間。 此事件會觸發播放視窗的開始。 要安全地強制播放窗口，伺服器需要確保用戶不備份和恢復客戶端狀態，以刪除儲存在客戶端上的播放窗口啟動時間。 伺服器通過跟蹤客戶機回滾計數器的值來執行此操作。

對於每個請求，伺服器通過調用獲取對象， `RequestMessageBase.getClientState()` 然後調用獲取 `ClientState` 客戶 `ClientState.getCounter()` 端狀態計數器的當前值來獲取計數器的值。 伺服器應為每個客戶端儲存此值(用 `MachineId.getUniqueId()` 於標識與回滾計數器值關聯的客戶端)，然後調用 `ClientState.incrementCounter()` 將計數器值增加一。 如果伺服器檢測到計數器值小於伺服器所看到的最後一個值，則客戶端狀態可能已回退。

如需用戶 `ClientState` 端狀態竄改偵測的詳細資訊，請參閱API參考檔案。

## 全域伺服器組態資料{#global-server-configuration-data}

除了授權伺服器使用的設定外，還會儲 `HandlerConfiguration` 存可傳送至用戶端的設定資訊，以控制授權的執行方式。 這是透過建立類別並呼叫 `ServerConfigData` 來完成的 `HandlerConfiguration.setServerConfigData()`。 這些設定僅適用於此授權伺服器所核發的授權。

時鐘回退容限是授權伺服器可設定的屬性之一，以控制用戶端執行授權的方式。 依預設，使用者可將其電腦時鐘設定在4小時前，而不會使授權失效。 如果授權伺服器運算子想要使用不同的設定，可以在類別中設定新 `ServerConfigData` 值。 當您變更其中任何設定的值時，請務必透過呼叫來增加版本號碼 `setVersion()`。 新值僅在客戶端上的版本比當前版本舊時才會發送到客 `ServerConfigData` 戶端。

## 跨域DRM策略檔案 {#crossdomain-drm-policy-file}

如果授權伺服器是裝載在視訊播放SWF以外的網域上，則需要跨網域DRM原則檔案( [!DNL crossdomain.xml])才能讓SWF向授權伺服器要求授權。 跨網域DRM原則檔案由XML檔案表示，讓伺服器指出其資料和檔案可供其他網域提供的SWF檔案使用。 任何從授權伺服器的跨網域DRM原則檔案中指定之網域提供的SWF檔案，都可從該授權伺服器存取資料或資產。

Adobe建議開發人員在部署跨網域原則檔案時，只要允許受信任網域存取授權伺服器，並限制對Web伺服器上授權子目錄的存取，就應遵循最佳實務。

如需跨網域DRM原則檔案的詳細資訊，請參閱下列位置：

* 網站控制項（DRM原則檔案）
* 跨域DRM策略檔案規範： [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)