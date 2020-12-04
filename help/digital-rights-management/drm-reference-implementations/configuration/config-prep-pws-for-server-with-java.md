---
description: 'null'
seo-description: 'null'
seo-title: 使用Java準備密碼
title: 使用Java準備密碼
uuid: 8a708d22-764f-4229-95ca-109482563432
translation-type: tm+mt
source-git-commit: 055989cbe3a187516f18816492aaea709cc80c81
workflow-type: tm+mt
source-wordcount: '24'
ht-degree: 0%

---


# 使用Java{#prepare-passwords-using-java}準備密碼

使用Java運行`ScrambleUtil.class` :

1. 導覽至`[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/scrambler/ refimpl/scrambler/`
1. 在命令行中鍵入：

   ```
   java -classpath [DRM SDK DVD]/SDK/adobe-flashaccess-sdk.jar;  
       com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```

