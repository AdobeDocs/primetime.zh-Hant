---
description: 為因應客戶只想依使用量付款，而不論實際使用量為何，Adobe會收集使用量度，並使用這些量度來決定向客戶收費的金額。
title: 計費量度
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# 計費量度 {#billing-metrics}

為因應客戶只想依使用量付款，而不論實際使用量為何，Adobe會收集使用量度，並使用這些量度來決定向客戶收費的金額。

每次播放器產生資料流開始事件時，TVSDK就會開始定期傳送HTTP訊息至Adobe的計費系統。 期間（稱為可計費期間）在標準VOD、專業VOD （啟用中段廣告）和即時內容中可能不同。 每種內容型別的預設持續時間為30分鐘，但您的Adobe合約會決定實際值。

訊息包含下列資訊：

* 內容型別（即時、線性或VOD）
* 內容URL
* 是否啟用廣告
* 是否啟用中段廣告（僅限VOD）
* 資料流是否受DRM保護
* TVSDK版本和平台

Adobe會預先設定此安排，但如果您想要變更安排，請與您的「Adobe啟用」代表合作。

若要監視TVSDK傳送至Adobe的統計資料，請向您的Adobe啟用代表取得URL，並使用網路擷取工具（例如Charles）來檢視資料。

## 設定計費量度 {#configure-billing-metrics}

如果您使用預設設定，則您不需要執行其他操作即可啟用或設定帳單。 如果您從「Adobe啟用」代表取得不同的設定引數，請在初始化媒體播放器之前使用PTBillingMetricsConfiguration類別設定這些引數。

大部分客戶應使用預設設定。

>[!IMPORTANT]
>
>您設定的設定會在媒體播放器的有效期內維持有效。 初始化媒體播放器後，便無法變更設定。

若要設定計費量度：

1. 輸入下列程式碼範例。

   ```
   PTBillingMetricsConfiguration *billingConfig = [[[PTBillingMetricsConfiguration alloc] init] autorelease]; 
   billingConfig.enabled = YES; 
   billingConfig.stdVODBillableDurationMinutes = 60.0; 
   billingConfig.proVODBillableDurationMinutes = 30.0; 
   billingConfig.liveBillableDurationMinutes = 15.0; 
   
   // metadata is the PTMetadata instance set on PTMediaPlayerItem 
   [metadata setMetadata:billingConfig forKey:PTBillingMetricsConfigurationMetadataKey];
   ```

## 傳輸計費量度 {#transmit-billing-metrics}

TVSDK會以XML格式將計費量度傳送至Adobe。

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

如果您使用網路擷取工具來監視TVSDK傳輸至Adobe的統計資料，您應該會看到如下的單位：

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

布林值屬性 `drmProtected`， `adsEnabled`、和 `midrollEnabled` 只有在為true時才出現。
