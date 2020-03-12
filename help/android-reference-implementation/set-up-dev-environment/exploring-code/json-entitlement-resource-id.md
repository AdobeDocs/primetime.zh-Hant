---
seo-title: 權益資源ID的JSON物件
title: 權益資源ID的JSON物件
uuid: f5b659da-1732-404c-bf00-d32a0ae39aa1
description: 當權益資源ID為簡單文字字串時，下列程式碼區塊提供JSON物件的範例。
seo-description: 當權益資源ID為簡單文字字串時，下列程式碼區塊提供JSON物件的範例。
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 權益資源ID的JSON物件 {#json-object-for-entitlement-resource-id}

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
