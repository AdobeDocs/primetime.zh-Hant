---
title: 判斷參考實作授權伺服器是否正確執行
description: 判斷參考實作授權伺服器是否正確執行
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 判斷參考實作授權伺服器是否正確執行 {#determining-if-reference-implementation-license-server-runs-properly}

有數種方式可判斷您的參考實作授權伺服器是否已正確啟動。 您可以檢視 [!DNL catalina.log] 記錄可能還不夠，因為許可證伺服器會記錄到自己的記錄檔。 請依照下列步驟操作，確定您的參考實作已正確啟動。

* 檢查您的 [!DNL AdobeFlashAccess.log] 檔案。 這是參考實作寫入記錄資訊的位置。 此記錄檔的位置由您的 [!DNL log4j.xml] 檔案，並可修改為指向任何您想要的位置。 依預設，日誌檔會複製到您執行catalina的工作目錄中。

* 前往下列URL： [!DNL https:// flashaccess/license/v4]*您的伺服器：伺服器連線埠*. 您應該會看到「License Server已正確設定」文字。

測試伺服器是否正確執行的另一種方法是封裝測試內容的區段、設定範例視訊播放器，然後播放它。

下列程式說明此程式：

1. 前往 [!DNL \Reference Implementation\Command Line Tools] 資料夾。

   另請參閱 [安裝命令列工具](../drm-reference-implementations/command-line-tools/install-command-line-tools.md) 說明如何安裝命令列工具。

1. 輸入下列指令以建立簡單的匿名DRM原則：

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   另請參閱 [命令列使用方式](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md) 有關如何使用DRM Policy Manager建立DRM政策。

1. 設定 `encrypt.license.serverurl` 中的屬性 [!DNL flashaccesstools.properties] 檔案至授權伺服器的URL。

   例如， [!DNL https:// localhost:8080/]. 此 [!DNL flashaccesstools.properties] 檔案位於 [!DNL \Reference Implementation\Command Line Tools] 資料夾。

1. 輸入下列命令以封裝內容的區段：

```
       java -jar libs\AdobePackager.jar  
       <i class="+ topic ph hi-d="" i "="">
         test_input_FLV  
        <i class="+ topic ph hi-d="" i "="">
       output_file  
               -p policy_test.pol 
       </i class="+ topic> 
       </i class="+ topic>
```

1. 將兩個產生的檔案複製到 [!DNL webapps\ROOT\Content] 資料夾。
1. 前往 [!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release] 目錄並將內容複製到 [!DNL webapps\ROOT\SVP\] 資料夾。

1. 安裝Flash Player版本10.1或更新版本。
1. 開啟網頁瀏覽器，然後前往下列URL： [!DNL        https:// localhost:8080/SVP/player.html]

1. 前往下列URL，然後按一下 **[!UICONTROL Play]**： [!DNL https:// localhost:8080/Content/] *`your_encrypted_FLV`*.

1. 如果影片無法播放，請檢查範例影片播放器的記錄窗格中是否顯示任何錯誤碼，或將其新增至 [!DNL AdobeFlashAccess.log] 檔案。

   您現在可以搜尋 [!DNL AdobeFlashAccess.log] log4j.xml檔案中的記錄檔，然後加以修改。 依預設，記錄檔會複製到您執行catalina的工作目錄中。
