---
description: 本節說明不同版本的Flash Player和TVSDK所提供的功能。
title: RBOP客戶端支援
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# RBOP客戶端支援{#rbop-client-support}

本節說明不同版本的Flash Player和TVSDK所提供的功能。

**錯誤派單** -當播放內容的解析度超過DRM原則中定義之裝置組態所允許的解析度時，下列TVSDK平台會派單DRM執行階段錯誤：

* Flash Player第18至20版
* Android —— 版本
* iOS —— 版本

>[!NOTE]
>
>* 所有Flash和行動平台都支援錯誤派單，但只有上述TVSDK用戶端會處理與RBOP相關的錯誤。
>* 與RBOP相關的[DRM客戶端錯誤](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages):
   >    * **3371**  —— 基於許可證中輸出保護約束的格式錯誤的解析。
   >    * **3372**  —— 內容的解析度大於輸出保護約束中指定的最大解析度。（如果有人嘗試插入其他裝置專用的內容，就會發生這種情況）。
   >    * **3373**  —— 內容的解析度大於目前有效的輸出保護限制所指定的解析度。（這意味著我們必須降級。）

>



**自動縮放** -用於縮放的技術因平台和Flash Player版本而異：

* Flash Player第21版：支援RBOP的自動縮放功能（智慧位元速率切換）
* Windows版Firefox 38及更新版本（含Access CDM）:Adobe會自動將較高位元速率的串流降級為較低的串流（而非下載較低等級的串流）。

>[!NOTE]
>
>這些平台會自動縮放視訊，並以低於或等於DRM原則所指定解析度的解析度顯示內容。 使用此功能，只要有符合DRM原則限制的可用串流，內容就會一律播放回用戶端。

**舊版輸出保護** -使用18版之前Flash Player的客戶端只能處理舊版OP限制。具有Flash Player版本18及更新版本的客戶端可處理舊版或RBOP限制。 如果要設定RBOP限制，則還應為舊客戶機設定舊OP限制。 對於支援RBOP的客戶，RBOP限制比舊有的OP限制更勝一籌。
