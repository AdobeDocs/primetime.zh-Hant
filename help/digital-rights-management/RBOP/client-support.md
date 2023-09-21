---
description: 本節說明不同版本的Flash Player和TVSDK可用的功能。
title: RBOP使用者端支援
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# RBOP使用者端支援 {#rbop-client-support}

本節說明不同版本的Flash Player和TVSDK可用的功能。

**錯誤分派**  — 當播放內容的解析度超過DRM原則中定義的裝置組態允許的解析度時，下列的TVSDK平台會傳送DRM執行階段錯誤：

* Flash Player版本18到20
* Android — 版本
* iOS — 版本

>[!NOTE]
>
>* 所有Flash和行動平台都支援錯誤分派，但只有上述的TVSDK使用者端會處理與RBOP相關的錯誤。
>* RBOP相關 [DRM使用者端錯誤](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)：
>    * **3371**  — 根據授權中的輸出保護限制，解析格式錯誤。
>    * **3372**  — 內容的解析度大於輸出保護限制中指定的最大解析度。 （如果有人嘗試插入要用於其他裝置的內容，就可能發生這種情況。）
>    * **3373**  — 內容的解析度大於目前作用中的輸出保護限制所指定的解析度。 （這表示我們必須降級。）
>

**自動縮減比例**  — 用於縮小規模的技巧因平台和Flash Player版本而異：

* Flash Player版本21：支援具有自動縮減縮放（智慧型位元速率切換）的RBOP
* Windows上的Firefox 38版和更新版本（含Access CDM）：Adobe會自動將較高的位元速率資料流降級為較低的資料流（與下載較低等級的資料流相反）。

>[!NOTE]
>
>這些平台會自動縮小視訊，並以低於或等於DRM政策所指定的解析度來顯示內容。 使用此功能，只要有符合DRM原則限制的可用資料流，內容就會一律播放給使用者端。

**舊版輸出保護**  — 使用18版之前Flash Player的使用者端只能處理舊版OP限制。 具有Flash Player版本18及更新版本的使用者端可以處理舊版或RBOP限制。 如果您正在設定RBOP限制，您也應該為舊版使用者端設定舊版OP限制。 對於支援RBOP的客戶，RBOP限制會取代舊版OP限制。
