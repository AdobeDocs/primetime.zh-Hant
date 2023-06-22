---
title: 識別受保護的資源
description: 識別受保護的資源
exl-id: e96aea02-54b2-491d-ba91-253c0d0e681c
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# 識別受保護的資源 {#identifying-protected-resources}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 概觀 {#overview}

每個授權請求（或檢查授權的請求）都必須包含使用者請求存取之受保護資源的唯一識別碼。 受保護的資源可以是任何層級的授權內容，如MVPD和參與的程式設計人員所協定。 潛在受保護資源必須適合此樹狀結構，且粒度越來越具體：

- 網路
   - 頻道
      - 顯示
         - 集數
            - 資產\
                

</br>

## 媒體RSS格式 {#media_rss}

資源可由簡單字串（管道的唯一識別碼）識別，或以Media RSS格式(MRSS)表示，如Adobe(或Adobe Primetime驗證授權合作夥伴)與參與的MVPD和程式設計人員所協定。 用作資源規範的RSS字串可以包含其他資訊，例如分級和家長監護中繼資料。\
 

如果您使用簡單資源識別碼（例如「TNT」），則會假設它代表管道，並轉譯成此RSS資源規範：

```RSS
    <rss version="2.0"> 
        <channel>
            <title>TNT</title>
        </channel>
    </rss>
```
 

例如，更複雜的規範可能包含其他評等資訊。 您可以將整個RSS字串傳遞至需要資源ID的Access Enabler函式，例如 [`getAuthorization()`](/help/authentication/rest-api-reference.md)：

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

資源指定字元對Adobe Primetime驗證而言是不透明的；它們只會傳遞到MVPD。 如果MVPD無法辨識或無法剖析您的資源規範，則會傳回Adobe Primetime驗證錯誤，並將錯誤傳回 `tokenRequestFailed()` callback。

<!--
## Related Information {#related}

-  User Metadata
-  Preflight Authorization
-->
