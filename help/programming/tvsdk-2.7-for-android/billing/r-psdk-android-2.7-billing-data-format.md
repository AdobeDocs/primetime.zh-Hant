---
description: TVSDK以XML格式將帳單量度傳送至Adobe。
seo-description: TVSDK以XML格式將帳單量度傳送至Adobe。
seo-title: 傳輸帳單量度
title: 傳輸帳單量度
uuid: f4a7f50e-f457-434e-bf26-1e06cb15a038
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# 傳送帳單量度{#transmit-billing-metrics}

TVSDK以XML格式將帳單量度傳送至Adobe。

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

如果您使用網路擷取工具來監控TVSDK傳送至Adobe的統計資料，您應該會看到下列單位：

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

布爾屬性`drmProtected`、`adsEnabled`和`midrollEnabled`只有在屬性為true時才會顯示。