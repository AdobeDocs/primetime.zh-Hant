---
title: 資訊清單重寫與廣告擷取規則
description: 資訊清單重寫與廣告擷取規則
exl-id: 3750abc1-da60-4faf-ba85-37914f33641f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# 資訊清單重寫與廣告擷取規則 {#manifest-rewriting}

PrimetimeAd Insertion能夠使用簡單的搜尋/取代規則重新寫入片段及擷取資產。  這可用來將https向下轉換為http請求，進而透過移除TLS握手來提升效能。  這也可以用來傳遞來自相同CDN的廣告資產和CDN資產。

規則定義為規則運算式搜尋/取代，可用於在傳送前以及插入資訊清單中後轉換url。

domain.com此範例規則會將所有廣告請求從https下載轉換為http。

```
find: "https://domain.com/(.*)"
replace: "http://domain.com/$1"
```

下列規則將使用內容CDN來傳遞位於Adobe廣告儲存CDN上的廣告。

```
find: "https?://primetime-a.akamaihd.net/(.*)"
replace: "http://mycdn.com/ad-mapping-pathname/$1"
```

您可以修改「 」，以命名和啟用/停用規則。 `ptprotoswitch` BootstrapAPI中的引數，以逗號分隔要執行的規則清單。  例如，這兩個規則都可透過設定來執行 `ptprotoswitch=adfetch_rule1,adfetch_rule2`：

```
<ruleSet>
    <rule name="rule1">
        <find><![CDATA[...]]></find>
        <replace><![CDATA[...]]></replace>
    </rule>
    <rule name="rule2">
        <find><![CDATA[...]]></find>
        <replace><![CDATA[...]]></replace>
    </rule>
</ruleSet>
```

請聯絡您的技術支援人員，為您的帳戶建立/啟用這些規則。
