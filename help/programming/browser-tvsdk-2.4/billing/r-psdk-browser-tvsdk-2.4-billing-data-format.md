---
description: 瀏覽器TVSDK會以XML格式傳送帳單量度給Adobe。
seo-description: 瀏覽器TVSDK會以XML格式傳送帳單量度給Adobe。
seo-title: 傳輸帳單量度
title: 傳輸帳單量度
uuid: ed2638d2-7894-4840-b31a-51e48e0a3f49
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# 傳輸帳單量度{#transmit-billing-metrics}

瀏覽器TVSDK會以XML格式傳送帳單量度給Adobe。

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

如果您使用網路擷取工具來監控瀏覽器TVSDK傳送至Adobe的統計資料，您應該會看到下列單位：

```
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