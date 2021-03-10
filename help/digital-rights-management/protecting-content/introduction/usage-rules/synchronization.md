---
title: 同步要求
description: 同步要求
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# 同步要求{#requirements-for-synchronization}

同步要求指定客戶端與伺服器同步其狀態的頻率。 如果客戶端已獲得帶外許可證（未聯繫許可證伺服器），使用規則可能會指定客戶端必須向伺服器發送同步消息，以便同步客戶端的安全時間，並向伺服器報告客戶端狀態。

同步行為使用以下參數定義：

* **啟動間隔** -指定上次成功同步後等待多久以啟動另一個同步請求。
* **硬停止間隔** -（可選）。如果未在指定的時間長度內成功同步，則不允許播放。
* **強制同步概率** -（可選）。客戶端在下一個啟動間隔之前發送同步消息的概率。

>[!NOTE]
>
>Primetime DRM用戶端3.0版或更新版本支援此使用規則。 舊客戶端的行為取決於許可證伺服器支援的最低客戶端版本。

