---
title: 權利資源ID的JSON物件
description: 下列程式碼區塊提供軟體權利資源ID為簡單文字字串時的JSON物件範例。
exl-id: 396c43e7-404a-40f5-8113-a720e2c834e7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# 權利資源ID的JSON物件 {#json-object-for-entitlement-resource-id}

下列程式碼區塊提供軟體權利資源ID為簡單文字字串時的JSON物件範例。 在此案例中，資源ID是字串「resource」。

```
"metadata" : { 
"entitlement" : { 
"id" : "resource" 
} 
}
```

下列程式碼區塊提供權利資源ID為HTML編碼的mRSS字串時的JSON物件範例。

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

下列mRSS字串會作為資源ID使用。

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
