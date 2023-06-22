---
title: 處理Adobe Primetime DRM請求
description: 處理Adobe Primetime DRM請求
copied-description: true
exl-id: ca9c2ccc-b848-4271-88bc-e7e3ced135ce
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%

---

# 處理Adobe Primetime DRM請求 {#process-adobe-primetime-drm-requests}

管理請求的一般方法是建立處理常式、剖析請求、設定回應資料或錯誤代碼，以及關閉處理常式。

處理單一請求/回應互動的基底類別為 `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. 的例項 `HandlerConfiguration` 類別用來初始化處理常式。 `HandlerConfiguration` 儲存伺服器組態資訊，包括傳輸認證、時間戳記公差、原則更新清單和撤銷清單。處理常式會讀取要求資料，並將要求剖析成的執行個體。 `RequestMessageBase`. 呼叫者可以檢查要求中的資訊，並決定是傳回錯誤還是成功回應(的子類別 `RequestMessageBase` 提供設定回應資料的方法)。

如果要求成功，請設定回應資料；否則會叫用 `RequestMessageBase.setErrorData()` 失敗時。 一律叫用「 」以結束實施 `close()` 方法(建議您 `close()` 在中呼叫 `finally` 區塊 `try` 陳述式)。 請參閱 `MessageHandlerBase` API參考檔案以取得如何叫用處理常式的範例。

>[!NOTE]
>
>應該傳送HTTP狀態碼200 （確定）以回應處理常式處理的所有要求。 如果因為伺服器錯誤而無法建立處理常式，伺服器可能會以其他狀態碼回應，例如500 （內部伺服器錯誤）。

使用者端使用封裝時指定的授權伺服器URL，作為傳送至授權伺服器之所有要求的基礎URL。 例如，如果將伺服器URL指定為&lt;[!DNL ht<span></span>tps://licenseserver.com/path]>，使用者端接著傳送要求給&lt;[!DNL ht<span></span>tps://licenseserver.com/path/flashaccess/...]>請參閱以下章節，瞭解用於每種請求型別的特定路徑的詳細資訊。 實作您的授權伺服器時，請確定伺服器會回應每種型別要求所需的路徑。

授權請求可包含驗證權杖。 如果使用使用者名稱/密碼驗證，請求可能包含 `AuthenticationToken` 產生者： `AuthenticationHandler`，且SDK會在核發授權之前確保權杖有效。

## 使用機器識別碼 {#use-machine-identifiers}

所有Adobe Primetime DRM請求（支援FMRMS相容性的請求除外）都包含已在個人化期間核發給使用者端之機器權杖的相關資訊。 電腦Token包含電腦ID，這是已在個人化期間指派的識別碼。 您可以使用此識別碼來計算使用者已要求授權或加入網域的電腦數量。

您可以使用識別碼，如下所示：

* 此 `getUniqueId()` 方法會傳回在個人化期間指派給裝置的字串。 您可以將字串儲存在資料庫中並按識別碼搜尋。 但是，如果使用者重新格式化硬碟並再次個人化，此識別碼會變更。 在相同電腦上的不同瀏覽器中，此識別碼在Adobe AIR和AdobeFlash Player之間也有不同的值。
* 如果您想要更準確地計算電腦，可以使用 `getBytes()` 以儲存整個識別碼。 若要判斷電腦之前是否曾出現過，請取得使用者名稱的所有識別碼，並呼叫 `matches()` 以檢查是否有任何相符專案。 因為 `matches()` 方法必須用來比較下列專案傳回的值： `MachineId.getBytes`，此選項只有在要比較的值數目較少時（例如，與特定使用者相關聯的電腦）才切實可行。

## 使用者驗證 {#user-authentication}

Adobe Primetime DRM請求可包含驗證權杖。

如果使用使用者名稱/密碼驗證，請求可能包含 `AuthenticationToken` 產生者： `AuthenticationHandler`. 如果您想要存取及驗證Token，您需要使用 `RequestMessageBase.getAuthenticationToken()`. 若要在使用者端上起始使用者名稱/密碼請求，請使用 `DRMManager.authenticate()` ActionScript或iOS API。

如果使用者端和伺服器使用自訂驗證機制，使用者端會透過其他通道取得驗證權杖，並使用設定自訂驗證權杖 `DRMManager.setAuthenticationToken` ActionScript3.0 API。 使用 `RequestMessageBase.getRawAuthenticationToken()` 以取得自訂驗證Token。 伺服器實作會判斷自訂驗證權杖是否有效。

## 重播保護 {#replay-protection}

針對重播保護，您可能想要透過呼叫檢查最近是否看到訊息識別碼 `RequestMessageBase.getMessageId()`. 若是如此，攻擊者可能會嘗試重新執行要求，但應予以拒絕。 若要偵測重播嘗試，伺服器可以儲存最近檢視的訊息ID清單，並根據快取清單檢查每個傳入請求。 若要限制需要儲存訊息識別碼的時間長度，請呼叫 `HandlerConfiguration.setTimestampTolerance()`. 若此屬性已設定，則SDK會拒絕任何包含時間戳記超過伺服器時間指定秒數的請求。

## 復原偵測 {#rollback-detection}

對於復原偵測，某些使用規則會要求使用者端維護執行許可權的狀態資訊。 例如，若要強制執行播放視窗使用規則，使用者端會儲存使用者首次開始檢視內容的日期和時間。 此事件會觸發播放視窗的開始。 為了安全地強制執行播放視窗，伺服器需要確保使用者沒有備份及還原使用者端狀態，以移除儲存在使用者端上的播放視窗開始時間。 伺服器透過追蹤使用者端復原計數器的值來執行此操作。

伺服器會針對每個要求呼叫，以取得計數器的值 `RequestMessageBase.getClientState()` 以取得 `ClientState` 物件，然後呼叫 `ClientState.getCounter()` 以取得使用者端狀態計數器的目前值。 伺服器應該為每個使用者端儲存此值(使用 `MachineId.getUniqueId()` 以識別與倒回計數器值相關聯的使用者端)，然後呼叫 `ClientState.incrementCounter()` 將計數器值增加1。 如果伺服器偵測到計數器值小於伺服器看到的最後一個值，則使用者端狀態可能已復原。

請參閱 `ClientState` API參考檔案，以取得使用者端狀態篡改偵測的詳細資訊。

## 全域伺服器設定資料{#global-server-configuration-data}

除了授權伺服器使用的設定， `HandlerConfiguration` 儲存可傳送給使用者端的設定資訊，以控制如何強制執行授權。 這是透過建立 `ServerConfigData` 類別和呼叫 `HandlerConfiguration.setServerConfigData()`. 這些設定僅套用至此授權伺服器所發行的授權。

時鐘回溯容許度是授權伺服器可以設定的一個屬性，用來控制使用者端執行授權的方式。 依預設，使用者可將電腦時鐘設定回4小時，而不會讓授權失效。 如果授權伺服器操作員想要使用不同的設定，則可以在以下位置設定新值： `ServerConfigData` 類別。 當您變更其中任何設定的值時，請務必透過呼叫來增加版本號碼 `setVersion()`. 只有在使用者端上的版本比目前的版本舊時，才會將新值傳送給使用者端 `ServerConfigData` 版本。

## 跨網域DRM原則檔 {#crossdomain-drm-policy-file}

如果授權伺服器託管在與視訊播放SWF不同的網域上，則為跨網域DRM原則檔( [!DNL crossdomain.xml])才能讓SWF向授權伺服器要求授權。 跨網域DRM原則檔案以XML檔案表示，可讓伺服器指出其資料和檔案可用於SWF從其他網域提供的檔案。 從授權伺服器的跨網域DRM原則檔中指定的網域提供的任何SWF檔，都允許從該授權伺服器存取資料或資產。

Adobe建議開發人員在部署跨網域原則檔案時，僅允許受信任的網域存取授權伺服器，並限制對Web伺服器上授權子目錄的存取，以遵循最佳實務。

如需有關跨領域DRM原則檔案的詳細資訊，請參閱下列位置：

* 網站控制（DRM原則檔）
* 跨網域DRM原則檔案規格： [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)
