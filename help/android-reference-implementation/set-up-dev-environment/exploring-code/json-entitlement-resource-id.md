---
title: 權利資源ID的JSON對象
description: 當權利資源ID為簡單文本字串時，以下代碼塊提供了JSON對象的示例。
exl-id: 396c43e7-404a-40f5-8113-a720e2c834e7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# 權利資源ID的JSON對象 {#json-object-for-entitlement-resource-id}

當權利資源ID為簡單文本字串時，以下代碼塊提供了JSON對象的示例。 在這種情況下，資源ID是字串&quot;resource&quot;。

```
"metadata" : { 
"entitlement" : { 
"id" : "resource" 
} 
}
```

當權利資源ID是HTML編碼的mRSS字串時，以下代碼塊提供了JSON對象的示例。

```
<rss version="2.0" xmlns:media="https://search.yahoo.com/mrss/"> 
<channel> 
<title>REF_ADOBE</title> 
<item> 
<title>Adobe Primetime Reference</title> 
<guid>1234</guid> 
<media:rating scheme="urn:v-chip">TV-PG</media:rating> 
</item> 
</channel> 
</rss>
```

以下mRSS字串用作資源ID。

```
"metadata" : { 
    "entitlement" : { 
        "id" : "<rss version=&quot;2.0&quot; 
        xmlns:media=&quot; 
        https://search.yahoo.com/mrss/&quot; 
        ><channel><title>REF_ADOBE</title><item> 
        <title>Adobe Primetime Reference</title><guid> 
        1234</guid><media:rating scheme=&quot;urn:v-chip&quot;> 
        TV-PG</media:rating></item></channel></rss>" 
        } 
} 
```
