---
description: 本節介紹不同版本的Flash Player和TVSDK所提供的功能。
title: RBOP客戶端支援
exl-id: 1120587e-45cf-45cc-8b41-1886ab2ed2a4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# RBOP客戶端支援 {#rbop-client-support}

本節介紹不同版本的Flash Player和TVSDK所提供的功能。

**錯誤派單**  — 當正在播放的內容的解析度超過DRM策略中定義的設備配置允許的解析度時，下面列出的TVSDK平台會調度DRM運行時錯誤：

* Flash Player版本18至20
* Android — 版本
* iOS — 版本

>[!NOTE]
>
>* 所有Flash和移動平台都支援錯誤派單，但只有上面列出的TVSDK客戶端處理與RBOP相關的錯誤。
>* RBOP相關 [DRM客戶端錯誤](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages):
   >    * **3371**  — 基於許可證中的輸出保護約束的解決方案格式不正確。
   >    * **3372**  — 內容的解析度大於輸出保護約束中指定的最大解析度。 （如果有人試圖注入用於其他設備的內容，則可能會發生這種情況。）
   >    * **3373**  — 內容的解析度大於當前活動的輸出保護約束所指定的解析度。 （這意味著我們將不得不降級。）
>


**自動縮放**  — 用於縮放的技術因平台和Flash Player版本而異：

* Flash Player版本21:支援RBOP和自動縮放（智慧比特率切換）
* Windows上的Firefox版本38及更高版本（帶Access CDM）:Adobe自動將較高比特率流降級到較低比特率流（而不是下載較低等級流）。

>[!NOTE]
>
>這些平台自動縮放視頻，並以低於或等於DRM策略指定的解析度顯示內容。 使用此功能，只要有符合DRM策略限制的可用流，內容將始終回放到客戶端。

**舊式輸出保護**  — 使用版本18之前Flash Player的客戶端只能處理舊版OP限制。 Flash Player版本18及更高版本的客戶端可以處理舊版或RBOP限制。 如果設定RBOP限制，還應為較舊的客戶端設定舊OP限制。 對於支援RBOP的客戶，RBOP限制要勝過傳統OP限制。
