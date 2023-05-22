---
title: 處理Adobe PrimetimeDRM請求
description: 處理Adobe PrimetimeDRM請求
copied-description: true
exl-id: ca9c2ccc-b848-4271-88bc-e7e3ced135ce
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%

---

# 處理Adobe PrimetimeDRM請求 {#process-adobe-primetime-drm-requests}

管理請求的一般方法是建立處理程式、分析請求、設定響應資料或錯誤代碼並關閉處理程式。

用於處理單個請求/響應交互的基類是 `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`。 實例 `HandlerConfiguration` 類用於初始化處理程式。 `HandlerConfiguration` 儲存伺服器配置資訊，包括傳輸憑據、時間戳容差、策略更新清單和吊銷清單。處理程式讀取請求資料並將請求解析到的實例中 `RequestMessageBase`。 調用方可以檢查請求中的資訊，並決定是返回錯誤還是成功響應（子類） `RequestMessageBase` 提供一種設定響應資料的方法)。

如果請求成功，請設定響應資料；否則調用 `RequestMessageBase.setErrorData()` 失敗。 始終通過調用 `close()` 方法(建議 `close()` 被叫來 `finally` 塊 `try` )。 查看 `MessageHandlerBase` API參考文檔，用於有關如何調用處理程式的示例。

>[!NOTE]
>
>應發送HTTP狀態代碼200(OK)以響應處理程式處理的所有請求。 如果由於伺服器錯誤而無法建立處理程式，則伺服器可能會使用其他狀態代碼(如500（內部伺服器錯誤）)進行響應。

