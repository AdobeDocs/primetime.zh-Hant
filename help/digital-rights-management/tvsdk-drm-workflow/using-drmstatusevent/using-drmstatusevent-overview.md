---
title: 使用DRMStatusEvent類概述
description: 使用DRMStatusEvent類概述
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---


# 概述 {#using-the-drmstatusevent-class-overview}

A `DRMStatusEvent` 當由Mogfire DRM保護的內容開始成功播放時，會調度對象。 （成功意味著許可證已驗證，用戶已通過驗證並且已授權查看內容）。

的 `DRMStatusEvent` 對象包含與許可證相關的資訊，包括許可證是否可以離線使用或許可證過期且內容無法再查看。
