---
description: 要允許廣告解析程式工作，廣告提供程式(如Adobe Primetime廣告決定)需要配置值才能啟用與提供程式的連接。
title: 廣告插入元資料
exl-id: 7245b42c-f3ba-43ec-b895-c1a2d66aa11f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 概述 {#ad-insertion-metadata}

要允許廣告解析程式工作，廣告提供程式(如Adobe Primetime廣告決定)需要配置值才能啟用與提供程式的連接。

TVSDK包括黃金時段廣告決策庫。 要使您的內容包括來自黃金時段廣告決策伺服器的廣告，您的應用程式必須提供以下要求 `AuditudeSettings` 資訊：

* `mediaID`，它是要播放的視頻的唯一標識符。

   發佈者將 `mediaID` 將視頻內容和廣告資訊提交到Adobe Primetime廣告決策伺服器時。 該ID由黃金時段廣告決策用於從伺服器檢索視頻的相關廣告資訊。

* （可選） `defaultMediaId`，它指定在滿足以下條件時提供的廣告：

   * 您對廣告伺服器的請求無效，或內容配置不正確。
   * 黃金時段廣告決策在傳播資料時遇到延遲。
   * 黃金時段廣告決策後端進程之一出現故障或不可用。

   >[!TIP]
   >
   >Adobe建議使用 `defaultMediaId`。

* 您 `zoneID`，由Adobe分配，標識您的公司或網站。
* 分配的廣告伺服器的域。
* 其他目標參數。

   您可以根據您的需要和廣告提供商的需要包括這些參數。
