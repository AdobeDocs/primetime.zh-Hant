---
title: 資訊清單重寫與廣告擷取規則
description: 資訊清單重寫與廣告擷取規則
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# 資訊清單重寫與廣告擷取規則 {#manifest-rewriting}

PrimetimeAd Insertion能夠使用簡單的搜尋/取代規則重新寫入片段及擷取資產。  這可用來將https向下轉換為http請求，進而透過移除TLS交換來提高效能。  這也可以用來從相同的CDN傳送廣告資產和CDN資產。

規則定義為規則運算式搜尋/取代，可用來在傳送之前以及插入資訊清單中之後轉換URL。

此範例規則會將所有廣告請求從https向下轉換為domain.com http。

```
find: "https://domain.com/(.*)"
replace: "http://domain.com/$1"
```

下列規則將使用內容CDN來傳遞位於Adobe廣告儲存CDN上的廣告。

```
find: "https?://primetime-a.akamaihd.net/(.*)"
replace: "http://mycdn.com/ad-mapping-pathname/$1"
```

您可以修改規則名稱並啟用/停用規則 `ptprotoswitch` BootstrapAPI中的引數，以逗號分隔要執行的規則清單。  例如，這兩個規則都可透過設定來執行 `ptprotoswitch=adfetch_rule1,adfetch_rule2`：

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

請連絡您的技術支援人員，為您的帳戶建立/啟用這些規則。
