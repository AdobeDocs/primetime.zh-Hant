---
description: 某些協力廠商廣告（或創意素材）無法銜接至HTTP即時串流(HLS)內容串流，因為其視訊格式與HLS不相容。 Primetime廣告插入和TVSDK可選擇將不相容的廣告重新封裝至相容的M3U8視訊。
title: 使用Adobe創意重新封裝服務重新封裝不相容的廣告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# 使用Adobe創意重新封裝服務重新封裝不相容的廣告{#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

某些協力廠商廣告（或創意素材）無法銜接至HTTP即時串流(HLS)內容串流，因為其視訊格式與HLS不相容。 Primetime廣告插入和TVSDK可選擇將不相容的廣告重新封裝至相容的M3U8視訊。

來自不同第三方（例如代理商廣告伺服器、您的庫存合作夥伴或廣告網路）的廣告通常以不相容的格式提供，例如漸進式下載MP4。

當TVSDK第一次遇到不相容的廣告時，播放器會忽略廣告，並向創意重新封裝服務(CRS)發出請求，以將廣告重新封裝為相容格式。 CRS會嘗試產生廣告的多位元速率M3U8轉譯，並將這些轉譯儲存在Primetime內容傳送網路(CDN)上。 下次TVSDK收到指向該廣告的廣告回應時，播放器會從CDN使用HLS相容的M3U8版本。

若要啟用此選用功能，請連絡您的Adobe代表。

如需CRS的詳細資訊，請參閱[創意封裝服務(CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf)。

## CRS廣告傳送{#section_900FDDA5454143718F1EB4C9732C8E1C}的多個CDN支援

雖然預設的Creative重新封裝服務(CRS)藍本是使用一個內容資料網路(CDN)，但您可以在多個CDN上部署CRS資產。

您可基於下列原因使用多個CDN:

* 需要針對大型檢視事件放大顯示。
* 將CRS資產的CDN來源與主內容的CDN來源相符的需求。

您可以使用TVSDK URL轉換器API來轉換CRS提供的預設URL。

以下是TVSDK中新增的API:

* `PTURLTransformer` 說明轉換TVSDK要求的CRS和URL所需方法的通訊協定。應用程式可實作此通訊協定，並提供所需方法的實作。

* `PTDefaultURLTransformer` 在TVSDK中建立並實作通訊協定的預設URL轉換器 `PTURLTransformer` 例項。應用程式可覆寫此類別或新增貼文URL轉換處理常式。 當應用程式要在套用預設轉換後變更URL請求時，這個處理常式很有用。

* `PTNetworkConfiguration setURLTransformer:defaultTransformer` 在元資料實例上提供的setter方 `PTNetworkConfiguration` 法，用於設定實 `PTURLTransformer` 現。

>[!IMPORTANT]
>
>您的應用程式實作必須檢查`PTURLTransformerInputType`列舉，並且只針對CRS檢查類型`PTURLTransformerInputTypeCRSCreative`的轉換URL。

下列程式碼範例說明應用程式如何將預設主機元件變更為不同的字串（例如`cdn.mycrsdomain.com`）:

```
// The sample code below uses Non-ARC code 
PTNetworkConfiguration *networkConfiguration = [[[PTNetworkConfiguration alloc] init] autorelease]; 
   
PTDefaultURLTransformer *defaultTransformer = [[[PTDefaultURLTransformer alloc] init] autorelease]; 
    [defaultTransformer addPostURLTransformHandler:^NSString *(NSString *url, PTURLTransformerInputType type) { 
        if (type == PTURLTransformerInputTypeCRSCreative) { 
            return [url stringByReplacingOccurrencesOfString:[NSURL URLWithString:url].host  
              withString:@"cdn.mycrsdomain.com"]; 
        } 
            return url; 
    }]; 
  
[networkConfiguration setURLTransformer:defaultTransformer]; 
   
// metadata is the PTMetadata instance set on a PTMediaPlayerItem instance. 
[metadata setMetadata:[self getNetworkConfiguration] forKey:PTNetworkConfigurationMetadataKey];
```

