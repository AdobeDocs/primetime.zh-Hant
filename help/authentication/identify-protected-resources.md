---
title: 確定受保護的資源
description: 確定受保護的資源
exl-id: e96aea02-54b2-491d-ba91-253c0d0e681c
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# 確定受保護的資源 {#identifying-protected-resources}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 概述 {#overview}

每個授權請求（或檢查授權的請求）必須包含用戶請求訪問的受保護資源的唯一標識符。 受保護的資源可以是任何級別的授權內容，如MVPD與參與的程式設計師所同意。 潛在的受保護資源必須適合此樹結構，其粒度越來越具體：

- 網路
   - 頻道
      - 顯示
         - 插曲
            - 資產\
                

</br>

## 媒體RSS格式 {#media_rss}

資源可以通過簡單字串（頻道的唯一標識符）來標識，也可以按照Adobe(或Adobe Primetime身份驗證授權夥伴)與參與的MVPD和程式設計師之間的約定以媒體RSS格式(MRSS)來表示。 用作資源說明符的RSS字串可以包括附加資訊，如分級和家長控制元資料。\
 

如果使用簡單的資源標識符，如&quot;TNT&quot;，則假定它代表一個通道，並被轉換為此RSS資源說明符：

```RSS
    <rss version="2.0"> 
        <channel>
            <title>TNT</title>
        </channel>
    </rss>
```
 

更複雜的說明符可能包括例如附加評級資訊。 您可以將整個RSS字串傳遞給需要資源ID的Access Enabler函式，如 [`getAuthorization()`](/help/authentication/rest-api-reference.md):

```rss
    var resource = 
        '<rss version="2.0" xmlns:media="http://search.yahoo.com/mrss/"> 
             <channel>
                 <title>TNT</title>
                 <media:rating scheme="urn:mpaa">pg</media:rating>
             </channel>
         </rss>'; 
    getAuthorization(resource);
```

資源說明符對Adobe Primetime驗證不透明；它們只是通過MVPD。 如果MVPD無法識別或無法分析您的資源說明符，它會將錯誤返回給Adobe Primetime驗證，從而將錯誤傳回給您 `tokenRequestFailed()` 回叫。

<!--
## Related Information {#related}

-  User Metadata
-  Preflight Authorization
-->
