---
description: 您可以選擇使用預設廣告行為。
title: 使用預設播放行為
exl-id: c277db2a-546e-4097-96ce-83914b726576
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# 使用預設播放行為 {#use-the-default-playback-behavior}

您可以選擇使用預設廣告行為。

若要使用預設行為：

    *如果您實作自己的「AdvertisingFactory」類別，請為「createAdPolicySelector」傳回null 。
    
    *如果您沒有「AdvertisingFactory」類別的自訂實施，TVSDK會使用預設的廣告原則選擇器。
