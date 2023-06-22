---
title: 同步化需求
description: 同步化需求
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# 同步化需求{#requirements-for-synchronization}

指定使用者端與伺服器同步狀態的頻率。 如果使用者端已獲得頻外授權（未連絡授權伺服器），則使用規則可指定使用者端必須傳送同步訊息給伺服器，以便同步使用者端的安全時間並向伺服器報告使用者端狀態。

使用下列引數定義同步化行為：

* 開始間隔 — 指定在上次成功同步化之後，要等待多久才能開始另一個同步化要求。
* 硬停止間隔 — （選擇性）。 如果在指定的時間內未發生成功的同步處理，則不允許播放。
* 強制同步處理機率 — （選擇性）。 使用者端在下次開始間隔之前傳送同步化訊息的可能性。

>[!NOTE]
>
>Adobe Access使用者端3.0版及更新版本支援此使用規則。 舊版使用者端的行為取決於授權伺服器支援的最低使用者端版本。 請參閱， [最低使用者端版本](../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).

