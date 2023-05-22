---
title: 自定義身份驗證/權利概述（可選）
description: 自定義身份驗證/權利概述（可選）
copied-description: true
exl-id: d92c4246-c772-44da-80b6-4086dfc30ff4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# 自定義身份驗證/權利概述（可選）{#custom-authentication-entitlement-overview-optional}

可將Mogife Cloud DRM配置為訪問您自己的後端身份驗證/權利服務，以確定：

* 是否允許此用戶獲取許可證？
* 許可證中應包含哪些權利/限制？

黃金時段雲DRM包括後端認證/權利服務的參考實現。 為了進行演示，此伺服器正在對BEES請求發出「允許」響應。 請參閱 [!DNL BEESServlet.java] 修改伺服器行為。

>[!NOTE]
>
>以前，這是一個名為 *後端權利伺服器* (BEES)，因此在本文檔和源檔案中都引用了BEES。
