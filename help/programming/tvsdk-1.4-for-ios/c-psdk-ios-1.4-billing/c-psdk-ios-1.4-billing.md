---
description: 為了迎合只想支付所用費用（而非固定費率，不論實際用途）的客戶，Adobe會收集使用量度，並使用這些度量來決定向客戶收取的費用。
seo-description: 為了迎合只想支付所用費用（而非固定費率，不論實際用途）的客戶，Adobe會收集使用量度，並使用這些度量來決定向客戶收取的費用。
seo-title: 帳單量度
title: 帳單量度
uuid: 658ffbcd-dedc-464c-8ec7-aa3bdfcb1512
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 帳單量度 {#billing-metrics}

為了迎合只想支付所用費用（而非固定費率，不論實際用途）的客戶，Adobe會收集使用量度，並使用這些度量來決定向客戶收取的費用。

每當播放器產生串流開始事件時，TVSDK就會定期傳送HTTP訊息至Adobe的帳單系統。 標準VOD、專業VOD（啟用中間卷廣告）和即時內容的時段稱為計費時段。 每種內容類型的預設持續時間為30分鐘，但您與Adobe的合約會決定實際值。

這些消息包含以下資訊：

* 內容類型（即時、線性或VOD）
* 內容URL
* 是否啟用廣告
* 是否啟用中轉廣告（僅限VOD）
* 流是否受DRM保護
* TVSDK版本與平台

Adobe會預先設定此安排，但如果您想要變更安排，請與您的Adobe啟用代表合作。

若要監控TVSDK傳送給Adobe的統計資料，請從您的Adobe啟用代表取得URL，並使用網路擷取工具（例如Charles）來查看資料。

## 設定帳單量度 {#configure-billing-metrics}

如果您使用預設設定，您就不需要執行其他動作來啟用或設定帳單。 如果您從Adobe啟用代表取得不同的設定參數，請使用PTBillingMetricsConfiguration類別，在初始化媒體播放器之前先設定這些參數。

大部分客戶應使用預設設定。

>[!IMPORTANT]
>
>您設定的組態在媒體播放器的使用期間仍有效。 初始化媒體播放器後，便無法變更設定。

若要設定帳單量度：

1. 輸入以下代碼範例。

   ```
   PTBillingMetricsConfiguration *billingConfig = [[[PTBillingMetricsConfiguration alloc] init] autorelease]; 
   billingConfig.enabled = YES; 
   billingConfig.stdVODBillableDurationMinutes = 60.0; 
   billingConfig.proVODBillableDurationMinutes = 30.0; 
   billingConfig.liveBillableDurationMinutes = 15.0; 
   
   // metadata is the PTMetadata instance set on PTMediaPlayerItem 
   [metadata setMetadata:billingConfig forKey:PTBillingMetricsConfigurationMetadataKey];
   ```

## 傳輸帳單量度 {#transmit-billing-metrics}

TVSDK以XML格式將帳單量度傳送至Adobe。

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

如果您使用網路擷取工具來監控TVSDK傳送至Adobe的統計資料，您應該會看到下列單位：

```
<request> 
     <sc_xml_ver>1.0</sc_xml_ver> 
     <reportSuiteID>ptebilling</reportSuiteID> 
     <visitorID>5536C629-5EF7-4F02-8E5D-9FA136CB3CED</visitorID> 
     <pageName>com.adobe.primetime.psdksample</pageName> 
     <timestamp>2016-11-22T18:06:30+0000</timestamp> 
     <userAgent>Mozilla/5.0 (iPad; CPU OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Mobile/13B143</userAgent> 
     <contextData> 
         <billingMetrics> 
                 <contentDuration>1799111</contentDuration> 
                 <contentURL>https%3A%2F%2Fdevimages.apple.com.edgekey.net%2Fstreaming%2Fexamples%2Fbipbop_16x9%2Fbipbop_16x9_variant.m3u8</contentURL> 
                 <contentType>vod</contentType> 
                 <midrollEnabled>true</midrollEnabled> 
                 <tvsdkVersion>1.0.211</tvsdkVersion> 
                 <platform>Mozilla/5.0 (iPad; CPU OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Mobile/13B143</platform> 
                 <publisherID>com.adobe.primetime.psdksample</publisherID> 
                 <adsEnabled>true</adsEnabled> 
                 <type>start</type> 
         </billingMetrics> 
     </contextData> 
</request>
```

布爾屬 `drmProtected`性、 `adsEnabled`和 `midrollEnabled` 僅當其為true時才顯示。