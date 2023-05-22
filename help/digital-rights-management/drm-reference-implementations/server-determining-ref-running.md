---
title: 確定引用實施許可證伺服器是否正常運行
description: 確定引用實施許可證伺服器是否正常運行
copied-description: true
exl-id: 97ca0b6c-2661-4cdc-b8d0-dcc545f009f6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 確定引用實施許可證伺服器是否正常運行 {#determining-if-reference-implementation-license-server-runs-properly}

有幾種方法可確定您的參考實施許可證伺服器是否已正確啟動。 您可以查看 [!DNL catalina.log] 日誌可能不足，因為許可證伺服器將記錄到其自己的日誌檔案中。 請按照以下步驟來確保您的參考實施已正確啟動。

* 檢查 [!DNL AdobeFlashAccess.log] 的子菜單。 這是參考實現寫入日誌資訊的位置。 此日誌檔案的位置由 [!DNL log4j.xml] 檔案，並可修改以指向任何您想要的位置。 預設情況下，日誌檔案複製到運行catalina的工作目錄。

* 轉到以下URL: [!DNL https:// flashaccess/license/v4]*伺服器：伺服器埠*。 您應看到文本「License Server is setup correctly（許可證伺服器設定正確）」。

如果伺服器運行正確，則另一種test方法是將test內容的一段打包，設定一個示例視頻播放器，然後播放。

以下過程描述了此過程：

1. 轉到 [!DNL \Reference Implementation\Command Line Tools] 的子菜單。

   請參閱 [安裝命令行工具](../drm-reference-implementations/command-line-tools/install-command-line-tools.md) 有關如何安裝命令行工具的資訊。

1. 鍵入以下命令以建立簡單的匿名DRM策略：

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   請參閱 [命令行用法](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md) 有關如何使用「DRM策略管理器」建立DRM策略。

1. 設定 `encrypt.license.serverurl` 屬性 [!DNL flashaccesstools.properties] 檔案到許可證伺服器的URL。

   比如說， [!DNL https:// localhost:8080/]。 的 [!DNL flashaccesstools.properties] 檔案位於 [!DNL \Reference Implementation\Command Line Tools] 的子菜單。

1. 鍵入以下命令以打包內容的段：

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

1. 將兩個生成的檔案複製到 [!DNL webapps\ROOT\Content] 資料夾。
1. 轉到 [!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release] 目錄並將內容複製到 [!DNL webapps\ROOT\SVP\] 資料夾。

1. 安裝Flash Player10.1版或更高版本。
1. 開啟Web瀏覽器並轉到以下URL: [!DNL        https:// localhost:8080/SVP/player.html]

1. 轉到以下URL，然後按一下 **[!UICONTROL Play]**: [!DNL https:// localhost:8080/Content/] *`your_encrypted_FLV`*。

1. 如果視頻播放失敗，請檢查示例視頻播放器的日誌窗格中是否顯示任何錯誤代碼或是否添加到 [!DNL AdobeFlashAccess.log] 的子菜單。

   您現在可以搜索 [!DNL AdobeFlashAccess.log] 日誌檔案，然後對其進行修改。 預設情況下，日誌檔案會複製到運行catalina的工作目錄中。
