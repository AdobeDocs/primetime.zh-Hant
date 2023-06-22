---
title: 判斷Reference Implementation License Server是否正確執行
description: 判斷Reference Implementation License Server是否正確執行
copied-description: true
exl-id: ef28e169-f8d2-4c7f-b606-aa4e811aae9b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 判斷Reference Implementation License Server是否正確執行 {#determining-if-reference-implementation-license-server-is-running-properly}

有數種方法可判斷伺服器是否正確啟動。 檢視 [!DNL catalina.log] 記錄檔可能不足，因為授權伺服器會記錄到自己的記錄檔。 請依照下列步驟操作，以確保您的Reference實作已正確啟動。

* 檢查您的 [!DNL AdobeFlashAccess.log] 檔案。 這是參考實作寫入記錄資訊的位置。 此記錄檔的位置由以下指示： [!DNL log4j.xml] 檔案，並可修改為指向您想要的任何位置。 依預設，記錄檔會輸出至您執行catalina的工作目錄。

* 導覽至下列URL： `https:///flashaccess/license/v4<your server:server port>`. 您應該會看到「License Server已正確設定」文字。

測試伺服器是否正常運作的另一種方法是封裝測試內容、設定範例視訊播放器並播放。 下列程式說明此程式：

1. 導覽至 [!DNL \Reference Implementation\Command Line Tools] 資料夾。 如需安裝命令列工具的資訊，請參閱 [安裝命令列工具](../aaxs-reference-implementations/command-line-tools/aaxs-ref-impl-command-line-overview.md#installing-the-command-line-tools).

1. 使用以下命令建立簡單的匿名原則：

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   如需有關使用原則管理員建立原則的詳細資訊，請參閱 [命令列使用方式](../aaxs-reference-implementations/command-line-tools/policy-manager/command-line-usage.md).

1. 設定 `encrypt.license.serverurl` 中的屬性 [!DNL flashaccesstools.properties] 檔案至授權伺服器的URL (例如， `https:// localhost:8080/`)。 此 [!DNL flashaccesstools.properties] 檔案位於 [!DNL \Reference Implementation\Command Line Tools] 資料夾。

1. 使用以下命令封裝一段內容：

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

1. 將2個產生的檔案複製到Tomcat [!DNL webapps\ROOT\Content] 資料夾。
1. 導覽至 `Reference Implementation\Sample Video Players\Desktop\Flash Player\Release` 並將內容複製到Tomcat `webapps\ROOT\SVP\` 資料夾。
1. 安裝Flash Player10.1或更新版本。
1. 開啟網頁瀏覽器，並導覽至下列URL：

   `https:// localhost:8080/SVP/player.html`
1. 導覽至下列URL，然後按一下「播放」按鈕：

   `https:// localhost:8080/Content/<your_encrypted_FLV>`
1. 如果視訊無法播放，請檢查是否已將任何錯誤碼寫入範例視訊播放器的記錄窗格中，或寫入 `AdobeFlashAccess.log` 檔案。 的位置 `AdobeFlashAccess.log` log檔案由您的log4j.xml檔案表示，可以修改為指向您想要的任何位置。 依預設，記錄檔會寫入您執行catalina的工作目錄中。
