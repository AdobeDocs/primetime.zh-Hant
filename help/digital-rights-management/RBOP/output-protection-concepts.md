---
description: 本節概述了與輸出保護相關的配置、選項和含義。
seo-description: 本節概述了與輸出保護相關的配置、選項和含義。
seo-title: RBOP概念
title: RBOP概念
uuid: fc19c3c9-39a1-4b62-b763-101e5454a01f
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# RBOP概念{#rbop-concepts}

本節概述了與輸出保護相關的配置、選項和含義。

您可以在階層式JSON結構中指定以解析度為基礎的輸出保護需求。 *輸出需求是以像素為基礎。*

在JSON規格的最高層級，您可以定義指定解析度的最大像素解析度和像素限制：

* `maxPixel` -最大像素解析度定義了將進行解密的最大解析度。
* `pixelConstraints` -像素約束定義必須針對指定解析度強制執行的輸出要求。

您可將輸出需求與特定像素限制建立關聯。 您可與指定像素限制關聯的需求類型包括數位、模擬和無線(OTA)連線的限制。

**數位輸出**

數位輸出需求可指定限制性選項，例如「需要數位輸出保護」或「不允許播放」。 輸出要求也可以指定限制較少的選項，例如「不應套用保護」或「如果有使用數位保護」。

**模擬輸出**

模擬輸出連接比數字輸出更簡單；它們由單一輸出要求組成。
