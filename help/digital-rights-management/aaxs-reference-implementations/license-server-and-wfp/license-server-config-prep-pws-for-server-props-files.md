---
title: 為伺服器屬性檔案準備密碼
description: 為伺服器屬性檔案準備密碼
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# 為伺服器屬性檔案{#preparing-passwords-for-the-server-properties-files}準備密碼

為確保憑證密碼的安全性，在將密碼輸入[!DNL flashaccess-refimpl.properties]或[!DNL flashaccess-refimpl-packager.properties]檔案之前，會提供加密工具。

要使用提供的ANT指令碼運行工具，請執行以下操作：

* 前往&#x200B;*`<Reference Implementation Server Path>`* [!DNL \refimpl]

* 確保[!DNL build-refimpl.xml]中的`sdkdir`屬性指向包含Adobe訪問SDK的目錄
* 使用ANT運行以下命令：

   ```
       ant -f build-refimpl.xml
   ```

* 出現提示時，鍵入憑據的密碼

要使用Java運行工具，請執行以下操作：

* 前往&#x200B;*`<Reference Implementation Server Path>`*\ [!DNL scrambler]

* 在命令提示符下，輸入命令：

* 在Windows上：

   ```
   java -classpath path_to_adobe-flashaccess-sdk.jar;.  
   com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```

* 在Linux上：

   ```
       java -classpath path_to_adobe-flashaccess-sdk.jar;.  
       com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```

該實用程式將輸出加密口令，您必須將該口令複製到。properties檔案。

>[!NOTE]
>
>使用隨參考實現提供的密碼置亂實用程式編碼的密碼將無法與Adobe Access Server的受保護流處理方案一起使用。
