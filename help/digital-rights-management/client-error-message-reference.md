---
description: 'DRM用戶端錯誤是TVSDK用戶端錯誤的子集。 '
seo-description: 'DRM用戶端錯誤是TVSDK用戶端錯誤的子集。 '
seo-title: DRM客戶端錯誤消息參考
title: DRM客戶端錯誤消息參考
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '5202'
ht-degree: 1%

---


# DRM客戶端錯誤消息參考 {#client-error-message-reference}

DRM客戶端錯誤是TVSDK客戶端錯誤的子集，與DRM相關的錯誤代碼範圍從3300到3399。

## DRM客戶端錯誤 {#drm-client-errors}

| 錯誤代碼 | 助憶鍵 | 補救 |
|---|---|---|
| 3300 | 無效憑單 | 配銷商的軟體應該如何運作： <ul><li> 如果您使用Google Chrome，而且您處於Incognito模式，而您的Flash Player版本低於11.6，則可能會發生此錯誤。 我們建議播放器檢查瀏覽器的版本號，並建議用戶退出Incognito模式。</li><li> 再次申請授權。 如果請求成功，您不需要記錄或呈報。 如果請求失敗，請記錄導致錯誤的內容。 `subErrorId` 包含行錯誤（如果存在）。</li></ul> 配銷商應該如何： <ul><li> 如果Chrome以外的Flash 11.6版以下的組態未成功重試，封裝中可能會發生錯誤。</li><li>檢查問題是否特定於特定內容並重新封裝。</li></ul> |
| 3301 | 驗證失敗 | 伺服器無法驗證或授權客戶端。<ul><li>配銷商的軟體應採取必要行動，重新建立使用者的認證或引導使用者取得內容存取權。</li><li>配銷商應確認其授權和驗證機制運作正常。 如果發佈商不打算使用驗證或授權功能，他們應檢查違規內容的政策是否需要驗證，並參閱診斷政策／授權差異。</li></ul> 有關此錯誤代碼的詳細資訊，請參 [閱DRM錯誤3301原因和解析度](https://forums.adobe.com/thread/1277149)。 |
| 3302 | RequireSSL | 對於Primetime DRM 4.0和更高版本，當遠端金鑰URL未使用HTTPS做為配置時，此錯誤會在iOS上引發。 需要HTTPS。 <ul><li>如果授權代理商使用的版本早於Primetime DRM 4，或至少是4版，但平台不是iOS，則授權代理商的軟體應記錄錯誤。 此錯誤只會在iOS上擲回。</li><li>如果配銷商的軟體至少是Primetime DRM第4版，而平台是iOS，則配銷商必須將其使用的遠端金鑰伺服器URL變更為HTTPS。 如果他們只使用HTTP，則發佈商可能必須設定HTTPS伺服器。 否則，配銷商必須將記錄的資訊提交給Adobe，並呈報問題。</li></ul> |
| 3303 | ContentExpired | 您檢視的內容已根據內容提供者設定的規則過期。  `subErrorId` 包含特定於客戶機的錯誤或行錯誤。 <ul><li>配銷商的軟體應嘗試從伺服器重新取得授權一次，以判斷是否有新的未過期授權。 如果沒有可用的授權或授權已過期，請允許使用者取得新的授權，或通知使用者內容無法觀看。</li></ul> 如果內容已封裝有過期／終止日期的原則，而授權伺服器記錄檔會報告PolicyEvaluationException，請指出原則結束日期已過期（伺服器錯誤碼303）。 檢查伺服器的日誌檔案以驗證。<br>如果可能，客戶應檢查包裝期間使用的原則，以查看其是否已過期。 Java命令行工具是： <ul><li>java -jar libs/AdobePolicyManager.jar</li><li> detail demo.pol</li><li>配銷商應確認授權到期日是否依預期設定。</li></ul> 如需此錯誤碼的詳細資訊，請參 [閱使用即時串流的AMS/FMS的3303（內容已過期）?](https://forums.adobe.com/thread/1300813) |
| 3304 | 授權失敗 | 目前的使用者未取得檢視內容的授權。 以其他使用者身分登入。<br>如需此錯誤碼的詳細資訊，請參閱錯誤碼3301。 |
| 3305 | ServerConnectionFailed | 由於網路延遲或客戶端離線，與許可證或域伺服器的連接超時。 通常subErrorId包含HTTP傳回程式碼。<ul><li>配銷商的軟體應嘗試連接至已知正常的伺服器。 如果嘗試失敗，提示用戶重新連接到網路。 如果嘗試成功，請記錄它。</li><li>配銷商應確認使用中的任何授權和網域伺服器皆已連線，且可從用戶端網路上檢視。</li></ul>有關此錯誤代碼的詳細資訊，請參 [閱DRM 3305 ServerConnectionFailed原因和解析](https://forums.adobe.com/thread/1284947.) |
| 3306 | ClientUpdateRequired | 目前的用戶端無法完成所要求的動作，但更新的用戶端可以完成請求。<br>這可能有幾個原因：<ul><li>已使用此客戶端上不可用的共用域。 在Chrome上播放時，可能會發生這種情況，但不會是其他瀏覽器，反之亦然。<br>**注意：**Chrome使用的PHDS/PHLS金鑰與其他瀏覽器所使用的不同。</li><li>當應用程式在5.0之前的iOS版本上執行時，會嘗試新增多個DRMSassion。</li><li>只支援第2版時，中繼資料的版本為3或更新版本。</li><li>配銷商的軟體應提醒使用者並中止作業。 如果軟體可以判斷是否提供升級，請以適當的方式引導使用者前往該平台。</li><li>若因共用網域而發生問題，配銷商將需要向Adobe洽詢更新的執行階段或程式庫。 若是Flash執行時期，授權代理商可強制其應用程式直接升級。 若是資料庫，配銷商需要取得更新的資料庫、重建其應用程式，並將它部署給其使用者。</li></ul>如果因多個DRMSassion而發生問題，授權代理商將需要更新其應用程式，以在新增多個DRMSassion之前檢查iOS版本號碼。 或者，他們可以限制將應用程式散發至iOS第5版及更高版本。<br>如果因為中繼資料版本高於第2版而發生問題，則問題可能已損毀中繼資料。 他們可以嘗試重建中繼資料並查看結果。 如果他們仍然發現問題，請記錄問題並呈報至Adobe。<br>有關此錯誤代碼的詳細資訊，請參 [閱How to remedy a 3306 DRMErrorEvent錯誤代碼](https://forums.adobe.com/thread/1266675)。 |
| 3307 | 內部故障 | 這通常代表Primetime DRM程式碼中的錯誤，且未預期，除非有已知錯誤，如以下。subErrorId包含用戶端特定的錯誤或行錯誤。<ul><li>如果瀏覽器是Windows版Chrome，而Flash版本是11.6（SWF版本19或更新版本），授權代理商的軟體應假設使用者按下資訊列上的「拒絕」，並將它視為3368。</li><li>如果3307發生在瀏覽器非Chrome或Flash版本非11.6時，授權代理商應呈報給Adobe。</li></ul>**注意：** 3307:1107296344(FailedToGetBrokerHandle)可能發生在Chrome瀏覽器版本24-28。 |
| 3308 | WrongLicenseKey | 當使用的授權包含解密內容的錯誤金鑰時，就會擲回此錯誤。 subErrorId包含用戶端特定的錯誤或行錯誤。<br>產生此錯誤的方式似乎只有兩種：<ul><li>客戶已修改產生授權的標準Adobe工具（例如授權者伺服器Java架構）。 在這種情況下，授權包含的金鑰可能不對應於任何內容。</li><li>客戶已使用相同的授權ID核發多份授權。 在此情況下，用戶端上有多份可用的授權，這些授權會符合內容中繼資料，而Primetime DRM程式碼已選取錯誤的授權供使用。</li><li>配銷商軟體應嘗試從伺服器重新取得授權。</li><li>如果沒有可用的授權或授權已過期，請為使用者提供工作流程以取得新的授權，或通知使用者內容無法觀看，並記錄問題。</li><li> 如果這是網域系結內容（適用於AIR），請為使用者提供加入網域的方式。</li><li>配銷商應：</li><li> 確認他們尚未自訂Primetime DRM授權伺服器的授權簽發部分。</li><li>確認他們正在為所有授權簽發唯一的授權ID。</li><li>向Adobe呈報問題。</li></ul> |
| 3309 | 損壞的AdditionalHeader | 如果標題大於65536位元組，就會發生此情況。<ul><li>配銷商的軟體應記錄導致錯誤的內容。</li><li>配銷商應確認該錯誤是否可重複於特定內容。 重新封裝損壞的內容。</li></ul> |
| 3310 | AppIDMismatch | 不允許列出應用程式。 Android、iOS或Flash SWF。<br>subErrorId: 郵遞區號1000942; 播放受保護的串流時出錯。 FAXS錯誤。<br>此外，用戶端也可能報告pubID（應用程式發行者ID）的空字串。<br>**Android:**Android應用程式與使用中的應用程式不符。 請記住，Android中除錯密鑰庫的目錄通常與發行密鑰庫的目錄不同。<br>**iOS:** 請參閱TVSDK iOS指南中的「允許清單您的iOS應用程式檔案」。 |
| 3312 | LicenseIntegrity | 再次從伺服器下載授權。 |
| 3313 | WriteMicrosafeFailed | 當系統無法寫入檔案系統時，會發生此問題。 subErrorId包含用戶端特定的錯誤或行錯誤。<br>在Microsoft Windows上，當加密內容的licenseID或policyID過長時，Active X或NPAPI外掛flash播放器可能會擲出錯誤3313。 這是因為Windows中的最大路徑長度。 （Pepper plugin沒有此問題。）<ul><li>配銷商的軟體應提示使用者確認其使用者目錄未鎖定，或是已滿或已鎖定的磁碟區。</li><li>如果配銷商使用AIR而非Flash，則問題可能是路徑長度限制所致。 配銷商應將其AIR應用程式的名稱縮短至合理的名稱。</li></ul> |
| 3314 | 已損壞的DRMMetadata | 此錯誤通常表示內容已與測試PKI憑證封裝，而播放器是使用生產PKI建立，反之亦然。<br>subErrorId包含用戶端特定的錯誤或行錯誤。<ul><li>配銷商的軟體應記錄導致錯誤的內容。</li><li>配銷商應確認錯誤可透過特定內容重制。</li></ul>您可能必須重新封裝損壞的內容。 |
| 3315 | PermissionDenied | 有已知錯誤，當有意使用3305時，可能會拋出此錯誤代碼。 如需詳細資訊，請參閱錯誤碼3305。<br>AIR載入的遠端SWF不允許存取Primetime DRM功能。 如果在網路訪問期間發生安全錯誤，也可能拋出此錯誤代碼。 例如，目標伺服器不使用crossdomain.xml連接客戶端，或者crossdomain.xmlis無法訪問。<br>如需詳細資訊，請參 [閱DRM錯誤3315可能的根本原因和解析度](https://forums.adobe.com/thread/1266592)。 |
| 3317 | AAXS_LoadAdobeCPFailed | **重要：** 這是罕見的錯誤，通常不會發生在生產環境中。<br>如果發生錯誤，您可以執行下列其中一項作業：<ul><li>如果您使用AIR，請重新安裝AIR。</li><li>如果您使用Flash Player，請再次下載AdobeCP模組。</li></ul> |
| 3318 | 不相容AdobeCPVersion | **重要：** 這是罕見的錯誤，通常不會發生在生產環境中。<br>如果發生錯誤，您可以執行下列其中一項作業：<ul><li>如果您使用AIR，請重新安裝AIR。</li><li>如果您使用Flash Player，請再次下載AdobeCP模組。</li></ul> |
| 3319 | 遺漏AdobeCPGetAPI | **重要：** 這是罕見的錯誤，通常不會發生在生產環境中。<br>如果發生錯誤，您可以執行下列其中一項作業：<ul><li>如果您使用AIR，請重新安裝AIR。</li><li>如果您使用Flash Player，請再次下載AdobeCP模組。</li></ul> |
| 3320 | 主機失敗 | **重要：** 這是罕見的錯誤，通常不會發生在生產環境中。<br>如果發生錯誤，您可以執行下列其中一項作業：<ul><li>如果您使用AIR，請重新安裝AIR。</li><li>請再次下載AdobeCP和Flash Player，因為這兩種解決方案都可能不同步。</li></ul>應用程式只需更新Flash Player，就會導致AdobeCP再次下載。 |
| 3321 | I15nFailed | 為客戶端提供密鑰的過程失敗。 subErrorId包含特定於客戶端、特定於伺服器或線路錯誤。<ul><li>配銷商的軟體應至少重試一次。</li></ul>如果您在Windows上使用Google Chrome，請提供如何允許不在沙盒中的外掛程式存取的說明。 如需詳細資訊，請參閱Google Chrome的無沙盒存取遭拒。<ul><li>配銷商應完成下列任一項工作：</li><li>如果錯誤在所有平台上都一致，您應該向Adobe說明問題。</li><li>如果錯誤僅限於Windows上的Chrome，請引導使用者允許未沙盒的外掛程式存取。</li></ul>經銷商應將其SWF更新至19版或更新版本。 對於Chrome特定的3321錯誤，會擲回3368錯誤。 錯誤3368可由配銷商的軟體加以處理。 此項變更是在Chrome Stable頻道26.0.1410.43版中引入。注<br>**意：**錯誤3321:1090519056可能發生在Flash Player 11.1到11.6版。 我們建議您升級至最新的Flash Player版本。<br>如需詳細資訊，請參[閱「DRM錯誤3321原因與解析度」](https://forums.adobe.com/thread/1277138)。 |
| 3322 | DeviceBindingFailed | 設備似乎與初始化時存在的配置不匹配。 subErrorId包含用戶端特定或行錯誤。<br>配銷商軟體應完成下列任一項工作：<ul><li>如果裝置未使用Flash Player，而且使用AIR、iOS等，請呼叫DRMManager.resetDRMVouchers()。</li></ul>如果iOS在開發階段發生問題，請要求開發人員確認在從協力廠商搶鮮版散發系統（例如HockeyApp）下載的建置與從Xcode本機建置之間切換時，是否發現問題。 在從HockeApp分發的組建版本和從Xcode分發的組建版本之間切換時，不會完全覆寫先前安裝的屬性。 這種情況可能會觸發3322錯誤。<br>若要解決此問題，開發人員應先從裝置移除舊版建置，然後再安裝新的建置。<ul><li>如果裝置使用Flash Player，而且無法從3322或3346錯誤碼使用，請參閱Adobe的指示，說明如何在 [DRM Error 3322/3346/3368(Info-Bar Problems)中程式設計重設您的DRM授權商店](https://forums.adobe.com/message/5535907#5535907)。</li></ul>此錯誤預期不會經常發生。 在使用漫遊配置檔案的公司環境中，如果用戶正在查看受DRM保護的內容，則當用戶從不同電腦登錄時發生的機會錯誤3322增加。 如果可能，配銷商應嘗試從使用者取得此項資訊。<br>如果錯誤經常發生，請呈報至Adobe。 您必須通知Adobe重設授權商店是否確實（或未）解決問題，並告知Adobe發生錯誤的瀏覽器。<br>如需詳細資訊，請參閱下列文章：<ul><li>https://forums.adobe.com/message/5520902</li><li>https://forums.adobe.com/message/5535911</li><li>https://forums.adobe.com/message/5748618</li><li>https://forums.adobe.com/message/6061165</li></ul> |
| 3323 | CorruptGlobalStateStore | DRM客戶端使用的檔案已意外修改。 subErrorId包含用戶端特定或行錯誤。<ul><li>配銷商的軟體應引導使用者以與錯誤碼3322相同的方式重設。</li><li>如果GlobalStore的故障率高於使用者群的硬碟的預期故障率，請將問題呈報給Adobe。</li></ul> |
| 3324 | MachineTokenInvalid | 許可證伺服器可能無法連接到證書撤銷清單(CRL)伺服器以刷新其CRL檔案，或者客戶機正在請求已被許可證伺服器撤銷的許可證／驗證。<br>在伺服器記錄檔中，錯誤碼111 isMachineTokenInvalid。 但是，在用戶端層級，錯誤碼111會轉換為錯誤碼3324。<br>DRM授權伺服器管理員應檢查客戶的授權伺服器是否能夠擷取Adobe CRL檔案。 如果客戶使用Tomcat，則客戶可以檢查tomcat/temp/目錄，以查看是否有4個。CRL檔案。<ul><li>如果檔案位於此目錄中，請按兩下Windows資源管理器和CRL查看器應用程式中的檔案，確定是否有任何檔案已過期。</li><li>如果tomcat/temp/中沒有檔案，則可以假定此許可證伺服器由於防火牆或路由問題而無法訪問Adobe CRL伺服器。</li></ul>如需詳細資訊，請參閱防火牆規則。<br>如果CRL檔案不可用或已過期，則必須確認是否可以訪問許可證伺服器。 在客戶的許可證伺服器上開啟網路嗅探器（如Charles或Wireshark），重新啟動伺服器，並讓客戶端嘗試向伺服器請求許可證。<br>您可以觀察網路流量，以查看對下列URL端點的呼叫是否成功：<br>**注意：**您也可以在瀏覽器中輸入下列CRL URL，以查看您是否可以手動下載每個檔案。<ul><li>[https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl](https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl)</li><li>[https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl](http://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl)</li><li>[https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl](http://crl2.adobe.com/Adobe/FlashAccessRootCA.crl)</li><li>[https://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl](http://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl)</li></ul>如果防火牆規則已開啟且目前沒有3324錯誤，則可能會發生暫時網路問題。 檢查客戶的伺服器日誌（可能位於/tomcat/logs/目錄中），以確定當許可證伺服器嘗試提取證書撤銷清單時是否發生錯誤。<br>**注意：**當大量（或拆分）的客戶端在更新CRL檔案時向臨時網路問題報告3324錯誤時，可能會發生錯誤。 解決網路問題時，3324問題也已解決。<br>如果tomcat/temp/目錄中存在所有4個CRL檔案，且客戶端仍然收到3324錯誤，則CRL檔案可能存在檔案訪問問題。<br>要解決此問題，您可能需要查看日誌並清除現有的CRL檔案。<br>如果沒有伺服器問題，請提示使用者重設，如錯誤碼3322所述。 |
| 3325 | CorruptServerStateStore | DRM客戶端使用的檔案已意外修改。 subErrorId包含用戶端特定或行錯誤。<ul><li>配銷商的軟體應再次重試該操作，因為AdobeCP已在內部刪除了違規的伺服器存放區，且應成功重試。 如果重試失敗，請記錄問題。</li><li>如果重試失敗的速率高於使用者群中硬碟的預期失敗率，請將問題呈報給Adobe。</li></ul> |
| 3326 | StoreHapperingDetected | 授權存放區已遭到竄改或損毀，無法再使用。<br>配銷商的軟體應引導使用者以與錯誤碼3322所述相同的方式重設。 |
| 3327 | ClockHapperingDetected | 修正時鐘或再次取得授權／授權／網域授權。 |
| 3328 | ServerErrorTryAgain | 這是伺服器端錯誤，伺服器無法從用戶端完成請求。 例如，當伺服器忙、HTTP/500、伺服器沒有解密請求所需的密鑰等時，可能會發生此錯誤。<br>在客戶端上，沒有辦法確定出了什麼問題。 客戶必須檢閱Primetime DRM伺服器記錄檔（通常稱為AdobeFlashAccess.log），以判斷出錯之處。 記錄檔中總是有描述性很強的堆疊追蹤，以指出問題。 subErrorId包含伺服器特定或行錯誤。<br>配銷商應查看伺服器記錄，以識別是哪個伺服器傳送此錯誤。 對於具有子錯誤代碼101的3328錯誤，伺服器無法解密請求。 客戶必須驗證安裝在許可證伺服器上的許可證／傳輸伺服器證書是否與打包期間使用的證書匹配並對應。<br>此外，如果客戶使用「參考實作」，則必須確保flashaccessrefimpl.properties檔案中沒有字型錯誤，而指定了主要和其他憑證。<br> |
| 3329 | ApplicationSpecificError | Primetime DRM不知道應用程式專用的子錯誤碼。 subErrorId包含來自發佈者自訂授權伺服器的伺服器特定錯誤。 伺服器在應用程式特定的命名空間中傳回錯誤。 |
| 3330 | NeedAuthentication | 當內容設定為要求用戶端在取得授權之前進行驗證時，就會發生此錯誤。<ul><li>配銷商的軟體應驗證使用者，然後再次取得授權。 如果您的服務不想使用驗證，請記錄造成此錯誤的內容的識別碼。</li><li>此錯誤不應需要呈報，除非內容不應設定為需要驗證。 在這種情況下，請使用適當的原則重新封裝違規內容。 如果內容封裝正確，請參閱診斷原則／授權差異。</li></ul> |
| 3331 | ContentNotYetValid | 取得的授權尚無效。 要解決此問題，請檢查客戶機時鐘設定是否正確。 要設定客戶端時鐘，請重新打包內容或修改許可證伺服器配置。 |
| 3332 | CachedLicenseExpired | 再次從伺服器取得授權。 |
| 3333 | PlaybackWindowExpired | 您必須通知使用者，在原則到期之前，他們無法播放此內容。 |
| 3334 | InvalidDRMPlatform | 此平台不允許播放內容，因為例如，內容提供者已設定Primetime DRM，以拒絕在平台上的Primetime DRM的內容或共用網域系結授權，系結至用於不同分區的共用網域Token。<br>如果內容未使用適當的（CDM功能選定）封裝器認證來封裝，CDM可能會擲出此錯誤。 如需詳細資訊，請參閱CDM功能門控。<br>如果內容封裝有不正確的PHDS/PHLS憑證，則內容可能適用於Chrome，但不適用於其他瀏覽器（反之亦然）。<br>**注意：**這是因為Chrome使用不同的PHDS/PHLS憑證。<br>若要確認使用的憑證，請轉儲內容中繼資料的詳細資料，並尋找收件者憑證。 |
| 3335 | InvalidDRMVersion | 要解決此問題，請完成以下任務之一：<ul><li>升級AIR</li><li>對於Flash Player，請升級AdobeCP模組並重試播放。</li></ul> |
| 3336 | InvalidRuntimePlatform | 此平台不允許播放內容，因為例如，內容提供者已設定Primetime DRM，以拒絕在平台上傳送內容給FP/AIR。 |
| 3337 | InvalidRuntimeVersion | 如果內容或伺服器設定為拒絕播放特定版本的Flash或AIR執行階段，就會發生此情況。<ul><li>如果使用者使用可升級Flash的作業系統，配銷商的軟體應提示使用者升級Flash，然後再試一次。 否則，建議使用者使用不同的機器。</li><li>如果懷疑有錯誤3337s，請識別是否發生在特定內容上，並重新封裝該內容。 如果正確封裝內容，請參閱診斷原則／授權差異。</li></ul> |
| 3338 | UnknownConnectionType | 無法檢測連接類型，策略要求您開啟「輸出保護」。 只有當內容封裝為需要數位或模擬輸出保護時，才會出現此問題。<br>11.8.800.168舊版Flash Player中的問題，有時會在原則指出內容保護為「USE IF AVAILABLE」的內容上發生錯誤3338。 此問題已在11.8.800.168版及更新版本中修正。<ul><li>配銷商的軟體選擇不需要輸出保護的內容變體（例如HD串流的SD變體）。 如果USE_IF_AVAILABLE內容發生錯誤3338，請檢查播放器版本號。 如果播放器版本低於11.8.800.168，建議使用者升級Flash Player。 如果錯誤3338發生在11.8.800.168以上的版本上，請記錄導致錯誤的內容。</li><li>配銷商應檢查哪些內容造成此錯誤，並驗證內容的原則是否設定NO_PROTECTION或USE_IF_AVAILABLE用於模擬和數位輸出。 如果內容不慎封裝為NO_OUTPUT或REQUIRED，請重新封裝內容。 如果正確封裝內容，請參閱診斷原則／授權差異。 否則呈報至Adobe。</li></ul>如需詳細資訊，請 [參閱「當您的DRM原則設為USE_IF_AVAILABLE時，發生未預期的3338錯誤](https://forums.adobe.com/message/5518688)?」 |
| 3339 | NoAnalogPlaybackAllowed | 無法在模擬設備上播放。 若要解決此問題，請連接數位裝置。 |
| 3340 | NoAnalogProtectionAvail | 無法播放內容，因為連接的模擬外部顯示設備（顯示器／電視）沒有正確的功能（例如，設備沒有Macrovision或ACP）。 |
| 3341 | NoDigitalPlaybackAllowed | 無法在數位裝置上播放內容。 |
| 3342 | NoDigitalProtectionAvail | 連接的數字外部顯示設備（顯示器／電視）沒有正確的功能。 例如，設備沒有HDCP。 |
| 3343 | 內部錯誤 | 目前已知此錯誤會在新版Flash發行後開始發生。 之所以會發生，是因為Flash在開啟時會升級Flash，使Flash在瀏覽器重新啟動之前處於不良狀態。<ul><li>配銷商軟體應完成下列工作：</li><li>建議使用者關閉或結束所有瀏覽器，然後重新開啟。</li><li>檢查Flash版本是否為最新版本。</li></ul>如果版本不是最新版本，建議客戶升級、關閉其瀏覽器中的所有標籤，然後重新開啟。<ul><li>如果瀏覽器重新啟動成功後發生錯誤，請呈報至Adobe。 當新版本發行時，我們建議您連絡Adobe支援，以查看背景更新問題是否已修正。</li></ul> |
| 3344 | MissingAdobeCPModule | Flash或AIR的部分安裝不正確。<br>要解決此問題，請完成以下任務之一：<ul><li>對於AIR，使用者必須重新解除安裝並安裝AIR。</li><li>若為Flash Player，請呼叫System.update。</li></ul> |
| 3346 | 遷移失敗 | 配銷商軟體應執行下列其中一項作業：<ul><li>如果是AIR，請呼叫DRMManager.resetDRMVouchers()。</li><li>如果Flash因錯誤3322或3346而無法使用，使用者應前往 [https://forums.adobe.com/message/5535907#5535907](https://forums.adobe.com/message/5535907#5535907) ，並依照Adobe文章的指示，以程式設計方式重設其DRM授權商店。</li><li>如果此錯誤頻發，配銷商應向Adobe提供頻率播放器版本和瀏覽器版本的詳細資訊。</li></ul>如需詳細資訊，請參閱下列論壇文章：<ul><li>[Chrome中的DRM錯誤3322/3346/3368（資訊列問題）](https://forums.adobe.com/message/5520902)</li><li>[硬體變更後出現3322或3346錯誤](https://forums.adobe.com/message/5535911)</li></ul> |
| 3347 | IndefouldDeviceCapabilities | 此錯誤的主要含義是授權有用戶端的DRM憑證指出其無法滿足的限制。 下列「硬體功能」是在發出用戶端DRM憑證時定義的：<ul><li>**非用戶可訪問匯流排。** 如果 **為真**，解密的媒體絕不會流過匯流排，也不會流入應用程式可存取的主記憶體。 如果 **為false**，則在解密後，應用程式可能會存取內容。</li><li>**硬體信任根。** 如果 **為true**，則啟動時在設備上載入的所有軟體都將通過僅在硬體中提供的密鑰或摘要進行驗證。 當針對用戶端的DRM憑證開啟授權時，這兩個限制都會在用戶端進行檢查，而且立即發生故障。 在核發授權之前，您也可以在伺服器端檢查這些限制。</li></ul>此錯誤的次要含義是授權已設定「Jailbreak Enforcement」（越獄執行）政策，且裝置上已偵測到越獄。 此檢查會在用戶端定期執行，且無法在伺服器端進行檢查。<br>配銷商可以更新政策並移除限制。 對於設備功能策略，請使用-devCapabilitiesV1標誌發出策略更新命令，而不使用參數。 用於jailbreak enforcement setpolicy.enforceJailbreak=false。 |
| 3348 | HardStopIntervalExpired | 硬停止間隔已過期。 |
| 3349 | ServerVersionTooHigh | 伺服器運行的版本高於客戶端支援的最高版本。 |
| 3350 | ServerVersionTooLow | 伺服器的執行版本低於用戶端支援的最低版本。 |
| 3351 | DomainTokenInvalid | 網域Token無效。 若要解決此問題，請再次向網域註冊。 |
| 3352 | DomainTokenTooOld | 網域Token比授權所需的Token舊。 若要解決此問題，請再次向網域註冊。 |
| 3353 | DomainTokenTooNew | 網域Token比授權所需的Token新。 |
| 3354 | DomainTokenExpired | 網域Token已過期。 |
| 3355 | DomainJoinFailed | 域連接失敗。 |
| 3356 | NoConterpongRoot | 找不到V3葉片許可證的根許可證。 |
| 3357 | NoValidEmbeddedLicense | 未找到有效的嵌入式許可證。 |
| 3358 | NoACPProtectionAvailable | 由於連接的模擬設備沒有ACP保護，因此無法回放。 |
| 3359 | NoCGSMAProtectionAvailable | 由於連接的模擬設備沒有CGMSA保護，因此無法播放。 |
| 3360 | DomainRegistrationRequired | 內容需要網域註冊。 |
| 3361 | NotRegisteredToDomain | 電腦未註冊到指定元資料的域。 |
| 3362 | OperationTimeoutError | 非同步操作所花的時間比配置的maxOperationTimeout長。<br>**注意：**此錯誤代碼僅由iOS DRMNative Framework傳回。 |
| 3363 | UnsupportedIOSPlaylistError | M3U8播放清單包含不支援的內容，或遺失必要的#EXT-X-FAXS-CM DRM中繼資料物件。<br>**注意：**此錯誤代碼僅由iOS DRMNative Framework傳回。 |
| 3364 | NoDeviceId | 框架請求設備ID，但返回的值為空。<br>框架請求設備ID，但返回的值為空。<br>在Chrome瀏覽器設定中，使用者不應選取「允許受保 **護內容的識別碼** 」核取方塊。 |
| 3365 | IncognitoModeNotAllowed | 此瀏覽器／平台組合不允許在Incognito模式下播放受DRM保護的內容。<br>配銷商的軟體應建議使用者退出Incognito模式或使用不同的瀏覽器。 如需詳細資訊，請參 [閱「DRM錯誤3365原因與解析度」](https://forums.adobe.com/thread/1266622)。 |
| 3366 | BadParameter | 主機執行時期會以錯誤的參數呼叫Primetime DRM程式庫。 |
| 3367 | BadSignature | M3U8資訊清單簽署失敗。<br>**注意：**此錯誤代碼僅由iOS DRMNative Framework或AVE傳回。 |
| 3368 | UserSettingsNoAccess | 用戶取消了操作或輸入了不允許訪問系統的設定。<br>此錯誤只會在SWF 19版或更新版本中擲回。 為了向後相容，SWF 18版或更舊版本會擲回錯誤碼3321。<br>配銷商的軟體應引導使用者說明如何允許無沙盒外掛程式存取。 如需詳細資訊，請參 [閱Chrome中Google Chrome的無沙盒存取被拒絕](https://helpx.adobe.com/adobe-access/kb/error-3321.html) , [以及Chrome（資訊列問題）中的DRM錯誤3322/3346/3368](https://forums.adobe.com/message/5520902)。 |
| 3369 | InterfaceNotAvailable | 不提供所需的瀏覽器介面。 此問題僅發生在Pepper上。 Flash外掛程式和瀏覽器版本可能不相符。<br>散發者的軟體應引導使用者確保已安裝最新版本的瀏覽器。<br>如果此錯誤的發生率增加，並對應於已發佈的瀏覽器更新，則呈報至Adobe。 |
| 3370 | ContentIdSettingsNoAccess | 使用者已停用「允許 **保護內容識別碼」設定。**<br>**注意：** Pepper 13.0.0.x版或更新版本會出現此錯誤。<br>配銷商的軟體和／或營運團隊應引導使用者啟用「允許識別 **碼」以設定受保護的內容** 。<br>如需詳細資訊，請參 [閱https://forums.adobe.com/message/6518323#6518323](https://forums.adobe.com/message/6518323#6518323)。 |
| 3371 | NoOPConstraintInPixelConstraints | 基於許可證中輸出保護約束的格式錯誤的解析。<br>配銷商的軟體應顯示錯誤訊息。 要求使用者以內容標題向配銷商報告問題。<br>配銷商應以有效政策重新封裝內容。 |
| 3372 | 解析度LagerThanMax解析度 | 內容的解析度大於輸出保護約束中指定的最大解析度。<br>如果授權代理商的營運團隊在記錄中發現此錯誤，則應檢閱以解析度為基礎的輸出保護政策，並視需要重新封裝內容。<br>有關基於解析度的輸出保護的詳細資訊，請參閱關於基於解析度的輸出保護。 |
| 3373 | DisplayResolutionLagerThanConstrain | 內容的解析度大於當前活動的輸出保護約束所指定的解析度。<br>如果授權代理商的營運團隊在記錄中發現此錯誤，則應檢閱以解析度為基礎的輸出保護政策，並視需要重新封裝內容。<br>有關基於解析度的輸出保護的詳細資訊，請參閱關於基於解析度的輸出保護。 |
| 3374 | ClientCommProcessFailed | 在用戶端通訊處理期間失敗，例如請求產生、回應處理、錯誤驗證Token等。 |

## 3328的子錯誤代碼映射 {#suberror-code-mapping-for-3328}

| 子錯誤 | 說明 |
|---|---|
| 100-1000 | 由Adobe的License Server保留 |
| 10000 - 20000 | 由Adobe的個人化伺服器保留 |
| 20100-21000 | 為Adobe Xbox鑰匙伺服器保留。<br>此範圍中的錯誤對應至一般的Primetime DRM伺服器SDK錯誤訊息參考，如下所示：<br>Xbox keyserver錯誤= DRM伺服器錯誤+ 0x2000<br>例如，Xbox Keyserver錯誤20202等同於DRM伺服器SDK錯誤202 |
| 100xxxx | 保留給客戶機子錯誤代碼 |