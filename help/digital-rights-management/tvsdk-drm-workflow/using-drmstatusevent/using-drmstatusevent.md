---
title: 使用DRMStatusEvent類別概觀
description: 使用DRMStatusEvent類別概觀
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# 使用DRMStatusEvent類別概觀 {#using-the-drmstatusevent-class-overview}

A `DRMStatusEvent` 物件會在Primetime DRM所保護的內容開始成功播放時傳送。 （成功表示授權已驗證，且使用者已驗證並獲授權檢視內容）。

此 `DRMStatusEvent` 物件包含與授權相關的資訊，包括授權是否可離線使用，或授權到期且無法再檢視內容時。
