---
title: 正在準備伺服器屬性檔案的密碼
description: 正在準備伺服器屬性檔案的密碼
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# 正在準備伺服器屬性檔案的密碼 {#preparing-passwords-for-the-server-properties-files}

為確保認證密碼的安全，系統提供工具在密碼輸入到密碼之前對其進行加密 [!DNL flashaccess-refimpl.properties] 或 [!DNL flashaccess-refimpl-packager.properties] 檔案。

若要使用提供的ANT指令碼執行工具：

* 前往 *`<Reference Implementation Server Path>`* [!DNL \refimpl]

* 確保 `sdkdir` 中的屬性 [!DNL build-refimpl.xml] 指向包含Adobe存取SDK的目錄
* 使用ANT執行以下命令：

  ```
      ant -f build-refimpl.xml
  ```

* 出現提示時，輸入您的認證密碼

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
>使用參考實作隨附的密碼加擾公用程式編碼的密碼，無法搭配Adobe Access Server使用保護資料流。
