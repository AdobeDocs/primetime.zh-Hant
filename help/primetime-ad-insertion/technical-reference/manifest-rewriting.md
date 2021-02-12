---
title: 資訊清單重寫和廣告擷取規則
description: '資訊清單重寫和廣告擷取規則 '
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# 資訊清單重寫和廣告擷取規則{#manifest-rewriting}

Primetime廣告插入功能可使用簡單的搜尋／取代規則重寫片段及擷取資產。  這可用來將https向下轉換為http要求，這可移除TLS握手來提升效能。  這也可用來從相同的CDN傳送廣告資產和cdn資產。

規則定義為規則運算式搜尋／取代，可用於在傳送前以及插入資訊清單後轉換URL。

此範例規則會將所有廣告要求從https轉換為https。

```
find: "https://domain.com/(.*)"
replace: "http://domain.com/$1"
```

下列規則將使用內容CDN來傳送位於Adobe廣告儲存CDN上的廣告。

```
find: "https?://primetime-a.akamaihd.net/(.*)"
replace: "http://mycdn.com/ad-mapping-pathname/$1"
```

修改引導API中的`ptprotoswitch`參數，即可命名和啟用／停用規則，此參數是要執行的逗號分隔規則清單。  例如，這兩個規則都可透過設定`ptprotoswitch=adfetch_rule1,adfetch_rule2`來執行：

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

請連絡您的技術支援以建立／啟用您帳戶的這些規則。