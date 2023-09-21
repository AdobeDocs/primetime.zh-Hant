---
title: 使用Ant準備密碼
description: 使用Ant準備密碼
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---

# 使用Ant準備密碼{#prepare-passwords-using-ant}

使用Ant加密您的密碼：

1. 瀏覽至 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`
1. 設定 `sdkdir` 中的屬性 [!DNL build-refimpl.xml] 指向包含Primetime DRM Java SDK的目錄。
1. 執行以下命令：

   ```
   ant -f build-refimpl.xml
   ```
