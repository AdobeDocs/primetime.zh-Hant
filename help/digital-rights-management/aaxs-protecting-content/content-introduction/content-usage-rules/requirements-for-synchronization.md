---
title: 同步要求
description: 同步要求
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# 同步要求{#requirements-for-synchronization}

指定客戶端將其狀態與伺服器同步的頻率。 如果客戶端已頒發帶外許可證（未聯繫許可證伺服器），則使用規則可指定客戶端必須向伺服器發送同步消息以便同步客戶端的安全時間並將客戶端狀態報告給伺服器。

同步行為使用以下參數定義：

* 啟動間隔 — 指定上次成功同步後等待啟動另一個同步請求的時間。
* 硬停止間隔 — （可選）。 如果在指定的時間內未成功同步，則不允許播放。
* 強制同步概率 — （可選）。 客戶端在下一個啟動間隔之前發送同步消息的概率。

>[!NOTE]
>
>Adobe訪問客戶端3.0及更高版本支援此使用規則。 舊客戶端的行為取決於許可證伺服器支援的最低客戶端版本。 看， [最低客戶端版本](../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md)。

