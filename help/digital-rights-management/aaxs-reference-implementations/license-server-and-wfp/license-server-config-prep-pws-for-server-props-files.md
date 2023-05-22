---
title: 為伺服器屬性檔案準備密碼
description: 為伺服器屬性檔案準備密碼
copied-description: true
exl-id: 70f75640-7075-450a-8191-dc348bd269b8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# 為伺服器屬性檔案準備密碼 {#preparing-passwords-for-the-server-properties-files}

為確保憑據密碼的安全性，在將密碼輸入到 [!DNL flashaccess-refimpl.properties] 或 [!DNL flashaccess-refimpl-packager.properties] 的子菜單。

要使用提供的ANT指令碼運行工具：

* 轉到 *`<Reference Implementation Server Path>`* [!DNL \refimpl]

* 確保 `sdkdir` 物業 [!DNL build-refimpl.xml] 指向包含Adobe訪問SDK的目錄
* 使用ANT運行以下命令：

   ```
       ant -f build-refimpl.xml
   ```

* 出現提示時，鍵入憑據的密碼

要使用Java運行工具：

* 轉到 *`<Reference Implementation Server Path>`*\ [!DNL scrambler]

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

該實用程式將輸出加密的密碼，您必須將其複製到.properties檔案。

>[!NOTE]
>
>使用隨參考實現提供的密碼加擾實用程式編碼的密碼將無法與Adobe Access Server的受保護流管理協作。
