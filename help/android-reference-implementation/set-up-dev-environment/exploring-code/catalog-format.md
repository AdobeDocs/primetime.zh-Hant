---
description: 黃金時段引用實現使用基於JSON的源格式進行響應。 此格式使用IFeedItemAdapter介面的實現進行分析。
title: 目錄格式
exl-id: faaeb647-9c01-4290-be1e-2b8461c8ad27
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# 目錄格式 {#catalog-format}

黃金時段引用實現使用基於JSON的源格式進行響應。 此格式使用IFeedItemAdapter介面的實現進行分析。

>[!NOTE]
>
>此饋送格式是引用實現使用的示例格式，並用作如何分析格式並將其映射到饋送介面的示例。 您可以將自己的輸入源格式與自己的源介面實現一起使用。

在高級別，格式由一組內容條目組成。 每個條目都表示即時或VOD發佈的視頻內容：

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

每個源項都是具有給定屬性集的JSON對象：

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
| `id` | 由饋送發佈系統設定的內容的唯一標識符/指南。 |
| `title` | 內容的標題。 |
| `description` | 內容的說明。 |
| `categories` | 為內容標籤的類別清單，該內容可由應用程式使用以增強用戶體驗。 讀入內容的屬性。 |
| `keywords` | 應用程式可以使用逗號分隔的關鍵字清單來增強用戶體驗。 讀入內容的屬性。 |
| `isLive` | true或false，指示它是Live還是VOD流。 |
| `content` | JSON對象的陣列，該JSON對象具有內容的替代格式以及相應的URL。 例如，f4m和m3u8格式可能有URL。 JSON對象屬性在下面進行進一步說明。 |
| `thumbnails` | JSON對象的陣列，具有不同大小縮略圖的URL。 JSON對象屬性在下面定義。 |
| `metadata` | 定義內容元資料的JSON對象，當前此元資料僅限於與廣告相關的元資料。 元資料對象在下面定義。 |

以下代碼塊定義構成JSON陣列的JSON對象 **內容對象**:

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
| 格式 | Android需要m3u8格式。 |
| url | 指定格式的視頻流的URL。 |

以下代碼塊定義構成JSON陣列的JSON對象 **縮略圖對象**:

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
| 格式 | 一個字串，指示縮略圖檔案的格式，例如JPEG、PNG等。 |
| 高度 | 縮略圖的高度。 在參照應用程式中，高度和寬度最小的縮略圖作為小縮略圖返回，而寬度和高度最大的縮略圖作為大縮略圖返回。 |
| 寬度 | 縮略圖的寬度。 在參照應用程式中，高度和寬度最小的縮略圖作為小縮略圖返回，而寬度和高度最大的縮略圖作為大縮略圖返回。 |
| url | 縮略圖檔案的URL。 |

以下代碼塊定義 **元資料對象**:

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
| 廣告 | 與廣告相關的元資料。 |
| 類型 | 值可以是黃金時段廣告、直接廣告分段或自定義廣告標籤。 <br/><br/>PSDK為以下類型的元資料提供內置支援：黃金時段廣告服務（黃金時段廣告）的與審計相關的元資料、帶廣告URL的直接廣告中斷（直接廣告中斷）以及為每個廣告標籤（自定義廣告標籤）提供TimeRange的自定義廣告標籤。 每種類型在PSDK中都有一個內置的AdProvider來處理元資料。  <br/><br/>下面定義了每種格式的JSON格式。 |
| 詳細資訊 | 包括廣告元資料屬性。 這兩種類型的廣告元資料都有其自己的一組屬性在下面定義。 對於內置類型，包括的屬性定義了PSDK所期望的該類型的資料。 |
| 權利 | 與權利相關的元資料 |
| ID | 用於針對Adobe Primetime付費電視通過服務的授權請求的媒體資源ID。 ID可以是文本字串或HTML編碼的mRSS字串。 任何需要授權的媒體內容必須包含有效的資源ID。 |
