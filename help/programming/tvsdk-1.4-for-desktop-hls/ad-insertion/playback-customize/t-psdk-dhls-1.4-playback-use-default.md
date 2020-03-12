---
description: 您可以選擇使用預設廣告行為。
seo-description: 您可以選擇使用預設廣告行為。
seo-title: 使用預設播放行為
title: 使用預設播放行為
uuid: 7139384c-167a-4cab-816a-c02fb723a5cb
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 使用預設播放行為{#use-the-default-playback-behavior}

您可以選擇使用預設廣告行為。

要使用預設行為：

    *如果您實作自己的「ContentFactory」類別，請在「doRetrieveAdPolicySelector」實作中傳回新的「DefaultAdPolicySelector」例項。
    
    &quot;公
    用類CustomContentFactory擴展了ContentFactory {
    
    //...
    /// your custom code for advertising classes
    //...
    
    /**
    @inherit*/
    override
    functiondoRetrieveAdPolicySelector(item:MediaEtimeSelector):AdPolicySelector
    return new DefaultAdPolicyPolicyPlecy(item)(**}imeritem*}item*}itoredore
    Rido
    
    
    
    
    funidoRidoReRetedo preReteRidoRetedo函式doReteRidoRido deRetreReteAdReRetriveAdAdAdPlectiodoAdAdPlectioPlectiveAdAdPlecoPlectoAd「類別，TVSDK使用「DefaultAdPolicySelector」。