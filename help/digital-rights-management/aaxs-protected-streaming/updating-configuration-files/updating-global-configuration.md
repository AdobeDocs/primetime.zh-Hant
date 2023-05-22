---
title: 更新全局配置檔案
description: 更新全局配置檔案
copied-description: true
exl-id: 6544d8ae-6d23-498e-92c5-bad6bfcc10ef
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# 更新全局配置檔案{#updating-the-global-configuration-file}

中的HSM密碼 [!DNL flashaccess-global.xml] 可以隨時修改，更改將在下次伺服器重新載入配置檔案時生效。 但是，不會重新載入對「日誌」和「快取」元素的更改；這些元素中的任何更改都需要重新啟動伺服器。
