---
title: 使用Ant準備密碼
description: 使用Ant準備密碼
copied-description: true
exl-id: 78f00fd7-ca9c-49a9-9e4b-6d1e2daf9241
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---

# 使用Ant準備密碼{#prepare-passwords-using-ant}

使用Ant加密您的密碼：

1. 導覽至 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`
1. 設定 `sdkdir` 中的屬性 [!DNL build-refimpl.xml] 指向包含Primetime DRM Java SDK的目錄。
1. 執行以下命令：

   ```
   ant -f build-refimpl.xml
   ```
