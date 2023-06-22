---
description: 部分協力廠商廣告（或創意）無法結合至HTTP即時串流(HLS)內容資料流，因為其視訊格式與HLS不相容。 Primetime廣告插入和TVSDK可選擇嘗試將不相容的廣告重新封裝成相容的M3U8影片。
title: 使用AdobeCreative重新封裝服務重新封裝不相容的廣告
exl-id: 86a8bd94-4de0-4aba-b6ee-4e0e1ee864c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# 使用AdobeCreative重新封裝服務重新封裝不相容的廣告 {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

部分協力廠商廣告（或創意）無法結合至HTTP即時串流(HLS)內容資料流，因為其視訊格式與HLS不相容。 Primetime廣告插入和TVSDK可選擇嘗試將不相容的廣告重新封裝成相容的M3U8影片。

代理廣告伺服器、詳細目錄合作夥伴或廣告網路等各種協力廠商提供的廣告，通常會以不相容的格式傳送，例如漸進式下載MP4。

當TVSDK首次遇到不相容的廣告時，播放器會忽略該廣告，並向創意重新封裝服務(CRS) （Primetime廣告插入後端的一部分）發出請求，以將廣告重新封裝為相容的格式。 CRS會嘗試產生廣告的多位元速率M3U8轉譯，並將這些轉譯儲存在Primetime內容傳遞網路(CDN)上。 下次TVSDK收到指向該廣告的廣告回應時，播放器會使用來自CDN的HLS相容M3U8版本。

若要啟用此選擇性功能，請聯絡您的Adobe代表。

## CRS廣告傳遞的多重CDN支援 {#section_900FDDA5454143718F1EB4C9732C8E1C}

雖然預設的Creative Repackaging Service (CRS)情境是使用一個Content Data Network (CDN)，但您可以在多個CDN上部署CRS資產。

基於以下原因，您可以使用多個CDN：

* 針對大型檢視事件進行擴充的需求。
* 必須符合CRS資產的CDN來源與主要內容的CDN來源。

您可以使用TVSDK URL Transformer API轉換CRS提供的預設URL。

以下是TVSDK中的API新增專案：

* `PTURLTransformer` 此通訊協定說明轉換TVSDK所要求的CRS和URL所需的方法。 應用程式可以實作此通訊協定，並提供所需方法的實作。

* `PTDefaultURLTransformer` 在TVSDK中建立且實作的預設URL轉換器例項 `PTURLTransformer` 通訊協定。 應用程式可以覆寫此類別或新增貼文URL轉換處理常式。 當應用程式想要在套用預設轉換後變更URL要求時，此處理常式會很有用。

* `PTNetworkConfiguration setURLTransformer:defaultTransformer` 提供於 `PTNetworkConfiguration` 中繼資料例項，以設定 `PTURLTransformer` 實作。

>[!IMPORTANT]
>
>您的應用程式實作必須檢查 `PTURLTransformerInputType` 分項清單和僅轉換型別的URL `PTURLTransformerInputTypeCRSCreative` 適用於CRS。

下列程式碼範例說明應用程式如何將預設主機元件變更為不同的字串(例如 `cdn.mycrsdomain.com`)：

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
