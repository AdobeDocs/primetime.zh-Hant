---
title: 更新全域組態檔
description: 更新全域組態檔
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# 更新全域組態檔{#updating-the-global-configuration-file}

中的HSM密碼 [!DNL flashaccess-global.xml] 可隨時修改，而變更會在下次伺服器重新載入組態檔時生效。 不過，不會重新載入「記錄」和「快取」元素的變更；這些元素中的任何變更都需要伺服器重新啟動。
