---
description: 當TVSDK在廣告伺服器回應中遇到中斷的VMAP時，會派單1109(NETWORK_AD_URL_FAILED)錯誤。
keywords: 1109;NETWORK_AD_URL_FAILED;broken VMAP
seo-description: 當TVSDK在廣告伺服器回應中遇到中斷的VMAP時，會派單1109(NETWORK_AD_URL_FAILED)錯誤。
seo-title: 中斷的VMAP的客戶端錯誤處理
title: 中斷的VMAP的客戶端錯誤處理
uuid: ab2c567d-d945-4ebe-b65a-c1f13518a576
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 中斷的VMAP的客戶端錯誤處理 {#client-error-handling-for-broken-vmap}

當TVSDK在廣告伺服器回應中遇到中斷的VMAP時，會派單1109(NETWORK_AD_URL_FAILED)錯誤。

視廣告伺服器回應的性質，以及您的廣告載入設定而定，當TVSDK在廣告伺服器回應中遇到中斷的VMAP時，您的播放器可能會收到不同數目的1109錯誤。

讓我們考慮廣告伺服器回應指向VMAP XML的案例。 假設廣告伺服器回應有四個可用廣告槽，每個插槽指向相同的VMAP。 最後，假設此VMAP已中斷。

在此案例中，如果啟用([Enable lazy ad resoling](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/t-enable-lazy-ad-resolving.md))懶惰廣告解析，TVSDK會派出兩個1109錯誤（不是預期的錯誤）:在時間軸上的每個剖析傳遞過程中都會傳送一個錯誤。 這是因為啟用延遲廣告解析時，TVSDK會以2遍解析廣告：第一個傳遞會發生在前段廣告的內容播放開始之前，而第二個傳遞會發生在播放開始後，中段廣告和後段廣告。

>[!NOTE]
>
>在此案例中，如果您停用延遲廣告解析，TVSDK只會觸發一個1109錯誤（僅一個剖析通過）。