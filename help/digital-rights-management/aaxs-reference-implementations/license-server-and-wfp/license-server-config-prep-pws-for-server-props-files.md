---
seo-title: 為伺服器屬性檔案準備密碼
title: 為伺服器屬性檔案準備密碼
uuid: 2d876eb0-b1a5-4c30-ae96-0a22f6a03910
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 為伺服器屬性檔案準備密碼 {#preparing-passwords-for-the-server-properties-files}

為確保憑證密碼的安全性，在將密碼輸入或檔案之前，會提供加密 [!DNL flashaccess-refimpl.properties] 工 [!DNL flashaccess-refimpl-packager.properties] 具。

要使用提供的ANT指令碼運行工具，請執行以下操作：

* 前往 *`<Reference Implementation Server Path>`*[!DNL \refimpl]

* 請確 `sdkdir` 定位 [!DNL build-refimpl.xml] 於包含Adobe Access SDK之目錄的屬性
* 使用ANT運行以下命令：

   ```
       ant -f build-refimpl.xml
   ```

* 出現提示時，鍵入憑據的密碼

要使用Java運行工具，請執行以下操作：

* 前往 *`<Reference Implementation Server Path>`*\ [!DNL scrambler]

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
>使用參考實作提供的密碼置亂公用程式編碼的密碼，將無法與Adobe Access Server for Protected Streaming搭配使用。
