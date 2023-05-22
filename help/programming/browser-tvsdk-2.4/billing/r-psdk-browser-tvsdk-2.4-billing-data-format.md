---
description: 瀏覽器TVSDK以XML格式向Adobe發送計費度量。
title: 傳輸計費度量
exl-id: f6ed72be-a5a8-48f2-b518-76c710300ea7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 0%

---

# 傳輸計費度量{#transmit-billing-metrics}

瀏覽器TVSDK以XML格式向Adobe發送計費度量。

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

如果使用網路捕獲工具監視瀏覽器TVSDK傳輸到Adobe的統計資訊，您應看到以下設備：

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

布爾屬性 `drmProtected`。 `adsEnabled`, `midrollEnabled` 只有在它們為真時才顯示。
