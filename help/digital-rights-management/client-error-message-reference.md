---
description: DRM使用者端錯誤是TVSDK使用者端錯誤的子集。
title: DRM使用者端錯誤訊息參考
exl-id: 3d74cb92-c0a7-4eab-91b8-7e60a9c33df4
source-git-commit: 1bc2f6c230c262babf2958c32fee31afcad04c2f
workflow-type: tm+mt
source-wordcount: '5173'
ht-degree: 1%

---

# DRM使用者端錯誤訊息參考 {#client-error-message-reference}

DRM使用者端錯誤是TVSDK使用者端錯誤的子集，與DRM相關的錯誤碼範圍從3300到3399。

## DRM使用者端錯誤 {#drm-client-errors}

| 錯誤代碼 | 助記鍵 | 補救措施 |
|---|---|---|
| 3300 | 無效的憑單 | 分銷商的軟體應該做什麼： <ul><li> 如果您使用Google Chrome，且處於無痕模式，而Flash Player版本低於11.6，則可能會發生此錯誤。 我們建議播放器檢查瀏覽器的版本號碼，並建議使用者退出無痕模式。</li><li> 再次要求授權。 如果請求成功，您就不需要記錄或呈報。 如果要求不成功，請記錄造成錯誤的內容。 `subErrorId` 包含行錯誤（如果存在）。</li></ul> 分銷商應該做什麼： <ul><li> 如果Flash低於11.6版的Chrome以外的設定重試失敗，封裝中可能會發生失敗。</li><li>檢查該問題是否特定於某些內容並重新封裝。</li></ul> |
| 3301 | 驗證失敗 | 伺服器無法驗證或授權使用者端。<ul><li>散發者的軟體應採取任何必要的動作來重新建立使用者的認證，或引導使用者取得內容的存取權。</li><li>散發者應確認其授權和驗證機制正常運作。 如果經銷商不打算使用驗證或授權功能，他們應該檢查違規內容的原則是否需要驗證，並參閱診斷原則/授權差異。</li></ul> 如需此錯誤碼的詳細資訊，請參閱 [DRM錯誤3301原因和解決方法](https://forums.adobe.com/thread/1277149). |
| 3302 | RequireSSL | 對於Primetime DRM 4.0和更新版本，當遠端金鑰URL未使用HTTPS作為配置時，會在iOS上擲回此錯誤。 需要HTTPS。 <ul><li>如果散發者使用的版本比Primetime DRM版本4舊，或至少是版本4，但平台不是iOS，散發者的軟體應該記錄錯誤。 此錯誤只會在iOS上擲回。</li><li>如果發行商的軟體至少是Primetime DRM版本4，而且平台是iOS，則發行商必須將其使用的遠端金鑰伺服器URL變更為HTTPS。 如果他們只使用HTTP，經銷商可能必須設定HTTPS伺服器。 否則，分銷商需要提交記錄的資訊以Adobe和升級問題。</li></ul> |
| 3303 | ContentExpired | 根據內容提供者設定的規則，您正在檢視的內容已過期。  `subErrorId` 包含使用者端特有的錯誤或行錯誤。 <ul><li>散發者的軟體應嘗試從伺服器重新取得授權一次，以判斷是否有新的未到期授權可用。 如果沒有可用的授權或授權已過期，請允許使用者取得新的授權，或通知使用者無法觀看內容。</li></ul> 如果內容已封裝有過期/結束日期無效的原則，且授權伺服器記錄報告PolicyEvaluationException，請指出原則結束日期已過期（伺服器錯誤碼303）。 檢查伺服器的記錄檔以進行驗證。<br>如果可行，客戶應檢查打包期間使用的原則，檢視是否已過期。 Java命令列工具是： <ul><li>java -jar libs/AdobePolicyManager.jar</li><li> detail demo.pol</li><li>分銷商應確認授權到期日是否按預期配置。</li></ul> 如需此錯誤碼的詳細資訊，請參閱 [3303 （內容已過期）與AMS/FMS使用即時資料流？](https://forums.adobe.com/thread/1300813) |
| 3304 | AuthorizationFailed | 目前使用者無權檢視內容。 以其他使用者身分登入。<br>如需此錯誤碼的詳細資訊，請參閱錯誤碼3301。 |
| 3305 | ServerConnectionFailed | 由於網路延遲或使用者端離線，與授權或網域伺服器的連線逾時。 通常，subErrorId包含HTTP傳回碼。<ul><li>散發者的軟體應嘗試與已知正常之伺服器進行網路連線。 如果嘗試失敗，則提示使用者重新連線到網路。 如果嘗試成功，則將其記錄。</li><li>散發者應確認任何使用中的授權和網域伺服器已上線，且可從使用者端網路中看到。</li></ul>如需此錯誤碼的詳細資訊，請參閱 [DRM 3305 ServerConnectionFailed原因和解決方法](https://forums.adobe.com/thread/1284947.) |
| 3306 | ClientUpdateRequired | 目前的使用者端無法完成要求的動作，但更新的使用者端可能能夠完成要求。<br>這可能有幾個原因：<ul><li>使用的共用網域在此使用者端上無法使用。 當播放在Chrome上運作時可能會發生這種情況，但其他任何瀏覽器都無法運作，反之亦然。<br>**注意：** Chrome使用的PHDS/PHLS金鑰與其他瀏覽器使用的不同。</li><li>應用程式嘗試在5.0之前的iOS版本上執行時新增多個DRMSession。</li><li>僅支援版本2時，中繼資料的版本為3或更高版本。</li><li>散發者的軟體應提醒使用者並中止作業。 如果軟體有辦法判斷是否有升級可用，請以適合平台的方式將使用者導向該升級。</li><li>如果問題是因為共用網域而發生，散發者將需要向Adobe檢查更新的執行階段或程式庫。 在Flash執行階段的情況下，散發者可以直接在其應用程式中強制升級。 若是程式庫，散發者需要取得更新的程式庫、重建其應用程式並將其部署給使用者。</li></ul>如果問題因多個DRMSessions而發生，發行者將需要更新其應用程式以在新增多個DRMSessions之前檢查iOS版本號碼。 或者，他們也可以限制將其應用程式發佈到iOS版本5及更高版本。<br>如果問題是因為中繼資料版本高於版本2而發生，則問題可能是中繼資料損毀。 他們可以嘗試重建中繼資料並檢視結果。 如果他們持續看到問題，請記錄問題並升級至Adobe。<br>如需此錯誤碼的詳細資訊，請參閱 [如何補救3306 DRMErrorEvent錯誤碼](https://forums.adobe.com/thread/1266675). |
| 3307 | InternalFailure | 這通常表示Primetime DRM程式碼中的錯誤，除非有已知錯誤，否則不會預期到。subErrorId包含使用者端特有的錯誤或行錯誤。<ul><li>如果瀏覽器在Windows上為Chrome，而Flash版本為11.6 (SWF版本19或更高版本)，則散發者的軟體應假設使用者在資訊列上按下「拒絕」，並將此視為相同的3368。</li><li>如果瀏覽器不是Chrome或Flash版本不是11.6時發生3307，則分銷商應升級至Adobe。</li></ul>**注意：** 3307：1107296344 (FailedToGetBrokerHandle)可能會在Chrome瀏覽器24-28版中發生。 |
| 3308 | WrongLicenseKey | 當使用的授權包含解密內容的錯誤金鑰時，就會擲回此錯誤。 subErrorIdentifis包含使用者端特有的錯誤或行錯誤。<br>產生此錯誤的方式似乎只有兩種：<ul><li>客戶已修改用於產生授權的標準Adobe工具（例如，授權者伺服器Java架構）。 在此情況下，授權包含可能未對應到任何內容的錯誤金鑰。</li><li>客戶已使用相同的授權ID核發多個授權。 在這種情況下，使用者端上有多個符合內容中繼資料的可用授權，且Primetime DRM程式碼已選取了錯誤的授權使用。</li><li>散發者的軟體應嘗試從伺服器重新取得授權。</li><li>如果沒有可用的授權或授權已過期，請提供工作流程讓使用者取得新授權，或通知使用者無法觀看內容，並記錄問題。</li><li> 如果這是網域繫結內容(適用於AIR)，請提供讓使用者加入網域的方式。</li><li>散發者應：</li><li> 確認他們尚未自訂Primetime DRM授權伺服器的授權發行部分。</li><li>驗證他們是否核發所有授權的唯一授權ID。</li><li>呈報Adobe的問題。</li></ul> |
| 3309 | CorruptedAdditionalHeader | 如果標題大於65536位元組，就會發生這種情況。<ul><li>散發者的軟體應記錄導致錯誤的內容片段。</li><li>散發者應確認錯誤可透過特定內容片段重現。 重新封裝中斷的內容。</li></ul> |
| 3310 | AppIDMismatch | 不允許列出應用程式。 Android、iOS或FlashSWF。<br>subErrorId： 1000942；播放受保護的資料流時發生錯誤。 FAX錯誤。<br>使用者端可能也會回報pubID （應用程式發佈者ID）的空字串。<br>**Android：** Android應用程式與正在使用的應用程式不相符。 請記住，Android中除錯金鑰存放區的目錄通常與發行金鑰存放區的目錄不同。<br>**iOS：** 請參閱 [允許列出您的iOS應用程式](/help/programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) TVSDK iOS指南中的檔案。 |
| 3312 | Licenseintegrity | 再次從伺服器下載授權。 |
| 3313 | WriteMicrosafeFailed | 當系統無法寫入檔案系統時，就會發生此問題。 subErrorIdcontains使用者端特有的錯誤或行錯誤。<br>在Microsoft Windows上，當加密的內容具有licenseID或policyID太長時，Active X或NPAPI外掛程式flash player可能會擲回錯誤3313。 這是因為Windows中的路徑長度上限。 （Pepper外掛程式沒有這個問題。）<ul><li>散發者的軟體應提示使用者確認其使用者目錄未鎖定，或位於已滿或已鎖定的磁碟區上。</li><li>如果散發者使用AIR而非Flash，則問題可能是由於路徑長度限制所造成。 經銷商應將其AIR應用程式的名稱縮短為合理名稱。</li></ul> |
| 3314 | CorruptedDRMMetadata | 此錯誤通常表示內容已搭配測試PKI憑證封裝，而播放器是搭配生產PKI建置，反之亦然。<br>subErrorId包含使用者端特有的錯誤或行錯誤。<ul><li>散發者的軟體應記錄導致錯誤的內容片段。</li><li>散發者應確認錯誤可透過特定內容片段重現。</li></ul>您可能必須重新封裝損毀的內容。 |
| 3315 | PermissionDenied | 已知的Bug會在預期3305時擲回此錯誤碼。 如需詳細資訊，請參閱錯誤代碼3305。<br>AIR載入的遠端SWF不允許存取Primetime DRM功能。 如果在網路存取期間發生安全性錯誤，也會擲回此錯誤碼。 例如，目的地伺服器未透過crossdomain.xml連線的使用者端，或無法連線crossdomain.xmlis。<br>如需詳細資訊，請參閱 [DRM錯誤3315可能的根本原因和解決方法](https://forums.adobe.com/thread/1266592). |
| 3317 | AAXS_LoadAdobeCPFailed | **重要：** 這是罕見的錯誤，通常不會發生在生產環境中。<br>如果發生錯誤，您可以執行下列任一項作業：<ul><li>如果您使用AIR，請重新安裝AIR。</li><li>如果您正在使用Flash Player，請再次下載AdobeCP模組。</li></ul> |
| 3318 | IncompatibleAdobeCPVersion | **重要：** 這是罕見的錯誤，通常不會發生在生產環境中。<br>如果發生錯誤，您可以執行下列任一項作業：<ul><li>如果您使用AIR，請重新安裝AIR。</li><li>如果您正在使用Flash Player，請再次下載AdobeCP模組。</li></ul> |
| 3319 | MissingAdobeCPGetAPI | **重要：** 這是罕見的錯誤，通常不會發生在生產環境中。<br>如果發生錯誤，您可以執行下列任一項作業：<ul><li>如果您使用AIR，請重新安裝AIR。</li><li>如果您正在使用Flash Player，請再次下載AdobeCP模組。</li></ul> |
| 3320 | 主機失敗 | **重要：** 這是罕見的錯誤，通常不會發生在生產環境中。<br>如果發生錯誤，您可以執行下列任一項作業：<ul><li>如果您使用AIR，請重新安裝AIR。</li><li>下載AdobeCP和FlashPlayeragree，因為任一解決方案可能不同步。</li></ul>應用程式只需要更新Flash Player，這會導致再次下載AdobeCP。 |
| 3321 | I15nFailed | 提供金鑰給使用者端的程式失敗。 subErrorId包含使用者端特有、伺服器特有或行錯誤。<ul><li>散發者的軟體應至少重試一次作業。</li></ul>如果您在Windows上使用Google Chrome，請提供說明來說明如何允許不在沙箱中的外掛程式存取。 如需詳細資訊，請參閱Google Chrome的非沙箱存取遭拒。<ul><li>散發者應完成下列其中一項工作：</li><li>如果錯誤在各平台間是一致的，您應使用Adobe來重新計算問題。</li><li>如果錯誤僅限於Windows上的Chrome，請引導使用者允許無沙箱外掛程式存取。</li></ul>經銷商應將其SWF更新至版本19或更新版本。 對於Chrome特定的3321錯誤，會擲回3368錯誤。 錯誤3368可以由散發者的軟體更具體處理。 此變更已在Chrome穩定通道26.0.1410.43版中引入。<br>**注意：** Flash播放器版本11.1到11.6可能發生錯誤3321：1090519056。建議您升級至最新的Flash Player版本。<br>如需詳細資訊，請參閱 [DRM錯誤3321原因與解決方法](https://forums.adobe.com/thread/1277138). |
| 3322 | DeviceBindingFailed | 裝置似乎不符合初始化時存在的設定。 subErrorId包含使用者端特有的錯誤或行錯誤。<br>散發者的軟體應完成下列其中一項作業：<ul><li>如果裝置未使用Flash Player，而是使用AIR、iOS等， `callDRMManager.resetDRMVouchers()`.</li></ul>如果iOS在開發階段發生問題，請要求開發人員確認在從協力廠商發行前發佈系統（例如HockeyApp）下載的組建與從Xcode下載的本機組建之間切換時，是否發現問題。 在從HockeyApp分發的組建和從Xcode分發的組建之間切換時，不會完全覆寫先前安裝的屬性。 這種情況可能會觸發3322錯誤。<br>若要解決此問題，開發人員應先從裝置移除舊版組建，然後再安裝新版組建。<ul><li>如果裝置正在使用Flash Player，且無法從3322或3346錯誤代碼使用，請參閱Adobe中有關如何以程式設計方式重設您的DRM授權存放區的指示。 [Chrome中的DRM錯誤3322/3346/3368 （資訊列問題）](https://forums.adobe.com/message/5535907#5535907).</li></ul>此錯誤預計不會頻繁發生。 在使用漫遊設定檔的公司環境中，如果使用者檢視受DRM保護的內容，則當使用者從不同電腦登入時，發生錯誤3322的可能性會增加。 如有可能，散發者應嘗試從使用者取得此資訊。<br>如果錯誤經常發生，請升級至Adobe。 您必須通知Adobe重設授權存放區是否解決此問題，並告知Adobe在哪些瀏覽器上發生錯誤。<br>如需詳細資訊，請參閱下列文章：<ul><li>https://forums.adobe.com/message/5520902</li><li>https://forums.adobe.com/message/5535911</li><li>https://forums.adobe.com/message/5748618</li><li>https://forums.adobe.com/message/6061165</li></ul> |
| 3323 | CorruptedGlobalStateStore | DRM使用者端使用的檔案已被意外修改。 subErrorIdentifis包含使用者端特有的錯誤或行錯誤。<ul><li>散發者的軟體應該會以錯誤碼3322的相同方式引導使用者重設。</li><li>如果GlobalStore的故障率高於使用者群硬碟的預期故障率，請將問題升級至Adobe。</li></ul> |
| 3324 | MachineTokenInvalid | 授權伺服器可能無法連線到憑證撤銷清單(CRL)伺服器來重新整理其CRL檔案，或是使用者端電腦正在要求由授權伺服器撤銷的授權/驗證。<br>在伺服器記錄檔中，錯誤碼111 isMachineTokenInvalid。 不過，在使用者端層級，錯誤碼111會轉譯為錯誤碼3324。<br>DRM授權伺服器管理員應檢查客戶的授權伺服器是否曾經能夠擷取AdobeCRL檔案。 如果客戶使用Tomcat，則可檢查tomcat/temp/目錄以檢視是否有4個.CRL檔案。<ul><li>如果檔案位於此目錄中，請在Windows檔案總管和CRL檢視器應用程式中連按兩下檔案，判斷是否有任何檔案已過期。</li><li>如果tomcat/temp/中沒有檔案，則可以假設由於防火牆或路由問題，此授權伺服器永遠無法連線到AdobeCRL伺服器。</li></ul>如需詳細資訊，請參閱防火牆規則。<br>如果CRL檔案無法使用或已過期，您必須確認是否可以連線到授權伺服器。 在客戶的授權伺服器上開啟網路Sniffer （例如Charles或Wireshark），重新啟動伺服器，並讓使用者端嘗試從伺服器要求授權。<br>您可以觀察網路流量，以檢視對以下URL端點的呼叫是否成功：<br>**注意：** 您也可以在瀏覽器中輸入下列CRL URL，以檢視是否可以手動下載每個檔案。<ul><li>[https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl](https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl)</li><li>[https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl](http://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl)</li><li>[https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl](http://crl2.adobe.com/Adobe/FlashAccessRootCA.crl)</li><li>[https://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl](http://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl)</li></ul>如果防火牆規則已開啟且目前沒有任何3324錯誤，則可能是暫時性的網路問題。 檢查客戶的伺服器記錄（可能位於/tomcat/logs/目錄中），以判斷授權伺服器嘗試擷取「憑證撤銷清單」時是否發生錯誤。<br>**注意：** 續約CRL檔案時，如果大量使用者端報告3324錯誤至暫時性網路問題，就可能發生錯誤。 網路問題解決後，3324問題也解決了。<br>如果所有4個CRL檔案都存在於tomcat/temp/目錄中，並且使用者端仍然收到3324錯誤，則可能會出現對CRL檔案的檔案存取問題。<br>若要解決此問題，您可能需要檢閱記錄檔並清除現有的CRL檔案。<br>如果沒有伺服器問題，請提示使用者重設，如錯誤碼3322所述。 |
| 3325 | CorruptedServerStateStore | DRM使用者端使用的檔案已被意外修改。 subErrorIdentifis包含使用者端特有的錯誤或行錯誤。<ul><li>散發者的軟體應再次重試操作，因為AdobeCP已在內部刪除違規的伺服器存放區，重試應該會成功。 如果重試失敗，請記錄問題。</li><li>如果重試失敗率高於使用者群硬碟的預期失敗率，請將問題升級至Adobe。</li></ul> |
| 3326 | StoreTamperingDetected | 授權存放區已被竄改或損毀，無法再使用。<br>散發者的軟體應該會以錯誤碼3322中說明的相同方式引導使用者重設。 |
| 3327 | ClockTamperingDetected | 請修正時鐘或再次取得授權/授權/網域授權。 |
| 3328 | ServerErrorTryArgety | 這是伺服器端錯誤，伺服器無法完成來自使用者端的請求。 例如，當伺服器忙碌中、HTTP/500、伺服器沒有解密請求所需的金鑰等時，就會發生此錯誤。<br>在使用者端上，無法判斷哪裡出了問題。 客戶必須檢閱Primetime DRM伺服器記錄（通常稱為AdobeFlashAccess.log），以判斷哪裡出問題。 記錄檔中總是有描述性很強的棧疊追蹤來指示問題。 subErrorId包含伺服器特有的錯誤或行錯誤。<br>散發者應檢視伺服器記錄檔，以識別傳送此錯誤的伺服器。 對於子錯誤碼為101的3328錯誤，伺服器無法解密請求。 客戶必須驗證安裝在授權伺服器上的授權/傳輸伺服器憑證是否相符，並與封裝期間使用的憑證相對應。<br>此外，如果客戶使用參考實作，他們必須確保flashaccessrefimpl.properties檔案中沒有指定主要和其他憑證的拼字。<br> |
| 3329 | ApplicationSpecificError | Primetime DRM不知道應用程式專屬的子錯誤代碼。 subErrorId包含來自發行者自訂授權伺服器的伺服器特定錯誤。 伺服器在應用程式專屬的名稱空間中傳回錯誤。 |
| 3330 | 需要驗證 | 當內容設定為要求使用者端在取得授權前進行驗證時，就會發生此錯誤。<ul><li>散發者的軟體應該驗證使用者，然後再次取得授權。 如果您的服務不打算使用驗證，請記錄造成此錯誤之內容的識別碼。</li><li>除非內容不應設定為需要驗證，否則此錯誤不應要求呈報。 在這種情況下，請使用適當的原則重新封裝違規內容。 如果內容已正確封裝，請參閱診斷原則/授權差異。</li></ul> |
| 3331 | ContentNotYetValid | 取得的授權尚未生效。 若要解決此問題，請檢查使用者端時鐘是否設定不正確。 若要設定使用者端時鐘，請重新封裝內容或修改許可證伺服器設定。 |
| 3332 | CachedLicenseExpired | 再次從伺服器取得授權。 |
| 3333 | PlaybackwindowExpired | 您必須通知使用者，在原則過期前他們無法播放此內容。 |
| 3334 | InvalidDRMPlatform | 此平台不允許播放內容，例如，內容提供者已設定Primetime DRM拒絕內容至平台上的Primetime DRM，或共用網域繫結授權繫結至適用於不同分割區的共用網域權杖。<br>若未使用適當的（閘道式CDM功能）封裝程式認證來封裝內容，CDM可能會擲回此錯誤。 如需詳細資訊，請參閱CDM功能閘道。<br>如果內容封裝有不正確的PHDS/PHLS憑證，內容可能會在Chrome中運作，但不能在其他瀏覽器中運作（反之亦然）。<br>**注意：** 這是因為Chrome使用不同的PHDS/PHLS憑證。<br>若要確認正在使用哪個憑證，請傾印內容中繼資料的詳細資訊並尋找收件者憑證。 |
| 3335 | InvalidDRMVersion | 若要解決此問題，請完成下列其中一項作業：<ul><li>升級AIR</li><li>若為Flash Player，請升級AdobeCP模組並重試播放。</li></ul> |
| 3336 | InvalidRuntimePlatform | 此平台不允許播放內容，因為內容提供者已將Primetime DRM設定為拒絕將內容傳送至平台上的FP/AIR。 |
| 3337 | InvalidRuntimeVersion | 如果內容或伺服器設定為拒絕播放至特定版本的Flash或AIR執行階段，就會發生這種情況。<ul><li>如果使用者在可以升級Flash的作業系統上，散發者的軟體應該提示使用者升級Flash，然後再試一次。 否則，建議使用者使用不同的電腦。</li><li>如果懷疑錯誤3337s，請確定它是否發生在特定內容中，並重新封裝該內容。 如果內容正確封裝，請參閱診斷原則/授權差異。</li></ul> |
| 3338 | UnknownConnectionType | 無法偵測連線型別，原則要求您開啟輸出保護。 僅當封裝的內容需要數位或類比輸出保護時，才會出現此問題。<br>在11.8.800.168版之前的Flash Player版本中，對於原則指出內容保護為USE IF AVAILABLE的內容，偶爾會發生錯誤3338。 此問題已在11.8.800.168版及更新版本中修正。<ul><li>經銷商的軟體會選取不需要輸出保護的內容變體（例如HD資料流的SD變體）。 如果onUSE_IF_AVAILABLE內容發生錯誤3338，請檢查播放器版本號碼。 如果播放器版本低於11.8.800.168，建議使用者升級Flash Player。 如果11.8.800.168以上的版本發生錯誤3338，請記錄導致錯誤的內容。</li><li>散發者應檢查造成此錯誤的內容，並確認內容的原則為類比與數位輸出設定NO_PROTECTION或USE_IF_AVAILABLE。 如果內容意外地以NO_OUTPUT或REQUIRED封裝，請重新封裝內容。 如果內容正確封裝，請參閱診斷原則/授權差異。 否則呈報至Adobe。</li></ul>如需詳細資訊，請參閱 [當您的DRM原則設定為USE_IF_AVAILABLE時，發生未預期的3338錯誤](https://forums.adobe.com/message/5518688)？ |
| 3339 | NoAnalogPlaybackAllowed | 無法在類比裝置上播放。 若要解決此問題，請連線數位裝置。 |
| 3340 | NoAnalogProtectionAvail | 無法播放內容，因為連線的類比外部顯示裝置（顯示器/電視）沒有正確的功能（例如，裝置沒有Macrovision或ACP）。 |
| 3341 | NoDigitalPlaybackAllowed | 無法在數位裝置上播放內容。 |
| 3342 | NoDigitalProtectionAvail | 連線的數位外接顯示裝置（顯示器/電視）功能不正確。 例如，裝置沒有HDCP。 |
| 3343 | 內部錯誤 | 目前已知此錯誤最初會在新版Flash發行後發生。 發生此問題的原因是Flash在Flash開啟時升級，這會使Flash處於不良狀態，直到瀏覽器重新啟動為止。<ul><li>散發者的軟體應完成下列工作：</li><li>建議使用者關閉或結束所有瀏覽器，然後重新開啟。</li><li>檢查Flash的版本是否為最新版本。</li></ul>如果版本不是最新版本，建議客戶升級、關閉其瀏覽器中的所有索引標籤，然後重新開啟。<ul><li>如果瀏覽器成功重新啟動後發生錯誤，請升級至Adobe。 發行新版本時，建議您聯絡Adobe支援，檢視背景更新問題是否已修正。</li></ul> |
| 3344 | MissingAdobeCPModule | 部分Flash或AIR未正確安裝。<br>若要解決此問題，請完成下列其中一項作業：<ul><li>若為AIR，使用者必須解除安裝並重新安裝AIR。</li><li>若要Flash Player，請呼叫System.update。</li></ul> |
| 3346 | 移轉失敗 | 散發者的軟體應執行下列其中一項作業：<ul><li>如果AIR，請呼叫 `DRMManager.resetDRMVouchers()`.</li><li>如果Flash因錯誤3322或3346而無法使用，使用者應前往 [https://forums.adobe.com/message/5535907#5535907](https://forums.adobe.com/message/5535907#5535907) 並遵循Adobe文章的指示，以程式設計方式重設其DRM授權存放區。</li><li>如果此錯誤經常發生，散發者應該提供頻率播放器版本的詳細資訊以及要Adobe的瀏覽器版本。</li></ul>如需詳細資訊，請參閱下列論壇文章：<ul><li>[Chrome中的DRM錯誤3322/3346/3368 （資訊列問題）](https://forums.adobe.com/message/5520902)</li><li>[硬體變更後出現3322或3346錯誤](https://forums.adobe.com/message/5535911)</li></ul> |
| 3347 | Devicecapabilities不足 | 此錯誤的主要含義是授權具有限制，使用者端的DRM憑證指出它無法滿足。 發行使用者端DRM憑證時，會定義下列「硬體功能」：<ul><li>**非使用者可存取的匯流排。** 若 **true**，解密的媒體絕不會流經匯流排或流入應用程式可存取它的主記憶體。 若 **false**，應用程式在解密後可存取內容。</li><li>**信任的硬體根目錄。** 若 **true**，所有在開機時載入到裝置上的軟體，都會根據硬體提供的金鑰或摘要進行驗證。 當使用者端的DRM憑證開啟許可證時，使用者端會檢查這兩個限制，並且會立即失敗。 在發行授權之前，也可以在伺服器端檢查這些限制。</li></ul>此錯誤的次要含義是授權已設定「Jailbreak Enforcement」原則，且在裝置上偵測到越獄。 這項檢查定期在使用者端完成，無法在伺服器端進行檢查。<br>經銷商可以更新原則並移除限制。 針對裝置功能原則，發出原則更新命令，其中包含 — devCapabilitiesV1flag且無引數。 對於越獄執行setpolicy.enforceJailbreak=false。 |
| 3348 | HardStopIntervalExpired | 硬停止間隔已過期。 |
| 3349 | ServerVersionToHigh | 伺服器的執行版本高於使用者端支援的最高版本。 |
| 3350 | ServerVersionTooLow | 伺服器的執行版本低於使用者端支援的最低版本。 |
| 3351 | DomainTokenInvalid | 網域權杖無效。 若要解決此問題，請再次向網域註冊。 |
| 3352 | DomainTokenTooOld | 網域權杖早於授權所需的權杖。 若要解決此問題，請再次向網域註冊。 |
| 3353 | DomainTokenToNew | 網域權杖比授權所需的權杖新。 |
| 3354 | DomainTokenExpired | 網域權杖已過期。 |
| 3355 | DomainJoinFailed | 網域加入失敗。 |
| 3356 | NoActivatedRoot | 找不到V3分葉授權的根授權。 |
| 3357 | NoValidEmbeddedLicense | 找不到有效的內嵌授權。 |
| 3358 | NoACProtectionAvailable | 無法播放，因為連線的類比裝置沒有ACP保護。 |
| 3359 | NoCGSMAProtectionAvailable | 無法播放，因為連線的類比裝置沒有CGMSA保護。 |
| 3360 | DomainRegistrationRequired | 內容需要網域註冊。 |
| 3361 | NotRegisteredToDomain | 電腦未註冊到指定中繼資料的網域。 |
| 3362 | OperationTimeoutError | 非同步作業所花的時間超過設定的maxOperationTimeout。<br>**注意：** 此錯誤碼僅由iOS DRMNative Framework傳回。 |
| 3363 | UnsupportedIOSPlaylistError | M3U8播放清單包含不支援的內容，或遺失必要的#EXT-X-FAXS-CM DRM中繼資料物件。<br>**注意：** 此錯誤碼僅由iOS DRMNative Framework傳回。 |
| 3364 | NoDeviceId | 框架已要求裝置ID，但傳回的值是空的。<br>框架已要求裝置ID，但傳回的值是空的。<br>在Chrome瀏覽器設定中，使用者不應選取 **允許受保護內容的識別碼** 核取方塊。 |
| 3365 | IncognitoModeNotAllowed | 此瀏覽器/平台組合不允許無痕模式下受DRM保護的播放。<br>散發者的軟體應建議使用者結束無痕模式或使用不同的瀏覽器。 如需詳細資訊，請參閱 [DRM錯誤3365原因和解決方法](https://forums.adobe.com/thread/1266622). |
| 3366 | Badparameter | 主機執行階段使用錯誤的引數呼叫Primetime DRM程式庫。 |
| 3367 | BadSignature | M3U8資訊清單簽署失敗。<br>**注意：** 此錯誤碼只會由iOS DRMNative Framework或AVE傳回。 |
| 3368 | UserSettingsNoAccess | 使用者已取消操作，或已輸入不允許存取系統的設定。<br>此錯誤只會在SWF版本19或更新版本中擲回。 為了回溯相容性，系統會針對SWF版本18或更早版本擲回錯誤代碼3321。<br>分銷商的軟體應引導使用者說明如何允許無沙箱外掛程式存取。 如需詳細資訊，請參閱 [Chrome中的DRM錯誤3322/3346/3368 （資訊列問題）](https://forums.adobe.com/message/5520902). |
| 3369 | InterfaceNotAvailable | 無法使用必要的瀏覽器介面。 此問題僅發生在Pepper上。 Flash外掛程式和瀏覽器版本之間可能會不相符。<br>散發者的軟體應引導使用者確保他們已安裝最新版本的瀏覽器。<br>如果此錯誤的發生次數增加，且對應於已發佈的瀏覽器更新，請升級至Adobe。 |
| 3370 | ContentIdSettingsNoAccess | 使用者已停用 **允許受保護內容設定的識別碼。**<br>**注意：** 此錯誤出現在Pepper 13.0.0.x版或更新版本中。<br>經銷商的軟體和/或操作團隊應引導使用者啟用 **允許受保護內容的識別碼** 設定。<br>如需詳細資訊，請參閱 [https://forums.adobe.com/message/6518323#6518323](https://forums.adobe.com/message/6518323#6518323). |
| 3371 | NoOPConstraintInPixelConstraints | 根據授權中的輸出保護限制，解析格式錯誤。<br>散發者的軟體應顯示錯誤訊息。 要求使用者以內容標題將問題報告給經銷商。<br>散發者應使用有效原則重新封裝內容。 |
| 3372 | ResolutionLargerThanMaxResolution | 內容的解析度大於輸出保護限制中指定的最大解析度。<br>如果散發者的作業團隊在記錄中看到此錯誤，他們應該檢閱以解析度為基礎的輸出保護原則，並在必要時重新封裝內容。<br>如需以解析度為基礎的輸出保護的詳細資訊，請參閱關於以解析度為基礎的輸出保護。 |
| 3373 | DisplayResolutionLargerThanConstrain | 內容的解析度大於目前作用中的輸出保護限制所指定的解析度。<br>如果散發者的作業團隊在記錄中看到此錯誤，他們應該檢閱以解析度為基礎的輸出保護原則，並在必要時重新封裝內容。<br>如需以解析度為基礎的輸出保護的詳細資訊，請參閱關於以解析度為基礎的輸出保護。 |
| 3374 | ClientCommProcessFailed | 在使用者端通訊處理期間失敗，例如，要求產生、回應處理、錯誤的驗證權杖等。 |

## 3328的子錯誤碼對應 {#suberror-code-mapping-for-3328}

| SubError | 說明 |
|---|---|
| 100-1000 | 由Adobe授權伺服器保留 |
| 10000 - 20000 | 由Adobe的個人化伺服器保留 |
| 20100-21000 | 保留給AdobeXbox金鑰伺服器。<br>此範圍內的錯誤對應至一般Primetime DRM伺服器SDK錯誤訊息參考，如下所示：<br>Xbox keyserver錯誤= DRM伺服器錯誤+ 0x20000<br>例如，Xbox Keyserver Error 20202等同於DRM Server SDK Error 202 |
| 100xxxx | 保留給使用者端子錯誤碼 |
