---
title: 權益資源ID的JSON物件
description: 當權益資源ID為簡單文字字串時，下列程式碼區塊提供JSON物件的範例。
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# 權益資源ID {#json-object-for-entitlement-resource-id}的JSON物件

當權益資源ID為簡單文字字串時，下列程式碼區塊提供JSON物件的範例。 在這種情況下，資源ID是字串&quot;resource&quot;。

```
"metadata" : { 
"entitlement" : { 
"id" : "resource" 
} 
}
```

當權益資源ID是HTML編碼的mRSS字串時，下列程式碼區塊提供JSON物件的範例。

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
