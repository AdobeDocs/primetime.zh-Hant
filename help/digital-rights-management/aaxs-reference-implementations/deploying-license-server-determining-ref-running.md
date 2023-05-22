---
title: 確定引用實施許可證伺服器是否正常運行
description: 確定引用實施許可證伺服器是否正常運行
copied-description: true
exl-id: ef28e169-f8d2-4c7f-b606-aa4e811aae9b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 確定引用實施許可證伺服器是否正常運行 {#determining-if-reference-implementation-license-server-is-running-properly}

有幾種方法可確定伺服器是否已正確啟動。 查看 [!DNL catalina.log] 日誌可能不足，因為許可證伺服器將記錄到其自己的日誌檔案中。 請按照以下步驟來確保您的參考實施已正確啟動。

* 檢查 [!DNL AdobeFlashAccess.log] 的子菜單。 這是參考實現寫入日誌資訊的位置。 此日誌檔案的位置由 [!DNL log4j.xml] 檔案，並可修改以指向任何您想要的位置。 預設情況下，日誌檔案將輸出到運行catalina的工作目錄。

* 導航到以下URL: `https:///flashaccess/license/v4<your server:server port>`。 您應看到文本「License Server is setup correctly（許可證伺服器設定正確）」。

如果伺服器正常運行，則test的另一種方法是打包一段test內容，設定一個示例視頻播放器，然後播放它。 以下過程描述了此過程：

1. 導航到 [!DNL \Reference Implementation\Command Line Tools] 的子菜單。 有關安裝命令行工具的資訊，請參見 [安裝命令行工具](../aaxs-reference-implementations/command-line-tools/aaxs-ref-impl-command-line-overview.md#installing-the-command-line-tools)。

1. 使用以下命令建立簡單的匿名策略：

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   有關使用策略管理器建立策略的詳細資訊，請參見 [命令行用法](../aaxs-reference-implementations/command-line-tools/policy-manager/command-line-usage.md)。

1. 設定 `encrypt.license.serverurl` 屬性 [!DNL flashaccesstools.properties] 檔案到許可證伺服器的URL(例如， `https:// localhost:8080/`)。 的 [!DNL flashaccesstools.properties] 檔案位於 [!DNL \Reference Implementation\Command Line Tools] 的子菜單。

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

1. 將生成的2個檔案複製到Tomcat [!DNL webapps\ROOT\Content] 的子菜單。
1. 導航到 `Reference Implementation\Sample Video Players\Desktop\Flash Player\Release` 並將內容複製到Tomcat `webapps\ROOT\SVP\` 的子菜單。
1. 安裝Flash Player10.1或更高版本。
1. 開啟Web瀏覽器並導航至以下URL:

   `https:// localhost:8080/SVP/player.html`
1. 導航到以下URL，然後按一下「播放」按鈕：

   `https:// localhost:8080/Content/<your_encrypted_FLV>`
1. 如果視頻播放失敗，請檢查示例視頻播放器的日誌記錄窗格中或 `AdobeFlashAccess.log` 的子菜單。 位置 `AdobeFlashAccess.log` 日誌檔案由log4j.xml檔案指示，可以修改為指向任意位置。 預設情況下，日誌檔案將寫入運行catalina的工作目錄。
