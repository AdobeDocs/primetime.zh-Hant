---
description: 當TVSDK在廣告伺服器響應中遇到損壞的VMAP時，它會派單1109(NETWORK_AD_URL_FAILED)錯誤。
keywords: 1109;NETWORK_AD_URL_FAILED；損壞的VMAP
title: 中斷的VMAP的客戶端錯誤處理
exl-id: e0ca36e7-ac88-44b8-bbdd-bcf29467417b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 中斷的VMAP的客戶端錯誤處理 {#client-error-handling-for-broken-vmap}

當TVSDK在廣告伺服器響應中遇到損壞的VMAP時，它會派單1109(NETWORK_AD_URL_FAILED)錯誤。

根據廣告伺服器響應的性質和廣告載入設定，當TVSDK在廣告伺服器響應中遇到損壞的VMAP時，播放器可能收到1109個錯誤。

讓我們考慮廣告伺服器響應指向VMAP XML的情形。 還假設廣告伺服器響應有四個可用的廣告插槽，每個插槽指向同一VMAP。 最後，假設此VMAP已損壞。

在此方案中，如果啟用了懶惰和解析([啟用延遲和解析](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/t-enable-lazy-ad-resolving.md)),TVSDK將發送兩個1109錯誤（不是預期的錯誤）:在時間線上的每個分析傳遞上都會調度一個錯誤。 這是因為啟用了懶惰廣告解析後，TVSDK將分兩步分析廣告：第一遍就在開始播放預卷廣告的內容之前進行，第二遍則在播放開始後進行，對於中卷廣告和後卷廣告。

>[!NOTE]
>
>在此方案中，如果禁用懶惰和解析，TVSDK將僅觸發一個1109錯誤（僅一個分析通道）。
