---
description: 'null'
seo-description: 'null'
seo-title: 使用Ant準備密碼
title: 使用Ant準備密碼
uuid: 9419ab0d-b448-4881-9d26-35c00f0b13bc
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用Ant準備密碼{#prepare-passwords-using-ant}

使用Ant加密您的密碼：

1. 導覽至 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`
1. 將中的 `sdkdir` 屬性設 [!DNL build-refimpl.xml] 置為指向包含Primetime DRM Java SDK的目錄。
1. 運行以下命令：

   ```
   ant -f build-refimpl.xml
   ```

