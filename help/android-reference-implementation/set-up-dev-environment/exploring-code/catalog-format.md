---
description: Primetime參考實作使用以JSON為基礎的動態消息格式來回應。 使用IFeedItemAdapter介面的實現來解析此格式。
seo-description: Primetime參考實作使用以JSON為基礎的動態消息格式來回應。 使用IFeedItemAdapter介面的實現來解析此格式。
seo-title: 目錄格式
title: 目錄格式
uuid: 6e1a526f-c0bb-403d-a792-666caf5479a5
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---


# 目錄格式{#catalog-format}

Primetime參考實作使用以JSON為基礎的動態消息格式來回應。 使用IFeedItemAdapter介面的實現來解析此格式。

>[!NOTE]
>
>此饋送格式是參考實作所使用的範例格式，並做為如何剖析格式及對應至饋送介面的範例。 您可以將自己的輸入動態消息格式與自己的動態消息介面實施搭配使用。

在高階層，此格式由一系列內容項目組成。 每個項目代表即時或VOD發佈的視訊內容：

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

每個動態消息項目都是具有一組特定屬性的JSON物件：

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
| `id` | 動態消息發佈系統所設定之內容的唯一識別碼／指南。 |
| `title` | 內容的標題。 |
| `description` | 內容說明。 |
| `categories` | 為內容標籤的類別清單，可供應用程式用來增強使用者體驗。 閱讀內容的屬性。 |
| `keywords` | 以逗號分隔的關鍵字清單，可供應用程式用來增強使用者的體驗。 閱讀內容的屬性。 |
| `isLive` | true或false，指出其為即時或VOD串流。 |
| `content` | JSON物件的陣列，內含內容的替代格式以及對應的URL。 例如，f4m和m3u8格式可能有URL。 JSON物件屬性將於下文進一步說明。 |
| `thumbnails` | JSON物件陣列，其中包含不同縮圖大小的URL。 JSON物件屬性定義如下。 |
| `metadata` | 定義內容中繼資料的JSON物件，目前此中繼資料僅限廣告相關中繼資料。 元資料對象定義如下。 |

下列程式碼區塊定義JSON物件，這些物件構成&#x200B;**內容物件**&#x200B;的陣列：

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
| 格式 | Android需要使用m3u8格式。 |
| url | 指定格式的視訊串流URL。 |

下列程式碼區塊會定義JSON物件，這些物件會構成&#x200B;**縮圖物件**&#x200B;的陣列：

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
| 格式 | 指示縮圖檔案格式的字串，例如JPEG、PNG等。 |
| 高度 | 縮圖的高度。 在參照應用程式中，高度和寬度最小的縮圖會傳回為小縮圖，而寬度和高度最大的縮圖則會傳回為大縮圖。 |
| 寬度 | 縮圖的寬度。 在參照應用程式中，高度和寬度最小的縮圖會傳回為小縮圖，而寬度和高度最大的縮圖則會傳回為大縮圖。 |
| url | 縮圖檔案的URL。 |

以下代碼塊定義&#x200B;**元資料對象**:

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
| type | 值可以是黃金時段廣告、直接廣告插播或自訂廣告標籤。 <br/><br/>PSDK提供下列中繼資料類型的內建支援：黃金時段廣告服務（黃金時段廣告）的Auditude相關中繼資料、具有廣告URL的直接廣告插播（直接廣告插播），以及提供每個廣告標籤（自訂廣告標籤）之TimeRange的自訂廣告標籤。每種類型在PSDK中都有內建的AdProvider，可處理中繼資料。  <br/><br/>以下定義了每種格式的JSON格式。 |
| 詳細資訊 | 包含廣告中繼資料屬性。 這兩種廣告中繼資料都有其專屬的屬性集，定義如下。 對於內建類型，包含的屬性會定義PSDK預期的該類型資料。 |
| 權益 | 權益相關中繼資料 |
| id | 用於Adobe Primetime付費電視通行證服務之授權要求的媒體資源ID。 ID可以是文字字串或HTML編碼的mRSS字串。 任何需要授權的媒體內容都必須包含有效的資源ID。 |

