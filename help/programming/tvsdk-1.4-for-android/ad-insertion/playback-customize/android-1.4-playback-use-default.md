---
description: 您可以選擇使用預設廣告行為。
title: 使用預設回放行為
exl-id: c277db2a-546e-4097-96ce-83914b726576
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# 使用預設回放行為 {#use-the-default-playback-behavior}

您可以選擇使用預設廣告行為。

要使用預設行為：

    *如果實現自己的「AdvertisingFactory」類，則為「createAdPolicySelector」返回空值。
    
    *如果您沒有「AdvertisingFactory」類的自定義實現，則TVSDK使用預設廣告策略選擇器。