客戶端將打包時指定的許可證伺服器URL用作發送到許可證伺服器的所有請求的基本URL。 例如，如果伺服器URL指定為&lt;[!DNL ht<span></span>tps://licenseserver.com/path]> ，然後客戶端向&lt;[!DNL ht<span></span>tps://licenseserver.com/path/flashaccess/...]>有關每種請求類型所用特定路徑的詳細資訊，請參閱以下各節。 在實施許可證伺服器時，確保伺服器響應每種請求類型所需的路徑。

許可請求可以包含驗證令牌。 如果使用了用戶名/密碼身份驗證，則請求可能包含 `AuthenticationToken` 由 `AuthenticationHandler`，並且SDK將確保令牌在頒發許可證之前有效。

## 使用電腦標識符 {#use-machine-identifiers}

所有Adobe PrimetimeDRM請求（支援FMRMS相容性的請求除外）都包括關於在個性化期間已發給客戶機的機器令牌的資訊。 電腦令牌包括電腦ID，該ID是在個性化期間分配的標識符。 您可以使用此標識符來計算用戶已請求許可證或加入域的電腦數。

您可以使用以下標識符：

* 的 `getUniqueId()` 方法返回在個性化期間分配給設備的字串。 可以將字串儲存在資料庫中並按標識符進行搜索。 但是，如果用戶重新格式化硬碟並再次個性化，則此標識符會更改。 此標識符在同一台電腦上的不同瀏覽器中的Adobe AIR和AdobeFlash Player之間也具有不同的值。
* 如果想更準確地計算電腦，可以使用 `getBytes()` 儲存整個標識符。 要確定以前是否看到過電腦，請獲取用戶名的所有標識符並調用 `matches()` 檢查是否匹配。 因為 `matches()` 方法必須用於比較由 `MachineId.getBytes`，此選項僅在有少量值可供比較時才實用；例如，與特定用戶關聯的電腦。

## 用戶驗證 {#user-authentication}

Adobe PrimetimeDRM請求可以包含驗證令牌。

如果使用了用戶名/密碼驗證，則請求可能包含 `AuthenticationToken` 由 `AuthenticationHandler`。 如果要訪問並驗證令牌，則需要使用 `RequestMessageBase.getAuthenticationToken()`。 要在客戶端上啟動用戶名/密碼請求，請使用 `DRMManager.authenticate()` ActionScript或iOSAPI。

如果客戶機和伺服器使用自定義認證機制，則客戶機通過其它通道獲得認證令牌並使用 `DRMManager.setAuthenticationToken` ActionScript3.0 API。 使用 `RequestMessageBase.getRawAuthenticationToken()` 獲取自定義身份驗證令牌。 伺服器實現確定自定義驗證令牌是否有效。

## 重放保護 {#replay-protection}

對於重播保護，您可能需要通過調用來檢查最近是否看到消息標識符 `RequestMessageBase.getMessageId()`。 如果是，則攻擊者可能正嘗試重播請求，應拒絕該請求。 為了檢測重播嘗試，伺服器可以儲存最近看到的消息ID的清單，並根據快取清單檢查每個傳入請求。 要限制消息標識符需要儲存的時間，請調用 `HandlerConfiguration.setTimestampTolerance()`。 如果設定了此屬性，則SDK會拒絕任何帶有超過指定秒數的時間戳的伺服器時間請求。

## 回滾檢測 {#rollback-detection}

對於回滾檢測，某些使用規則要求客戶端維護狀態資訊以執行權限。 例如，要強制實施播放窗口使用規則，客戶端儲存用戶首次開始查看內容的日期和時間。 此事件觸發播放窗口的開始。 為了安全地強制播放窗口，伺服器需要確保用戶不備份和恢復客戶端狀態，以刪除儲存在客戶端上的播放窗口開始時間。 伺服器通過跟蹤客戶端回滾計數器的值來執行此操作。

對於每個請求，伺服器通過調用獲取計數器的值 `RequestMessageBase.getClientState()` 獲取 `ClientState` 對象，然後調用 `ClientState.getCounter()` 獲取客戶端狀態計數器的當前值。 伺服器應為每個客戶端儲存此值(使用 `MachineId.getUniqueId()` 標識與回滾計數器值關聯的客戶端)，然後調用 `ClientState.incrementCounter()` 將計數器值增加1。 如果伺服器檢測到計數器值小於伺服器看到的最後一個值，則客戶端狀態可能已回滾。

查看 `ClientState` 有關客戶端狀態篡改檢測的詳細資訊，請參閱API參考文檔。

## 全局伺服器配置資料{#global-server-configuration-data}

除了許可證伺服器使用的配置外， `HandlerConfiguration` 儲存可發送到客戶端的配置資訊，以控制如何強制實施許可證。 通過建立 `ServerConfigData` 類和呼叫 `HandlerConfiguration.setServerConfigData()`。 這些設定僅適用於此許可證伺服器頒發的許可證。

時鐘向後容錯是許可證伺服器可以設定的一個屬性，以控制客戶端如何實施許可證。 預設情況下，用戶可以將其電腦時鐘設定回4小時，而不會使許可證失效。 如果許可證伺服器操作員希望使用其他設定，可以在 `ServerConfigData` 類。 更改這些設定中的任何一個的值時，請確保通過調用來增加版本號 `setVersion()`。 僅當客戶端上的版本比當前版本舊時，新值才會發送到客戶端 `ServerConfigData` 。

## 跨域DRM策略檔案 {#crossdomain-drm-policy-file}

如果許可證伺服器托管在與視頻播放SWF不同的域上，則跨域DRM策略檔案( [!DNL crossdomain.xml])，以啟用SWF從許可證伺服器請求許可證。 跨域DRM策略檔案由XML檔案表示，該XML檔案使伺服器能夠指示其資料和文檔可用於SWF從其他域服務的檔案。 允許從許可證伺服器的跨域DRM策略檔案中指定的域提供的任何SWF檔案從該許可證伺服器訪問資料或資產。

Adobe建議開發人員在部署跨域策略檔案時遵循最佳做法，方法是僅允許受信任的域訪問許可證伺服器並限制對Web伺服器上許可證子目錄的訪問。

有關跨域DRM策略檔案的詳細資訊，請參閱以下位置：

* 網站控制項（DRM策略檔案）
* 跨域DRM策略檔案規範： [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)
