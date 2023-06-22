---
description: 本節說明不同Flash Player版本和TVSDK版本的功能。
title: RBOP使用者端支援
exl-id: 1120587e-45cf-45cc-8b41-1886ab2ed2a4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# RBOP使用者端支援 {#rbop-client-support}

本節說明不同Flash Player版本和TVSDK版本的功能。

**錯誤分派**  — 當正在播放的內容的解析度超過DRM原則中定義的裝置設定所允許的解析度時，下列的TVSDK平台會傳送DRM執行階段錯誤：

* Flash Player版本18到20
* Android — 版本
* iOS — 版本

>[!NOTE]
>
>* 所有Flash和行動平台都支援錯誤分派，但只有上述的TVSDK使用者端會處理與RBOP相關的錯誤。
>* RBOP相關 [DRM使用者端錯誤](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)：
   >    * **3371**  — 根據授權中的輸出保護限制，解析格式錯誤。
   >    * **3372**  — 內容的解析度大於輸出保護限制中指定的最大解析度。 （如果有人嘗試插入適用於其他裝置的內容，就可能發生這種情況。）
   >    * **3373**  — 內容的解析度大於目前作用中的輸出保護限制所指定的解析度。 （這表示我們必須降級。）
>


**自動縮減縮放**  — 用於縮減規模的技術因平台和Flash Player版本而異：

* Flash Player版本21：支援具有自動縮減縮放（智慧型位元速率切換）的RBOP
* Windows上的Firefox 38版和更新版本（含Access CDM）：Adobe會自動將較高位元速率資料流降級為較低位元速率資料流（與下載較低等級的資料流相反）。

>[!NOTE]
>
>這些平台會自動縮小視訊規模，並以低於或等於DRM原則所指定的解析度來顯示內容。 使用此功能時，只要有符合DRM原則限制的可用資料流，內容就會一律播放給使用者端。

**舊版輸出保護**  — 使用18版之前Flash Player的使用者端只能處理舊版OP限制。 具有Flash Player版本18及更新版本的使用者端可以處理舊版或RBOP限制。 如果您設定RBOP限制，您也應該為舊版使用者端設定舊版OP限制。 對於支援RBOP的客戶，RBOP限制會取代舊版OP限制。
