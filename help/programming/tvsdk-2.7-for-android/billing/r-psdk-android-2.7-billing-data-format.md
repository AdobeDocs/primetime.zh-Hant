---
description: TVSDK以XML格式向Adobe發送計費度量。
title: 傳輸計費度量
exl-id: 5f42d032-cd2c-4e5e-8960-db555ba75626
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---

# 傳輸計費度量 {#transmit-billing-metrics}

TVSDK以XML格式向Adobe發送計費度量。

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

如果使用網路捕獲工具監視TVSDK傳輸到Adobe的統計資訊，則應看到以下單元：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<request>
    <sc_xml_ver>1.0</sc_xml_ver>
    <reportSuiteID>primesample2</reportSuiteID>
    <visitorID>947310128cb56f41</visitorID>
    <pageURL>https://. . ..m3u8</pageURL>
    <timestamp>2016-4-7T10:1:4</timestamp>
    <contextData>
        <billingMetrics>
            <publisherID>com.adobe.primetime.reference.PrimetimeReference</publisherID>
            <contentType>vod</contentType>
            <adsEnabled>true</adsEnabled>
            <midrollEnabled>true</midrollEnabled>
            <platform>Mac OSX 10.11.5</platform>
            <tvsdkVersion>2,4,0,1559</tvsdkVersion>
            <contentURL>https://. . ..m3u8</contentURL>
        </billingMetrics>
    </contextData>
</request>
```

布爾屬性 `drmProtected`。 `adsEnabled`, `midrollEnabled` 只有在它們為真時才顯示。
