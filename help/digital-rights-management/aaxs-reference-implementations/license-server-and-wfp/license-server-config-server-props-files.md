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

伺服器需要兩個配置檔案，一個用於許可證伺服器，一個用於打包器。 兩個檔案都必須放在類路徑上。 屬性檔案包含由Adobe發出的憑據的位置。 這些憑據可以指定為.pfx檔案和密碼，或者為儲存在HSM上的憑據提供別名和密碼。

有關每個參數的特定值和用法的詳細資訊，請參閱屬性檔案。 示例屬性檔案可在引用實現（引用實現\伺服器\資源）的「資源」目錄中找到。

為確保憑據密碼的安全性，在密碼輸入flashaccess-refimpl.properties或flashaccess-refimpl-packager.properties檔案之前，將提供一個工具(ScrableUtil.class)來加密該密碼。

正確準備憑據的密碼：

1. 轉到 [!DNL Reference Implementation\Server\refimpl\scrambler]。
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
>上例使用分號(;)作為分隔符。 對於MicrosoftWindows以外的平台，請使用冒號(:)作為分隔符。

實用程式將輸出加密的密碼，您必須將其複製到 [!DNL .properties] 的子菜單。
