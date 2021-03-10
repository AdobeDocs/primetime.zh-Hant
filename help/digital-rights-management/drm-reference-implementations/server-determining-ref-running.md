---
title: 確定Reference Implementation License Server是否正常運行
description: 確定Reference Implementation License Server是否正常運行
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# 確定Reference Implementation License Server是否正確運行{#determining-if-reference-implementation-license-server-runs-properly}

有幾種方法可判斷您的「參考實作授權伺服器」是否已正確啟動。 您可以查看[!DNL catalina.log]日誌可能不夠，因為許可證伺服器將日誌記錄到其自己的日誌檔案。 請依照下列步驟來確保您的參考實作已正確啟動。

* 檢查[!DNL AdobeFlashAccess.log]檔案。 這是「參考實施」寫入日誌資訊的位置。 此日誌檔案的位置由[!DNL log4j.xml]檔案指示，可修改為指向任何您想要的位置。 預設情況下，日誌檔案被複製到運行Catalina的工作目錄。

* 前往下列URL:[!DNL https:// flashaccess/license/v4]*您的伺服器：伺服器埠*。 您應看到「License Server is setup correctly（授權伺服器已正確設定）」文字。

另一個測試伺服器是否正確執行的方法是封裝測試內容的區段、設定範例視訊播放器，然後播放它。

以下過程說明此過程：

1. 前往[!DNL \Reference Implementation\Command Line Tools]資料夾。

   有關如何安裝命令行工具的資訊，請參見[安裝命令行工具](../drm-reference-implementations/command-line-tools/install-command-line-tools.md)。

1. 鍵入以下命令以建立簡單的匿名DRM策略：

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   有關如何使用DRM策略管理器建立DRM策略，請參見[命令行使用](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md)。

1. 將[!DNL flashaccesstools.properties]檔案中的`encrypt.license.serverurl`屬性設定為授權伺服器的URL。

   例如，[!DNL https:// localhost:8080/]。 [!DNL flashaccesstools.properties]檔案位於[!DNL \Reference Implementation\Command Line Tools]資料夾中。

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

1. 將兩個生成的檔案複製到Tomcat伺服器上的[!DNL webapps\ROOT\Content]資料夾。
1. 轉到[!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release]目錄，並將內容複製到Tomcat伺服器上的 [!DNL webapps\ROOT\SVP\] 資料夾。

1. 安裝Flash Player10.1版或更新版本。
1. 開啟網頁瀏覽器並前往下列URL:[!DNL        https:// localhost:8080/SVP/player.html]

1. 前往下列URL，然後按一下&#x200B;**[!UICONTROL Play]**:[!DNL https:// localhost:8080/Content/] *`your_encrypted_FLV`*。

1. 如果視頻播放失敗，請檢查「示例視頻播放器」的記錄窗格中是否顯示任何錯誤代碼，或者是否添加到[!DNL AdobeFlashAccess.log]檔案。

   您現在可以在log4j.xml檔案中搜索[!DNL AdobeFlashAccess.log]日誌檔案的位置，然後對其進行修改。 預設情況下，日誌檔案將複製到運行Catalina的工作目錄中。

