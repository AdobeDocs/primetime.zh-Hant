---
description: 'null'
seo-description: 'null'
seo-title: 確定Reference Implementation License Server是否正常運行
title: 確定Reference Implementation License Server是否正常運行
uuid: 84d32c94-7594-464e-a883-5338b52de2bf
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 確定Reference Implementation License Server是否正常運行 {#determining-if-reference-implementation-license-server-is-running-properly}

有幾種方法可判斷您的伺服器是否已正確啟動。 查看日 [!DNL catalina.log] 志可能不夠，因為許可證伺服器會登錄到自己的日誌檔案。 請依照下列步驟來確保您的參考實作已正確啟動。

* 檢查您的 [!DNL AdobeFlashAccess.log] 檔案。 這是「參考實施」寫入日誌資訊的位置。 此日誌檔案的位置由您的文 [!DNL log4j.xml] 件指示，可以修改為指向任何您想要的位置。 預設情況下，日誌檔案將輸出到運行Catalina的工作目錄。

* 導覽至下列URL: `https:///flashaccess/license/v4<your server:server port>`。 您應看到「License Server is setup correctly（授權伺服器已正確設定）」文字。

另一種測試伺服器是否正常運作的方式，是封裝測試內容、設定範例視訊播放程式，然後播放它。 以下過程說明此過程：

1. 導覽至資料 [!DNL \Reference Implementation\Command Line Tools] 夾。 有關安裝命令行工具的資訊，請參 [閱安裝命令行工具](../aaxs-reference-implementations/command-line-tools/aaxs-ref-impl-command-line-overview.md#installing-the-command-line-tools)。

1. 使用以下命令建立簡單的匿名策略：

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   有關使用策略管理器建立策略的詳細資訊，請參閱命 [令行用法](../aaxs-reference-implementations/command-line-tools/policy-manager/command-line-usage.md)。

1. 將檔 `encrypt.license.serverurl` 案中的屬 [!DNL flashaccesstools.properties] 性設為授權伺服器的URL(例如 `https:// localhost:8080/`)。 文 [!DNL flashaccesstools.properties] 件位於資料夾 [!DNL \Reference Implementation\Command Line Tools] 下。

1. 使用下列命令封裝內容：

   ```java
       java -jar libs\AdobePackager.jar  
   <i class="+ topic ph hi-d="" i "="">
   test_input_FLV  
   <i class="+ topic ph hi-d="" i "="">
   output_file  
               -p policy_test.pol 
   </i class="+ topic> 
   </i class="+ topic>
   ```

1. 將生成的2個檔案複製到Tomcat文 [!DNL webapps\ROOT\Content] 件夾。
1. 導覽至 `Reference Implementation\Sample Video Players\Desktop\Flash Player\Release` 內容並將其複製到Tomcat資 `webapps\ROOT\SVP\` 料夾。
1. 安裝Flash Player 10.1或更新版本。
1. 開啟網頁瀏覽器並導覽至下列URL:

   `https:// localhost:8080/SVP/player.html`
1. 導覽至下列URL，然後按一下「播放」按鈕：

   `https:// localhost:8080/Content/<your_encrypted_FLV>`
1. 如果視訊播放失敗，請檢查Sample Video Player的記錄窗格或檔案中是否已寫入任何錯誤 `AdobeFlashAccess.log` 碼。 日誌檔案的 `AdobeFlashAccess.log` 位置由log4j.xml檔案指示，可以修改為指向您想要的任何位置。 預設情況下，日誌檔案將寫入到運行Catalina的工作目錄。
