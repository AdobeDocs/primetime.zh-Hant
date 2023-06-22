---
title: 正在準備伺服器屬性檔案的密碼
description: 正在準備伺服器屬性檔案的密碼
copied-description: true
exl-id: 70f75640-7075-450a-8191-dc348bd269b8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# 正在準備伺服器屬性檔案的密碼 {#preparing-passwords-for-the-server-properties-files}

為確保認證密碼的安全性，系統會在您輸入密碼之前提供加密密碼的工具。 [!DNL flashaccess-refimpl.properties] 或 [!DNL flashaccess-refimpl-packager.properties] 檔案。

若要使用提供的ANT指令碼執行工具：

* 前往 *`<Reference Implementation Server Path>`* [!DNL \refimpl]

* 確保 `sdkdir` 中的屬性 [!DNL build-refimpl.xml] 指向包含Adobe存取SDK的目錄
* 使用ANT執行以下命令：

   ```
       ant -f build-refimpl.xml
   ```

* 出現提示時，輸入認證的密碼

若要使用Java執行工具：

* 前往 *`<Reference Implementation Server Path>`*\ [!DNL scrambler]

* 在命令提示字元中輸入命令：

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

公用程式會輸出加密的密碼，您必須將其複製到.properties檔案。

>[!NOTE]
>
>使用參考實作隨附的密碼加擾公用程式編碼的密碼，無法搭配Adobe Access Server使用。
