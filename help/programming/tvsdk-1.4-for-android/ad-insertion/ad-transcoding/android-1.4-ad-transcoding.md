---
description: 部分協力廠商廣告（或創意）無法結合至HTTP即時資料流(HLS)內容串流，因為其視訊格式與HLS不相容。 Primetime廣告插入和TVSDK可選擇嘗試將不相容的廣告重新封裝為相容的M3U8影片。
title: 使用Adobe Creative重新封裝服務重新封裝不相容的廣告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 使用Adobe Creative重新封裝服務重新封裝不相容的廣告 {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

部分協力廠商廣告（或創意）無法結合至HTTP即時資料流(HLS)內容串流，因為其視訊格式與HLS不相容。 Primetime廣告插入和TVSDK可選擇嘗試將不相容的廣告重新封裝為相容的M3U8影片。

由不同協力廠商提供的廣告，例如代理商廣告伺服器、您的詳細目錄合作夥伴或廣告網路，通常會以不相容的格式傳送，例如漸進式下載MP4。

當TVSDK首次遇到不相容的廣告時，播放器會忽略該廣告並向Creative重新封裝服務(CRS) （這是Primetime廣告插入後端的一部分）發出請求，以將廣告重新封裝為相容格式。 CRS會嘗試產生廣告的多位元速率M3U8轉譯，並將這些轉譯儲存至Primetime內容傳遞網路(CDN)。 下次TVSDK收到指向該廣告的廣告回應時，播放器會使用來自CDN的HLS相容M3U8版本。

若要啟用此選用功能，請聯絡您的Adobe代表。

如需CRS的詳細資訊，請參閱 [Creative Packaging Service (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf).

## CRS廣告傳遞的多重CDN支援{#multiple-cdn-support-for-crs-ad-delivery}

雖然預設的Creative Repackaging Service (CRS)情境是使用單一內容資料網路(CDN)，但您可以在多個CDN上部署CRS資產。

基於以下原因，您可以使用多個CDN：

* 需要針對大型檢視事件進行擴充。
* 必須符合CRS資產的CDN來源與主要內容的CDN來源。

您可以使用TVSDK URL Transformer API來轉換CRS提供的預設URL。

以下是TVSDK中的API新增專案：

* `URLTransformer` 此介面說明轉換TVSDK所要求的CRS和URL所需的方法。 應用程式可以實作此介面並提供所需方法的實作。

* `DefaultURLTransformer` 在TVSDK中建立且實作的預設URL轉換器例項 `URLTransformer` 介面。 應用程式可以覆寫此類別或新增貼文URL轉換處理常式。 當應用程式要在套用預設轉換後變更URL要求時，此處理常式會很有用。

* `NetworkConfiguration.setURLTransformer` 提供於 `NetworkConfiguration` 中繼資料例項以設定 `URLTransformer` 實作。

>[!IMPORTANT]
>
>您的應用程式實作必須檢查 `URLTransformerInputType` 分項清單且只轉換型別的URL `URLTransformerInputType.CRSCreative` 用於CRS。

下列程式碼範例說明應用程式如何將預設主機元件變更為不同的字串(例如 `cdn.mycrsdomain.com`)：

```java
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
DefaultURLTransformer urlTransformer = new DefaultURLTransformer(); 
urlTransformer.addPostURLTransformHandler(new DefaultURLTransformer.URLTransformHandler() { 
    @Override 
    public String call(String url, URLTransformerInputType type) { 
        if (type == URLTransformerInputType.CRSCreative) { 
            try { 
                return url.replaceAll(new java.net.URI(url).getHost(), "cdn.mycrsdomain.com"); 
            } catch (URISyntaxException e) { 
            } 
        } 
        return url; 
    } 
}); 
   
networkConfiguration.setURLTransformer(urlTransformer); 
   
// metadata is the Metadata instance set on a MediaResource instance. 
metadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(), networkConfiguration);
```
