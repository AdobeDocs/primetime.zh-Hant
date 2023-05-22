---
description: 某些第三方廣告（或創意）無法縫合到HTTP即時流(HLS)內容流中，因為其視頻格式與HLS不相容。 黃金時段廣告插入和TVSDK可以選擇嘗試將不相容的廣告重新打包到相容的M3U8視頻中。
title: 使用Adobe創意重新打包服務重新打包不相容的廣告
exl-id: dddc7e44-88ba-438b-aa45-ed03f436cd53
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 使用Adobe創意重新打包服務重新打包不相容的廣告 {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

某些第三方廣告（或創意）無法縫合到HTTP即時流(HLS)內容流中，因為其視頻格式與HLS不相容。 黃金時段廣告插入和TVSDK可以選擇嘗試將不相容的廣告重新打包到相容的M3U8視頻中。

來自不同第三方（如代理廣告伺服器、您的清單合作夥伴或廣告網路）的廣告通常以不相容的格式提供，如累進下載MP4。

當TVSDK第一次遇到不相容的廣告時，播放器忽略該廣告並向作為黃金時段廣告插入後端的一部分的創造性重新打包服務(CRS)發出將該廣告重新打包成相容格式的請求。 CRS嘗試生成廣告的多比特率M3U8格式副本，並將這些格式副本儲存在黃金時段內容交付網路(CDN)上。 下次TVSDK收到指向該廣告的廣告響應時，播放器使用CDN中與HLS相容的M3U8版本。

要啟用此可選功能，請與Adobe代表聯繫。

有關CRS的詳細資訊，請參見 [創意包裝服務(CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf)。

## 對CRS和交付的多個CDN支援 {#multiple-cdn-support-for-crs-ad-delivery}

雖然預設的Creative重新打包服務(CRS)方案是使用一個內容資料網路(CDN)，但您可以在多個CDN上部署CRS資產。

您可以使用多個CDN，原因如下：

* 對大型查看事件進行擴展的要求。
* 將CRS資產的CDN源與主內容的CDN源匹配的要求。

可以使用TVSDK URL轉換器API轉換CRS提供的預設URL。

以下是TVSDK中的API添加：

* `URLTransformer` 描述轉換TVSDK請求的CRS和URL所需方法的介面。 應用程式可以實現此介面並提供所需方法的實現。

* `DefaultURLTransformer` 在TVSDK中建立並實現的預設URL轉換器實例 `URLTransformer` 。 應用程式可以覆蓋此類或添加帖子URL轉換處理程式。 當應用預設轉換後，應用程式希望對URL請求進行更改時，此處理程式非常有用。

* `NetworkConfiguration.urlTransformer` 提供在 `NetworkConfiguration` 要設定的元資料實例 `URLTransformer` 執行。

>[!IMPORTANT]
>
>您的應用實現必須檢查 `URLTransformerInputType` 枚舉和僅轉換類型的URL `URLTransformerInputType.CRSCreative` CRS。

下面的代碼示例說明應用程式如何將預設主機元件更改為其他字串(例如， `cdn.mycrsdomain.com`):

```
var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   
var urlTransformer:DefaultURLTransformer = new DefaultURLTransformer(); 
urlTransformer.addPostURLTransformHandler(function (url:String, type:String) { 
    if (type == URLTransformerInputType.CRSCreative) { 
        return url.replace(URLUtil.getServerName(url), "cdn.mycrsdomain.com"); 
    } 
    return url; 
}); 
  
networkConfiguration.urlTransformer = urlTransformer; 
   
// metadata is the Metadata instance set on a MediaResource instance. 
metadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                     networkConfiguration);
```
