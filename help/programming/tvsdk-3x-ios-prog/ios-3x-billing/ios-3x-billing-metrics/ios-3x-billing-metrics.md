---
description: 為了適應那些只想按使用付費而不是按固定費率付費的客戶，Adobe收集使用量度，並使用這些度量來確定向客戶收取的費用。
title: 計費使用情況度量
exl-id: 8b76d8ea-c8d6-427b-886a-4ae8764bd47a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# 計費度量 {#billing-metrics}

為了適應那些只想按使用付費而不是按固定費率付費的客戶，Adobe收集使用量度，並使用這些度量來確定向客戶收取的費用。

每次播放器生成流啟動事件時，TVSDK開始定期向Adobe的計費系統發送HTTP消息。 該週期稱為可計費持續時間，對於標準VOD、pro VOD（啟用中間廣告）和即時內容可以不同。 每種內容類型的預設持續時間為30分鐘，但您與Adobe的合同將確定實際值。

這些消息包含以下資訊：

* 內容類型（即時、線性或VOD）
* 內容URL
* 是否啟用廣告
* 是否啟用中間卷廣告（僅VOD）
* 流是否受DRM保護
* TVSDK版本和平台

Adobe預先配置此安排，但如果要更改此安排，請與您的Adobe支援代表合作。

要監視TVSDK發送到Adobe的統計資訊，請從Adobe啟用代表獲取URL，然後使用網路捕獲工具（例如Charles）查看資料。

## 配置計費度量 {#configure-billing-metrics}

如果使用預設配置，則無需執行其他任何操作即可啟用或配置計費。 如果您從Adobe啟用代表處獲得了不同的配置參數，請在初始化媒體播放器之前使用PTBillingMetricsConfiguration類設定這些參數。

大多數客戶應使用預設配置。

>[!IMPORTANT]
>
>您設定的配置在媒體播放器的生命週期中仍然有效。 初始化媒體播放器後，無法更改配置。

要配置計費度量，請執行以下操作：

輸入以下代碼樣例。

```
PTBillingMetricsConfiguration *billingConfig = [[[PTBillingMetricsConfiguration alloc] init] autorelease]; 
billingConfig.enabled = YES; 
billingConfig.stdVODBillableDurationMinutes = 60.0; 
billingConfig.proVODBillableDurationMinutes = 30.0; 
billingConfig.liveBillableDurationMinutes = 15.0; 
                
// metadata is the PTMetadata instance set on PTMediaPlayerItem 
[metadata setMetadata:billingConfig forKey:PTBillingMetricsConfigurationMetadataKey];
```

## 傳輸計費度量 {#transmit-billing-metrics}

TVSDK以XML格式向Adobe發送計費度量。

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

如果使用網路捕獲工具監視TVSDK傳輸到Adobe的統計資訊，則應看到以下單元：

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

布爾屬性 `drmProtected`。 `adsEnabled`, `midrollEnabled` 只有在它們為真時才顯示。
