---
description: Primetime參考實作會使用JSON型摘要格式來回應。 會使用IFeedItemAdapter介面的實作來剖析此格式。
title: 目錄格式
exl-id: faaeb647-9c01-4290-be1e-2b8461c8ad27
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# 目錄格式 {#catalog-format}

Primetime參考實作會使用JSON型摘要格式來回應。 會使用IFeedItemAdapter介面的實作來剖析此格式。

>[!NOTE]
>
>此摘要格式是參考實作所使用的範例格式，可做為如何剖析格式並對應至摘要介面的範例。 您可以將自己的輸入摘要格式用於自己的摘要介面實作。

從高層面來看，格式是由一系列內容專案所組成。 每個專案代表即時或VOD發佈的視訊內容：

```
{
    "entries": [
        {
        },
        {
        },
        ...
    ]
}
```

每個摘要專案都是一個JSON物件，其中包含一組給定的屬性：

```
{
    "entries": [
        
            "id": "episode1",
            "title": "My episode1",
            "description": "This is an episode.",
            "categories": "documentary, educational, children",
            "keywords": "List, of, comma, separated, keywords",
            "isLive": false,
            "content":  [
                
                },
                
                },
            ],
            "thumbnails": [
                
                },
                
                }
            ]
            "metadata": 
            } 
        }
    ]
}
```

| 屬性 | 說明 |
|---|---|
| `id` | 摘要發佈系統所設定的內容唯一識別碼/指南。 |
| `title` | 內容的標題。 |
| `description` | 內容的說明。 |
| `categories` | 為內容標籤的類別清單，可供應用程式用於增強使用者體驗。 閱讀內容的屬性。 |
| `keywords` | 以逗號分隔的關鍵字清單，可供應用程式用來增強使用者的體驗。 閱讀內容的屬性。 |
| `isLive` | true或false，指出其為即時或VOD資料流。 |
| `content` | JSON物件陣列，具有內容的替代格式以及對應的URL。 例如，可能有f4m和m3u8格式的url。 JSON物件屬性在下方進一步說明。 |
| `thumbnails` | JSON物件的陣列，其中包含不同大小縮圖的URL。 JSON物件屬性定義如下。 |
| `metadata` | 定義內容中繼資料的JSON物件，目前此中繼資料僅限於廣告相關中繼資料。 中繼資料物件定義如下。 |

下列程式碼區塊會定義構成陣列的JSON物件 **內容物件**：

```
"content":  [
    {
        "format": "M3U8",
        "url": "https://adobeprimetime-f.akamaihd.net/i/
<i>longstringofcharacters</i>/
                 Episode_,640x360_1000,640x360_700,_b.mp4.csmil/master.m3u8",
        "language": "en"
    }  
],
```

| 屬性 | 說明 |
|--- |--- |
| 格式 | Android必須是m3u8格式。 |
| url | 指定格式的視訊資料流的URL。 |

下列程式碼區塊會定義構成陣列的JSON物件 **縮圖物件**：

```
"thumbnails": [
    {
        "format": "JPEG",
        "height":  "90",
        "width": "160",
        "url": "https://example.com/small.jpg"
    },
    {
        "format": "JPEG",
        "height": "450",
        "width": "800",
        "url": "https://example.com/large.jpg"
    }
],
```

| 屬性 | 說明 |
|---|---|
| 格式 | 字串，指出縮圖檔案的格式，例如JPEG、PNG等。 |
| 高度 | 縮圖的高度。 在參考應用程式中，高度和寬度最小的縮圖會以小型縮圖傳回，而寬度與高度最大的縮圖則會以大型縮圖傳回。 |
| 寬度 | 縮圖的寬度。 在參考應用程式中，高度和寬度最小的縮圖會以小型縮圖傳回，而寬度與高度最大的縮圖則會以大型縮圖傳回。 |
| url | 縮圖檔案的url。 |

下列程式碼區塊會定義 **中繼資料物件**：

```
"metadata" : {
    "ad" : {
        "type" : "",
        "details" : {
        }
    }
    "entitlement" : {
        "id" : ""
    }
}
```

| 屬性 | 說明 |
|--- |--- |
| 廣告 | 廣告相關中繼資料。 |
| type | 值可以是Primetime廣告、直接廣告插播或自訂廣告標籤。 <br/><br/>PSDK內建支援下列中繼資料型別：Primetime廣告服務（Primetime廣告）的稽核相關中繼資料、具有廣告URL的直接廣告插播（直接廣告插播），以及為每個廣告標籤提供TimeRange的自訂廣告標籤（自訂廣告標籤）。 每種型別在PSDK中都有內建的AdProvider，可處理中繼資料。  <br/><br/>下文已定義每個專案的JSON格式。 |
| 詳細資料 | 包含廣告中繼資料屬性。 這兩種型別的廣告中繼資料都有各自專屬的屬性集，定義如下。 對於內建型別，包含的屬性會定義PSDK預期適用於該型別的資料。 |
| 權利 | 權益相關中繼資料 |
| id | 用於向Adobe Primetime pay-TV pass服務提出授權請求的媒體資源ID。 ID可以是文字字串或HTML編碼的mRSS字串。 任何需要授權的媒體內容都必須包含有效的資源ID。 |
