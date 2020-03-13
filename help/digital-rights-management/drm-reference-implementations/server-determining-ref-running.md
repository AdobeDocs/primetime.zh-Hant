---
description: 'null'
seo-description: 'null'
seo-title: 確定Reference Implementation License Server是否正常運行
title: 確定Reference Implementation License Server是否正常運行
uuid: afd82d6d-a11c-48ff-b48c-8f81d4b406a0
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# 確定Reference Implementation License Server是否正常運行 {#determining-if-reference-implementation-license-server-runs-properly}

有幾種方法可判斷您的「參考實作授權伺服器」是否已正確啟動。 由於許可證服 [!DNL catalina.log] 務器登錄到自己的日誌檔案，因此您可以查看日誌可能不夠。 請依照下列步驟來確保您的參考實作已正確啟動。

* 檢查您的 [!DNL AdobeFlashAccess.log] 檔案。 這是「參考實施」寫入日誌資訊的位置。 此日誌檔案的位置由您的文 [!DNL log4j.xml] 件指示，可以修改為指向任何您想要的位置。 預設情況下，日誌檔案被複製到運行Catalina的工作目錄。

* 前往下列URL:您的 [!DNL https:// flashaccess/license/v4]*伺服器：伺服器埠&#x200B;*。 您應看到「License Server is setup correctly（授權伺服器已正確設定）」文字。

另一個測試伺服器是否正確執行的方法是封裝測試內容的區段、設定範例視訊播放器，然後播放它。

以下過程說明此過程：

1. 前往資料 [!DNL \Reference Implementation\Command Line Tools] 夾。

   請參 [閱安裝命令行工具](../drm-reference-implementations/command-line-tools/install-command-line-tools.md) ，瞭解如何安裝命令行工具。

1. 鍵入以下命令以建立簡單的匿名DRM策略：

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   請參 [閱命令行使用](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md) ，瞭解如何使用DRM策略管理器建立DRM策略。

1. 將檔 `encrypt.license.serverurl` 案中的屬 [!DNL flashaccesstools.properties] 性設為授權伺服器的URL。

   For example, [!DNL https:// localhost:8080/]. 文 [!DNL flashaccesstools.properties] 件位於檔案 [!DNL \Reference Implementation\Command Line Tools] 夾中。

1. 鍵入以下命令以封裝內容的段：

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

1. 將兩個生成的檔案複製到Tomcat [!DNL webapps\ROOT\Content] 伺服器上的資料夾。
1. 轉到目 [!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release] 錄，並將內容複製到Tomcat伺服器上的[!DNL webapps\ROOT\SVP\]資料夾。

1. 安裝Flash Player 10.1版或更新版本。
1. 開啟網頁瀏覽器並前往下列URL: [!DNL        https:// localhost:8080/SVP/player.html]

1. 前往下列URL，然後按一下 **[!UICONTROL Play]**: [!DNL https:// localhost:8080/Content/]*`your_encrypted_FLV`*.

1. 如果視訊播放失敗，請檢查「範例視訊播放器」的記錄窗格中是否顯示任何錯誤碼，或是新增至檔 [!DNL AdobeFlashAccess.log] 案。

   您現在可以搜尋log4j.xml檔 [!DNL AdobeFlashAccess.log] 案中記錄檔的位置，然後加以修改。 預設情況下，日誌檔案將複製到運行Catalina的工作目錄中。

