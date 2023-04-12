---
title: 標識受保護的資源
description: 標識受保護的資源
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# 標識受保護的資源 {#identifying-protected-resources}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 概述 {#overview}

每個授權請求（或檢查授權的請求）必須包含用戶請求訪問的受保護資源的唯一標識符。 受保護的資源可以是授權內容的任何級別，如MVPD與參與的程式設計人員之間的協定。 潛在的受保護資源必須適合這種粒度越來越特定的樹結構：

- 網路
   - 管道
      - 顯示
         - 集數
            - 資產\
                

</br>

## 媒體RSS格式 {#media_rss}

資源可以由簡單字串（通道的唯一識別碼）來識別，或可以按照Adobe(或Adobe Primetime驗證授權合作夥伴)與參與的MVPD和程式設計人員之間的協定，以Media RSS格式(MRSS)來表示。 用作資源說明符的RSS字串可以包括諸如分級和家長控制元資料等其他資訊。\
 

如果您使用簡單的資源標識符，如&quot;TNT&quot;，則假定它表示通道，並轉換為此RSS資源說明符：

```RSS
    <rss version="2.0"> 
        <channel>
            <title>TNT</title>
        </channel>
    </rss>
```
 

更複雜的說明符可能包括，例如，附加評級資訊。 您可以將整個RSS字串傳遞到需要資源ID的Access Enabler函式，例如 [`getAuthorization()`](/help/authentication/rest-api-reference.md):

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

資源說明符對Adobe Primetime驗證不透明；它們只會傳遞至MVPD。 如果MVPD不識別或無法剖析資源說明碼，會傳回錯誤給Adobe Primetime驗證，這會將錯誤傳回給您的 `tokenRequestFailed()` 回呼。

<!--
## Related Information {#related}

-  User Metadata
-  Preflight Authorization
-->