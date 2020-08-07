---
seo-title: 伺服器屬性檔案
title: 伺服器屬性檔案
uuid: 3d3a0ee3-009f-4d62-9587-7e487ecdcafd
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# 伺服器屬性檔案 {#server-properties-files}

伺服器需要兩個配置檔案，一個用於許可證伺服器，一個用於包裝器。 兩個檔案都必須放在類路徑上。 屬性檔案包含Adobe所核發之憑證的位置。 這些憑據可以指定為。pfx檔案和密碼，或通過為儲存在HSM上的憑據提供別名和密碼來指定。

請參閱屬性檔案，以取得每個參數之特定值和使用情形的詳細資訊。 範例屬性檔案可在參考實作的「資源」目錄(參考Implementation\Server\resources)中找到。

為確保憑證密碼的安全性，我們提供了一個工具(ScrapkUtil.class)，可在密碼輸入flashaccess-refimpl.properties或flashaccess-refimpl-packager.properties檔案之前加密密碼。

要正確準備憑據的密碼，請執行以下操作：

1. 前往 [!DNL Reference Implementation\Server\refimpl\scrambler]。
1. 在命令提示符下，輸入命令：

   ```
   java -classpath  
   <i class="+ topic ph hi-d="" i "="">
   path_to_adobe-flashaccess-sdk.jar.; 
        com.adobe.flashaccess.refimpl.util.ScrambleUtil " 
   <i class="+ topic ph hi-d="" i "="">
   your_pfx_password" 
   </i class="+ topic> 
   </i class="+ topic>
   ```

>[!NOTE]
>
>上例使用分號(;)作為分隔字元。 對於Microsoft Windows以外的平台，請使用冒號(:)作為分隔字元。

該實用程式將輸出加密口令，您必須將其複製到文 [!DNL .properties] 件。
