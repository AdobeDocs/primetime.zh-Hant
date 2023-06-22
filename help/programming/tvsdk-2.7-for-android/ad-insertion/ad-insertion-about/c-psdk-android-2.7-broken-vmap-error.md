---
description: 當TVSDK在廣告伺服器回應中遇到VMAP中斷時，它會傳送1109 (NETWORK_AD_URL_FAILED)錯誤。
keywords: 1109；NETWORK_AD_URL_FAILED；損毀VMAP
title: 中斷VMAP的使用者端錯誤處理
exl-id: 268307a9-b72e-45fa-84f2-a8e7d969e2ba
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 中斷VMAP的使用者端錯誤處理 {#client-error-handling-for-broken-vmap}

當TVSDK在廣告伺服器回應中遇到VMAP中斷時，它會傳送1109 (NETWORK_AD_URL_FAILED)錯誤。

根據廣告伺服器回應的性質以及廣告載入設定，當TVSDK在廣告伺服器回應中遇到VMAP中斷時，您的播放器可能會收到不同的1109錯誤數目。

讓我們考慮廣告伺服器回應指向VMAP XML的案例。 也假設廣告伺服器回應有四個可用的廣告槽，每個槽都指向相同的VMAP。 最後，假設此VMAP已中斷。

在此案例中，如果已啟用延遲廣告解析( [啟用延遲廣告解析](../../../tvsdk-2.7-for-android/ad-insertion/c-psdk-android-2.7-lazy-ad-resolving/t-psdk-android-2.7-enable-lazy-ad-resolving.md))，TVSDK將會傳送兩個1109錯誤（而不是預期的一個）：在時間軸的每個剖析階段都會傳送一個錯誤。 這是因為啟用延遲廣告解析時，TVSDK會分兩階段剖析廣告：第一階段發生在前段廣告的內容播放開始之前，而第二階段發生在播放開始之後（中段和後段廣告）。

>[!NOTE]
>
>在此案例中，如果您停用延遲廣告解析，TVSDK將只會引發一個1109錯誤（只有一個剖析階段）。
