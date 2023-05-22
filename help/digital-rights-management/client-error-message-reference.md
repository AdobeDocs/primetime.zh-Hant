---
description: DRM客戶端錯誤是TVSDK客戶端錯誤的子集。
title: DRM客戶端錯誤消息參考
exl-id: 3d74cb92-c0a7-4eab-91b8-7e60a9c33df4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '5185'
ht-degree: 1%

---

# DRM客戶端錯誤消息參考 {#client-error-message-reference}

DRM客戶端錯誤是TVSDK客戶端錯誤的子集，與DRM相關的錯誤代碼範圍從3300到3399。

## DRM客戶端錯誤 {#drm-client-errors}

| 錯誤代碼 | 助記法 | 補救 |
|---|---|---|
| 3300 | 憑證無效 | 分銷商的軟體應該做什麼： <ul><li> 如果您使用的是GoogleChrome，並且您處於Incognito模式，且Flash Player版本低於11.6，則可能會發生此錯誤。 我們建議播放器檢查瀏覽器的版本號，並建議用戶退出Incognito模式。</li><li> 再次請求許可證。 如果請求成功，則無需記錄或升級。 如果請求不成功，請記錄導致錯誤的內容。 `subErrorId` 包含行錯誤（如果存在）。</li></ul> 分銷商應該做的： <ul><li> 如果對Flash低於11.6版的Chrome以外的配置重試失敗，則打包中可能出現故障。</li><li>檢查問題是否特定於某些內容並重新打包。</li></ul> |
| 3301 | 身份驗證失敗 | 伺服器無法驗證或授權客戶端。<ul><li>分銷商的軟體應採取任何必要的操作來重新建立用戶的憑據，或指導用戶獲取對內容的訪問。</li><li>分發伺服器應確認其授權和身份驗證機制正常工作。 如果分銷商不計畫使用身份驗證或授權功能，他們應檢查違規內容的策略是否需要身份驗證，並參閱診斷策略/許可證差異。</li></ul> 有關此錯誤代碼的詳細資訊，請參見 [DRM錯誤3301的原因和解決方法](https://forums.adobe.com/thread/1277149)。 |
| 3302 | 需要SSL | 對於黃金時段DRM 4.0及更高版本，當遠程密鑰URL不使用HTTPS作為方案時，在iOS引發此錯誤。 需要HTTPS。 <ul><li>如果分發伺服器使用的版本早於黃金時段DRM版本4，或至少是版本4，但平台不是iOS，則分發伺服器的軟體應記錄該錯誤。 此錯誤僅在iOS引發。</li><li>如果分銷商的軟體至少是黃金時段DRM版本4，而平台是iOS，則分銷商必須將他們使用的遠程密鑰伺服器URL更改為HTTPS。 如果它們只使用HTTP，則分發伺服器可能必須設定HTTPS伺服器。 否則，分銷商需要將記錄的資訊提交到Adobe並上報問題。</li></ul> |
| 3303 | 內容已過期 | 您正在查看的內容已根據內容提供程式設定的規則過期。  `subErrorId` 包含特定於客戶端的錯誤或行錯誤。 <ul><li>分發伺服器的軟體應嘗試從伺服器重新獲取一次許可證，以確定是否有新的未過期許可證可用。 如果沒有可用的許可證或許可證已過期，允許用戶獲取新的許可證，或通知用戶無法監視內容。</li></ul> 如果內容已與具有失效過期/終止日期的策略打包，並且許可證伺服器日誌報告PolicyEvaluationException，則聲明策略結束日期已失效（伺服器錯誤代碼303）。 檢查伺服器的日誌檔案以驗證。<br>如果可能，客戶應檢查他們在打包期間使用的策略，以查看該策略是否已過期。 Java命令行工具是： <ul><li>java -jar libs/AdobePolicyManager.jar</li><li> 詳細演示.pol</li><li>分發伺服器應確認許可證到期日期是否按預期配置。</li></ul> 有關此錯誤代碼的詳細資訊，請參見 [AMS/FMS使用即時流時3303（內容已過期）?](https://forums.adobe.com/thread/1300813) |
| 3304 | 授權失敗 | 當前用戶無權查看內容。 以其他用戶身份登錄。<br>有關此錯誤代碼的詳細資訊，請參閱錯誤代碼3301。 |
| 3305 | ServerConnection失敗 | 由於網路延遲或客戶端離線，與許可證或域伺服器的連接超時。 通常，subErrorId包含HTTP返回代碼。<ul><li>分發伺服器的軟體應嘗試連接到已知良好的伺服器。 如果嘗試失敗，則提示用戶重新連接到網路。 如果嘗試成功，請記錄。</li><li>分發伺服器應驗證正在使用的任何許可證和域伺服器是否聯機且可從客戶端網路中看到。</li></ul>有關此錯誤代碼的詳細資訊，請參見 [DRM 3305 ServerConnectionFailed原因和解決方法](https://forums.adobe.com/thread/1284947.) |
| 3306 | ClientUpdateRequired | 當前客戶端無法完成請求的操作，但更新的客戶端可能能夠完成請求。<br>這可能有幾個原因：<ul><li>使用的共用域在此客戶端上不可用。 在Chrome上播放時可能會出現這種情況，但不會出現其他瀏覽器，反之亦然。<br>**注：** Chrome使用的PHDS/PHLS密鑰與其他瀏覽器使用的密鑰不同。</li><li>當在5.0之前的iOS版本上運行時，應用程式正嘗試添加多個DRMSassion。</li><li>只支援版本2時，元資料的版本為3或更高。</li><li>分發伺服器的軟體應提醒用戶並中止操作。 如果軟體有確定升級是否可用的方法，請以適當的方式引導用戶進行升級。</li><li>如果由於共用域而出現此問題，則分發伺服器需要使用Adobe檢查更新的運行時或庫。 在Flash運行時，分發伺服器可以直接在其應用程式中強制升級。 對於庫，分發伺服器需要獲取更新的庫，重建其應用程式並將其部署到其用戶。</li></ul>如果由於多個DRMSassion而出現問題，則分銷商需要更新其應用程式以在添加多個DRMSassion之前檢查iOS版本號。 或者，他們可以限制將他們的申請分發到iOS第5版及更高版本。<br>如果由於元資料版本高於版本2而出現問題，則問題可能是元資料損壞。 他們可以嘗試重建元資料並查看結果。 如果他們繼續看到問題，請記錄問題並升級為Adobe。<br>有關此錯誤代碼的詳細資訊，請參見 [如何修復3306 DRMErrorEvent錯誤代碼](https://forums.adobe.com/thread/1266675)。 |
| 3307 | 內部故障 | 這通常表示黃金時段DRM代碼中的錯誤，並且是意外的，除非存在已知的錯誤，如下所示。subErrorId包含特定於客戶端的錯誤或行錯誤。<ul><li>如果瀏覽器是Windows上的Chrome，而Flash版本是11.6(SWF版本19或更高版本)，則分銷商的軟體應假定用戶在資訊欄上按了「拒絕」，並將其與3368一樣處理。</li><li>如果3307在瀏覽器不是Chrome或Flash版本不是11.6時發生，則分銷商應升級為Adobe。</li></ul>**注：** 3307:1107296344(FailedToGetBrokerHandle)可能發生在Chrome瀏覽器版本24-28上。 |
| 3308 | WrongLicenseKey | 當使用的許可證包含解密內容的錯誤密鑰時，會引發此錯誤。 subErrorId包含客戶端特定的錯誤或行錯誤。<br>產生此錯誤的方法似乎只有兩種：<ul><li>客戶修改了用於生成許可證的標準Adobe工具（例如許可證伺服器Java框架）。 在這種情況下，許可證包含的密鑰可能與任何內容不對應。</li><li>客戶已使用相同的許可證ID頒發多個許可證。 在這種情況下，客戶端上有多個可用的許可證，這些許可證與內容元資料相匹配，而黃金時段DRM代碼已選擇了錯誤的許可證供使用。</li><li>分發伺服器的軟體應嘗試從伺服器重新獲取許可證。</li><li>如果沒有可用的許可證或許可證已過期，請為用戶提供一個工作流以獲取新的許可證，或通知用戶無法監視內容，然後記錄問題。</li><li> 如果這是域綁定內容(對於AIR)，請為用戶提供加入域的方法。</li><li>分發商應：</li><li> 驗證他們是否尚未自定義Mighine DRM許可證伺服器的許可證頒發部分。</li><li>驗證他們是否為所有許可證頒發唯一的許可證ID。</li><li>將問題升級為Adobe。</li></ul> |
| 3309 | 損壞的附加頭 | 如果報頭大於65536位元組，則會發生這種情況。<ul><li>分發商的軟體應記錄導致錯誤的內容。</li><li>分發商應確認該錯誤可通過特定內容再現。 重新打包損壞的內容。</li></ul> |
| 3310 | AppIDMismatch | 不允許列出應用程式。 安卓、iOS或FlashSWF。<br>subErrorId:1000942;播放受保護的流時出錯。 FAXS錯誤。<br>也可能是客戶端報告pubID（應用發佈者ID）的空字串。<br>**Android:** Android應用程式與正在使用的應用程式不匹配。 請記住，Android中調試密鑰庫的目錄通常與發行版密鑰庫的目錄不同。<br>**iOS:** 查看 [允許列出您的iOS應用程式](/help/programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) TVSDKiOS指南中的文檔。 |
| 3312 | 許可證完整性 | 再次從伺服器下載許可證。 |
| 3313 | WriteMicrosafe失敗 | 當系統無法寫入檔案系統時，會出現此問題。 subErrorId包含客戶端特定的錯誤或行錯誤。<br>在MicrosoftWindows上，當加密內容的licenseID或policyID太長時，Active X或NPAPI插件快閃記憶體播放器可能會拋出錯誤3313。 這是因為Windows中的最大路徑長度。 （Pepper插件沒有此問題。）<ul><li>分發伺服器的軟體應提示用戶確認其用戶目錄未鎖定，或者卷已滿或已鎖定。</li><li>如果分銷商使用的是AIR，而不是Flash，則問題可能由路徑長度限制引起。 分銷商應將其AIR申請的名稱縮短到合理的程度。</li></ul> |
| 3314 | 損壞的DRMMetadata | 此錯誤通常表示內容已與testPKI證書打包，而播放器是使用生產PKI構建的，反之亦然。<br>subErrorId包含客戶端特定的錯誤或行錯誤。<ul><li>分發商的軟體應記錄導致錯誤的內容。</li><li>分發者應確認該錯誤可通過特定內容再現。</li></ul>您可能必須重新打包損壞的內容。 |
| 3315 | 拒絕權限 | 當打算使用3305時，可能會引發此錯誤代碼的已知錯誤。 有關詳細資訊，請參閱錯誤代碼3305。<br>AIR載入的遠程SWF不允許訪問黃金時段DRM功能。 如果在網路訪問期間出現安全錯誤，也可以拋出此錯誤代碼。 例如，目標伺服器不能通過使用crossdomain.xml連接客戶端，或者無法訪問crossdomain.xml。<br>有關詳細資訊，請參見 [DRM錯誤3315可能的根本原因和解決方法](https://forums.adobe.com/thread/1266592)。 |
| 3317 | AAXS_LoadAdobeCPF失敗 | **重要提示：** 這是一個罕見的錯誤，通常不會在生產環境中出現。<br>如果確實發生錯誤，可以執行下列操作之一：<ul><li>如果使用AIR，請重新安裝AIR。</li><li>如果使用Flash Player，請再次下載AdobeCP模組。</li></ul> |
| 3318 | 不相容AdobeCPVersion | **重要提示：** 這是一個罕見的錯誤，通常不會在生產環境中出現。<br>如果確實發生錯誤，可以執行下列操作之一：<ul><li>如果使用AIR，請重新安裝AIR。</li><li>如果使用Flash Player，請再次下載AdobeCP模組。</li></ul> |
| 3319 | 缺少AdobeCPGetAPI | **重要提示：** 這是一個罕見的錯誤，通常不會在生產環境中出現。<br>如果確實發生錯誤，可以執行下列操作之一：<ul><li>如果使用AIR，請重新安裝AIR。</li><li>如果使用Flash Player，請再次下載AdobeCP模組。</li></ul> |
| 3320 | 主機失敗 | **重要提示：** 這是一個罕見的錯誤，通常不會在生產環境中出現。<br>如果確實發生錯誤，可以執行下列操作之一：<ul><li>如果使用AIR，請重新安裝AIR。</li><li>再次下載AdobeCP和FlashPlayer，因為任何一個解決方案都可能不同步。</li></ul>應用程式只需更新Flash Player，這將導致AdobeCP再次下載。 |
| 3321 | I15nFailed | 使用密鑰設定客戶端的過程失敗。 subErrorId包含特定於客戶端、特定於伺服器或行的錯誤。<ul><li>分發伺服器的軟體應至少重試一次該操作。</li></ul>如果您在Windows上使用GoogleChrome，請說明如何允許不在沙箱中的插件訪問。 有關詳細資訊，請參閱GoogleChrome的「無沙箱」訪問被拒絕。<ul><li>分發伺服器應完成以下任務之一：</li><li>如果錯誤跨平台一致，應使用Adobe來解決問題。</li><li>如果錯誤僅限於Windows上的Chrome，請引導用戶允許無沙盒插件訪問。</li></ul>分銷商應將其SWF更新為19版或更高版本。 對於Chrome特定的3321錯誤，將引發3368錯誤。 錯誤3368可以由分銷商的軟體更具體地處理。 此更改是在Chrome Stable通道26.0.1410.43版中引入的。<br>**注：** 錯誤3321:1090519056可能發生在Flash播放器版本11.1到11.6之間。我們建議您升級到最新的Flash Player版。<br>有關詳細資訊，請參見 [DRM錯誤3321原因和解決方法](https://forums.adobe.com/thread/1277138)。 |
| 3322 | 設備綁定失敗 | 設備似乎與初始化時存在的配置不匹配。 subErrorId包含客戶端特定或行錯誤。<br>分銷商的軟體應完成以下任務之一：<ul><li>如果設備不使用Flash Player，而是AIR,iOS等， `callDRMManager.resetDRMVouchers()`。</li></ul>如果在開發階段的iOS出現此問題，請讓開發人員確認在從第三方預發行分發系統（例如，HockeyApp）下載的生成和從Xcode下載的本地生成之間切換時是否觀察到此問題。 在從HockeApp分發的生成和從Xcode分發的生成之間切換時，不會完全覆蓋以前安裝的屬性。 此情況可能觸發3322錯誤。<br>要解決此問題，開發人員應在安裝新生成之前從設備中刪除舊生成。<ul><li>如果設備正在使用Flash Player，並且無法從3322或3346錯誤代碼中複製，請參閱Adobe中有關如何以寫程式方式在上重置DRM許可證儲存的說明 [Chrome中的DRM錯3322/3346/3368（資訊欄問題）](https://forums.adobe.com/message/5535907#5535907)。</li></ul>此錯誤不應頻繁發生。 在使用漫遊配置檔案的企業環境中，如果用戶正在查看受DRM保護的內容，則當用戶從不同機器登錄時發生的概率錯誤3322增加。 如果可能，分發伺服器應嘗試從用戶獲取此資訊。<br>如果錯誤頻發，請升級為Adobe。 您必須通知Adobe重置許可證儲存是否解決了問題，並告知Adobe在哪些瀏覽器上發生錯誤。<br>有關詳細資訊，請參閱以下文章：<ul><li>https://forums.adobe.com/message/5520902</li><li>https://forums.adobe.com/message/5535911</li><li>https://forums.adobe.com/message/5748618</li><li>https://forums.adobe.com/message/6061165</li></ul> |
| 3323 | CorruptGlobalStateStore | DRM客戶端使用的檔案已意外修改。 subErrorId包含客戶端特定或行錯誤。<ul><li>分銷商軟體應指導用戶以與錯誤代碼3322相同的方式重置。</li><li>如果GlobalStore的故障率高於用戶群硬碟的預期故障率，請將問題上報到Adobe。</li></ul> |
| 3324 | MachineTokenInvalid | 許可證伺服器可能無法連接到證書吊銷清單(CRL)伺服器以刷新其CRL檔案，或者客戶端電腦正在請求已被許可證伺服器吊銷的許可證/身份驗證。<br>在伺服器日誌中，錯誤代碼111 isMachineTokenInvalid。 但是，在客戶端級別，錯誤代碼111被轉換為錯誤代碼3324。<br>DRM許可證伺服器管理員應檢查客戶的許可證伺服器是否能夠檢索AdobeCRL檔案。 如果客戶使用Tomcat，則客戶可以檢查tomcat/temp/目錄以查看是否有4個.CRL檔案。<ul><li>如果檔案在此目錄中，請按兩下Windows資源管理器和CRL查看器應用程式中的檔案，確定是否有任何檔案已過期。</li><li>如果tomcat/temp/中沒有檔案，則可以假定此許可證伺服器由於防火牆或路由問題從未能到達AdobeCRL伺服器。</li></ul>有關詳細資訊，請參閱防火牆規則。<br>如果CRL檔案不可用或已過期，則必須確認是否可以訪問許可證伺服器。 在客戶的許可證伺服器上開啟網路嗅探器（例如，Charles或Wireshark），重新啟動伺服器，並讓客戶端嘗試從伺服器請求許可證。<br>可以觀察網路通信量，以查看對以下URL端點的調用是否成功：<br>**注：** 您還可以在瀏覽器中輸入以下CRL URL，以查看是否可以手動下載每個檔案。<ul><li>[https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl](https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl)</li><li>[https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl](http://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl)</li><li>[https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl](http://crl2.adobe.com/Adobe/FlashAccessRootCA.crl)</li><li>[https://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl](http://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl)</li></ul>如果防火牆規則已開啟且當前沒有3324個錯誤，則可能存在臨時網路問題。 檢查客戶的伺服器日誌（可能位於/tomcat/logs/目錄中），以確定當許可證伺服器嘗試獲取證書吊銷清單時是否出現錯誤。<br>**注：** 在更新CRL檔案時，當大量客戶端（或拆分）將3324錯誤報告到臨時網路問題時，可能會發生錯誤。 網路問題解決後，3324個問題也解決了。<br>如果tomcat/temp/目錄中存在所有4個CRL檔案，並且客戶端仍然收到3324個錯誤，則CRL檔案可能存在檔案訪問問題。<br>要解決此問題，您可能需要查看日誌並清除現有CRL檔案。<br>如果沒有伺服器問題，請提示用戶按錯誤代碼3322中所述重置。 |
| 3325 | 損壞的ServerStateStore | DRM客戶端使用的檔案已意外修改。 subErrorId包含客戶端特定或行錯誤。<ul><li>分發伺服器的軟體應再次重試該操作，因為AdobeCP已在內部刪除了違規伺服器儲存，重試應成功。 如果重試失敗，請記錄問題。</li><li>如果重試失敗的速率大於用戶群硬碟的預期失敗速率，請將問題升級為Adobe。</li></ul> |
| 3326 | 檢測到StorePampertingDetected | 許可證儲存已被篡改或損壞，無法再使用。<br>分發伺服器軟體應指導用戶以與錯誤代碼3322中所述相同的方式重置。 |
| 3327 | 檢測到ClockPampertingDetected | 修復時鐘或再次獲取Authn/Lic/Domain許可證。 |
| 3328 | 伺服器錯誤重試 | 這是伺服器端錯誤，伺服器無法從客戶端完成請求。 例如，當伺服器忙、HTTP/500、伺服器沒有解密請求所需的密鑰等時，可能會發生此錯誤。<br>在客戶身上，無法確定出了什麼問題。 客戶必須查看黃金時段DRM伺服器日誌（通常稱為AdobeFlashAccess.log），以確定出錯的原因。 日誌中始終存在描述性很強的堆棧跟蹤，以指示問題。 subErrorId包含伺服器特定的或行錯誤。<br>分發伺服器應查看伺服器日誌以確定哪個伺服器正在發送此錯誤。 對於子錯誤代碼為101的3328錯誤，伺服器無法解密該請求。 客戶必須驗證安裝在許可證伺服器上的許可證/傳輸伺服器證書是否匹配並與打包期間使用的證書對應。<br>此外，如果客戶正在使用「參考實施」，則他們必須確保在指定主證書和附加證書的flashaccessrefimpl.properties檔案中沒有拼寫錯誤。<br> |
| 3329 | ApplicationSpecificError | Mighine DRM不知道特定於應用程式的子錯誤代碼。 subErrorId包含發佈者自定義許可證伺服器中的伺服器特定錯誤。 伺服器在特定於應用程式的命名空間中返回錯誤。 |
| 3330 | 需要身份驗證 | 當內容配置為要求客戶端在獲取許可證之前進行身份驗證時，會出現此錯誤。<ul><li>分銷商的軟體應驗證用戶，然後再次獲取許可證。 如果您的服務不打算使用身份驗證，請記錄導致此錯誤的內容的標識。</li><li>此錯誤不應要求升級，除非不應將內容配置為需要身份驗證。 在這種情況下，使用適當的策略重新打包違規內容。 如果內容打包正確，請參閱診斷策略/許可證差異。</li></ul> |
| 3331 | ContentNotYetValid | 獲取的許可證尚未生效。 要解決此問題，請檢查客戶端時鐘是否設定不正確。 要設定客戶端時鐘，請重新打包內容或修改許可證伺服器配置。 |
| 3332 | CachedLicenseExpired | 再次從伺服器獲取許可證。 |
| 3333 | 播放窗口已過期 | 您必須通知用戶在策略過期之前無法播放此內容。 |
| 3334 | DRMPlatform無效 | 不允許該平台回放內容，因為例如，內容提供商已將Mighile DRM配置為拒絕在平台上的Mighile DRM的內容或共用域綁定許可證綁定到用於不同分區的共用域令牌。<br>如果內容未通過使用適當（CDM功能選通）打包器證書打包，CDM可能會引發此錯誤。 有關詳細資訊，請參閱CDM功能選中。<br>如果內容與不正確的PHDS/PHLS證書打包，則內容可能在Chrome中工作，但不能在其他瀏覽器中工作（反之亦然）。<br>**注：** 這是因為Chrome使用不同的PHDS/PHLS證書。<br>要確認正在使用哪個證書，請轉儲內容元資料的詳細資訊並查找收件人證書。 |
| 3335 | DRMVersion無效 | 要解決此問題，請完成以下任務之一：<ul><li>升級AIR</li><li>對於Flash Player，請升級AdobeCP模組並重試播放。</li></ul> |
| 3336 | InvalidRuntimePlatform | 不允許此平台回放內容，因為例如，內容提供商已將Mighile DRM配置為拒絕在平台上將內容發給FP/AIR。 |
| 3337 | InvalidRuntimeVersion | 如果內容或伺服器配置為拒絕播放特定版本的Flash或AIR運行時，則會發生這種情況。<ul><li>如果用戶在可升級Flash的作業系統上，分發伺服器的軟體應提示用戶升級Flash，然後重試。 否則建議用戶使用其他電腦。</li><li>如果懷疑出現錯誤3337s，請確定是否針對特定內容發生錯誤並重新打包該內容。 如果內容打包正確，請參閱診斷策略/許可證差異。</li></ul> |
| 3338 | 未知連接類型 | 無法檢測連接類型，並且策略要求您開啟「輸出保護」。 只有在內容打包以需要數字或模擬輸出保護時，才會出現此問題。<br>11.8.800.168版以前的Flash Player版本中出現問題，導致錯誤338偶爾出現在策略指示內容保護為USE IF AVAILABLE的內容上。 此問題已在11.8.800.168版和更高版本中解決。<ul><li>分銷商的軟體選擇不需要輸出保護的內容的變體（例如HD流的SD變體）。 如果錯誤3338發生在USE_IF_AVAILABLE內容上，請檢查播放器版本號。 如果播放器版本小於11.8.800.168，建議用戶升級Flash Player。 如果11.8.800.168以上版本發生錯誤338，請記錄導致錯誤的內容。</li><li>分發伺服器應檢查哪些內容導致此錯誤，並驗證內容的策略是否為模擬和數字輸出設定了NO_PROTECTION或USE_IF_AVAILABLE。 如果內容無意中使用NO_OUTPUT或REQUIRED打包，請重新打包內容。 如果內容打包正確，請參閱診斷策略/許可證差異。 否則，請升級為Adobe。</li></ul>有關詳細資訊，請參見 [將DRM策略設定為USE_IF_AVAILABLE時，將獲取意外的3338錯誤](https://forums.adobe.com/message/5518688)? |
| 3339 | NoAnalogPlaybackAllowed | 無法在模擬設備上回放。 要解決此問題，請連接數字設備。 |
| 3340 | 無模擬保護可用 | 無法回放內容，因為連接的模擬外部顯示設備（監視器/電視）沒有正確的功能（例如，設備沒有Macrovision或ACP）。 |
| 3341 | NoDigitalPlaybackAllowed | 無法在數字設備上回放內容。 |
| 3342 | NoDigitalProtectionAvail | 連接的數字外部顯示設備（顯示器/電視）沒有正確的功能。 例如，設備沒有HDCP。 |
| 3343 | 內部錯誤 | 當前已知在發佈新版本的Flash後，此錯誤最初會發生。 出現此情況是因為Flash在Flash開啟時升級，這會使Flash處於一個錯誤狀態，直到瀏覽器重新啟動。<ul><li>分銷商的軟體應完成以下任務：</li><li>建議用戶關閉或退出所有瀏覽器，然後重新開啟。</li><li>檢查Flash的版本是否為當前版本。</li></ul>如果版本不是最新版本，建議客戶升級，關閉其瀏覽器中的所有頁籤，然後重新開啟。<ul><li>如果瀏覽器成功重新啟動後出現錯誤，請升級到Adobe。 發佈新版本時，我們建議您與Adobe支援部門聯繫，以查看後台更新問題是否已解決。</li></ul> |
| 3344 | 缺少AdobeCPModule | 部分Flash或AIR未正確安裝。<br>要解決此問題，請完成以下任務之一：<ul><li>對於AIR，用戶必須重新卸載並安裝AIR。</li><li>對於Flash Player，請調用System.update。</li></ul> |
| 3346 | 遷移失敗 | 分銷商的軟體應執行以下操作之一：<ul><li>如果AIR，打電話 `DRMManager.resetDRMVouchers()`。</li><li>如果Flash因錯誤3322或3346而不可用，則用戶應轉到 [https://forums.adobe.com/message/5535907#5535907](https://forums.adobe.com/message/5535907#5535907) 並按照Adobe文章的說明以寫程式方式重置其DRM許可證儲存。</li><li>如果此錯誤經常發生，分發伺服器應提供有關頻率播放器版本和要Adobe的瀏覽器版本的詳細資訊。</li></ul>有關詳細資訊，請參閱以下論壇文章：<ul><li>[Chrome中的DRM錯3322/3346/3368（資訊欄問題）](https://forums.adobe.com/message/5520902)</li><li>[硬體更改後出現3322或3346錯誤](https://forums.adobe.com/message/5535911)</li></ul> |
| 3347 | DeviceCapabilities不足 | 此錯誤的主要含義是許可證具有客戶端的DRM證書表示它不能滿足的約束。 下列「硬體功能」是在發出客戶端DRM證書時定義的：<ul><li>**非用戶可訪問的匯流排。** 如果 **真**，解密的媒體從不流經匯流排或進入主儲存器，應用程式可以在主儲存器中訪問它。 如果 **假**，解密後，應用程式可以訪問內容。</li><li>**硬體信任根。** 如果 **真**，啟動時在設備上載入的所有軟體都通過僅在硬體中可用的密鑰或摘要進行驗證。 當針對客戶機的DRM證書開啟許可證時，在客戶端上檢查這兩個約束，並且立即失敗。 在發放許可證之前，還可以在伺服器端檢查這些約束。</li></ul>此錯誤的次要含義是許可證已設定「Jailbreak Enforcement」策略，並且在設備上檢測到了越獄。 此檢查在客戶端定期完成，在伺服器端無法檢查。<br>分銷商可以更新策略並取消限制。 對於設備功能策略，使用 — devCapabilitiesV1flag和no參數發出策略更新命令。 用於jaylbreak強制setpolicy.enforceJailbreak=false。 |
| 3348 | HardStopIntervalExpired | 硬停止間隔已過期。 |
| 3349 | ServerVersionTooHigh | 伺服器運行的版本高於客戶端支援的最高版本。 |
| 3350 | 伺服器版本太低 | 伺服器運行的版本低於客戶端支援的最低版本。 |
| 3351 | DomainToken無效 | 域令牌無效。 要解決此問題，請再次向域註冊。 |
| 3352 | 域令牌太舊 | 域令牌早於許可證所需的令牌。 要解決此問題，請再次向域註冊。 |
| 3353 | 域令牌太新 | 域令牌比許可證所需的令牌新。 |
| 3354 | 域令牌已過期 | 域令牌已過期。 |
| 3355 | 域加入失敗 | 域加入失敗。 |
| 3356 | 無對應根 | 找不到V3葉許可證的根許可證。 |
| 3357 | NoValidEmbeddedLicense | 找不到有效的嵌入式許可證。 |
| 3358 | 無可用的ACPProtection | 無法回放，因為連接的模擬設備沒有ACP保護。 |
| 3359 | 無CGSMAProtectionAvailable | 無法回放，因為連接的模擬設備沒有CGMSA保護。 |
| 3360 | 需要域註冊 | 內容需要域註冊。 |
| 3361 | 未註冊到域 | 電腦未註冊到指定元資料的域。 |
| 3362 | OperationTimeoutError | 非同步操作所花費的時間比配置的maxOperationTimeout要長。<br>**注：** 此錯誤代碼僅由iOSDRMNative Framework返回。 |
| 3363 | 不支援的IOSPlaylistError | M3U8播放清單包含不受支援的內容，或缺少所需的#EXT-X-FAXS-CM DRM元資料對象。<br>**注：** 此錯誤代碼僅由iOSDRMNative Framework返回。 |
| 3364 | 無設備ID | 框架請求了設備ID，但返回的值為空。<br>框架請求了設備ID，但返回的值為空。<br>在Chrome瀏覽器設定中，用戶不應選擇 **允許受保護內容的標識符** 的子菜單。 |
| 3365 | IncognitoModeNotAllowed | 此瀏覽器/平台組合不允許在Incognito模式下播放受DRM保護的內容。<br>分發伺服器的軟體應建議用戶退出Incognito模式或使用其他瀏覽器。 有關詳細資訊，請參見 [DRM錯誤3365原因和解決方法](https://forums.adobe.com/thread/1266622)。 |
| 3366 | 錯誤參數 | 主機運行時使用錯誤的參數調用了Mighine DRM庫。 |
| 3367 | 錯誤簽名 | M3U8清單簽名失敗。<br>**注：** 此錯誤代碼僅由iOSDRMNative Framework或AVE返回。 |
| 3368 | 用戶設定無訪問 | 用戶取消了操作或輸入了不允許訪問系統的設定。<br>此錯誤僅在SWF版本19或更高版本中引發。 為了向後相容，對於SWF版本18或更早版本，拋出錯誤代碼3321。<br>分銷商的軟體應指導用戶解釋如何允許無沙盒插件訪問。 有關詳細資訊，請參見 [GoogleChrome的無沙盒訪問被拒絕](https://helpx.adobe.com/adobe-access/kb/error-3321.html) 和 [Chrome中的DRM錯3322/3346/3368（資訊欄問題）](https://forums.adobe.com/message/5520902)。 |
| 3369 | 介面不可用 | 所需的瀏覽器介面不可用。 此問題僅發生在Pepper上。 Flash插件和瀏覽器版本之間可能不匹配。<br>分發程式的軟體應指導用戶確保安裝了最新版本的瀏覽器。<br>如果此錯誤的發生率在增加，並且它們對應於正在發佈的瀏覽器更新，則升級為Adobe。 |
| 3370 | 內容ID設定無訪問 | 用戶已禁用 **允許受保護內容設定的標識符。**<br>**注：** Pepper 13.0.0.x或更高版本出現此錯誤。<br>分銷商的軟體和/或操作團隊應指導用戶啟用 **允許受保護內容的標識符** 的子菜單。<br>有關詳細資訊，請參見 [https://forums.adobe.com/message/6518323#6518323](https://forums.adobe.com/message/6518323#6518323)。 |
| 3371 | NoOPConstraintInPixelConstraints | 基於許可證中的輸出保護約束的解析格式不正確。<br>分發伺服器的軟體應顯示錯誤消息。 要求用戶向具有內容標題的分銷商報告問題。<br>分發伺服器應使用有效的策略重新打包內容。 |
| 3372 | 解析度LagerThanMax解析度 | 內容的解析度大於輸出保護約束中指定的最大解析度。<br>如果分發商的操作團隊在日誌中看到此錯誤，則他們應檢查基於解析度的輸出保護策略，並在必要時重新打包內容。<br>有關基於解析度的輸出保護的詳細資訊，請參見關於基於解析度的輸出保護。 |
| 3373 | DisplayResolutionLagerThanConstrain | 內容的解析度大於當前活動的輸出保護約束所指定的解析度。<br>如果分發商的操作團隊在日誌中看到此錯誤，則他們應檢查基於解析度的輸出保護策略，並在必要時重新打包內容。<br>有關基於解析度的輸出保護的詳細資訊，請參見關於基於解析度的輸出保護。 |
| 3374 | ClientCommProcessFailed | 在客戶端通信處理期間失敗，例如請求生成、響應處理、錯誤的身份驗證令牌等。 |

## 3328的子錯誤代碼映射 {#suberror-code-mapping-for-3328}

| 子錯誤 | 說明 |
|---|---|
| 100-1000 | 由Adobe的許可證伺服器保留 |
| 10000 - 20000 | 由Adobe的個性化伺服器保留 |
| 20100-21000 | 為AdobeXbox密鑰伺服器保留。<br>此範圍中的錯誤映射到常規Mighine DRM Server SDK錯誤消息參考，如下所示：<br>Xbox KeyServer錯誤= DRM伺服器錯誤+ 0x20000<br>例如，Xbox Keyserver Error 20202等效於DRM Server SDK Error 202 |
| 100xxxx | 為客戶端子錯誤代碼保留 |
