---
title: 伺服器屬性檔案
description: 伺服器屬性檔案
copied-description: true
exl-id: c42fde8f-e438-4497-bd15-ebd0f6e2eed7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# 伺服器屬性檔案 {#server-properties-files}

伺服器需要兩個組態檔，一個用於授權伺服器，另一個用於封裝程式。 這兩個檔案都必須放置在類別路徑上。 屬性檔案包含Adobe所核發的認證的位置。 這些認證可指定為.pfx檔案和密碼，或為HSM上儲存的認證提供別名及密碼。

請參考屬性檔案，以取得有關每個引數的特定值和用法的詳細資訊。 範例屬性檔案可在參考實作(Reference Implementation\Server\resources)的「resources」目錄中找到。

為確保認證密碼的安全性，系統提供工具(ScrambleUtil.class)，用於在密碼輸入flashaccess-refimpl.properties或flashaccess-refimpl-packager.properties檔案之前加密密碼。

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
