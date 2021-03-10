---
title: 使用Ant準備密碼
description: 使用Ant準備密碼
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---


# 使用Ant{#prepare-passwords-using-ant}準備密碼

使用Ant加密您的密碼：

1. 導覽至`[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`
1. 將[!DNL build-refimpl.xml]中的`sdkdir`屬性設為指向包含Primetime DRM Java SDK的目錄。
1. 運行以下命令：

   ```
   ant -f build-refimpl.xml
   ```

