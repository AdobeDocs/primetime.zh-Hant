---
title: 伺服器屬性檔案
description: 伺服器屬性檔案
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# 伺服器屬性檔案 {#server-properties-files}

伺服器需要兩個組態檔，一個用於授權伺服器，另一個用於封裝程式。 兩個檔案都必須放置在類別路徑上。 屬性檔案包含Adobe所核發的認證位置。 這些認證可指定為.pfx檔案和密碼，或為HSM上儲存的認證提供別名及密碼。

如需每個引數之特定值和使用方式的詳細資訊，請參閱屬性檔案。 範例屬性檔案可在參考實作(Reference Implementation\Server\resources)的「resources」目錄中找到。

為了確保認證密碼的安全性，系統提供工具(ScrambleUtil.class)，以便在密碼輸入flashaccess-refimpl.properties或flashaccess-refimpl-packager.properties檔案之前先加密密碼。

若要正確準備認證的密碼：

1. 前往 [!DNL Reference Implementation\Server\refimpl\scrambler].
1. 在命令提示字元中輸入命令：

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
>上一個範例使用分號(；)做為分隔字元。 對於Microsoft Windows以外的平台，請使用冒號(：)作為分隔字元。

公用程式會輸出加密的密碼，您必須將其複製到 [!DNL .properties] 檔案。
