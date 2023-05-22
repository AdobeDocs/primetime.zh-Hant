---
title: 清單重寫和讀取規則
description: 清單重寫和讀取規則
exl-id: 3750abc1-da60-4faf-ba85-37914f33641f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# 清單重寫和讀取規則 {#manifest-rewriting}

黃金時段Ad Insertion能夠使用簡單的搜索/替換規則重寫片段和獲取資產。  這可用於將https向下轉換為http請求，通過刪除TLS握手來提高效能。  這也可用於從同一CDN交付廣告資產和CDN資產。

規則定義為規則運算式搜索/替換，可用於在發送URL之前以及插入清單後轉換URL。

此示例規則將將所有廣告請求從https轉換為http。

```
find: "https://domain.com/(.*)"
replace: "http://domain.com/$1"
```

以下規則將使用內容CDN傳遞位於Adobe廣告儲存CDN上的廣告。

```
find: "https?://primetime-a.akamaihd.net/(.*)"
replace: "http://mycdn.com/ad-mapping-pathname/$1"
```

通過修改 `ptprotoswitch` BootstrapAPI中的參數，該參數是要執行的規則的逗號分隔清單。  例如，這兩個規則都可以通過設定 `ptprotoswitch=adfetch_rule1,adfetch_rule2`:

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

請與技術支援聯繫，為您的帳戶建立/啟用這些規則。
