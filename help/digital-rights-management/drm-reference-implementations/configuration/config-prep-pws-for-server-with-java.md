---
title: 使用Java準備密碼
description: 使用Java準備密碼
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '22'
ht-degree: 0%

---

# 使用Java準備密碼{#prepare-passwords-using-java}

執行 `ScrambleUtil.class` 使用Java：

1. 瀏覽至 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/scrambler/ refimpl/scrambler/`
1. 在命令列中，輸入：

   ```
   java -classpath [DRM SDK DVD]/SDK/adobe-flashaccess-sdk.jar;  
       com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```
