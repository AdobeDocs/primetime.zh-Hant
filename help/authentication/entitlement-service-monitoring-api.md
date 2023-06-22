---
title: 權益服務監視API
description: 權益服務監視API
exl-id: a9572372-14a6-4caa-9ab6-4a6baababaa1
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '2026'
ht-degree: 0%

---

# 權益服務監視API {#entitlement-service-monitoring-api}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## API概述 {#api-overview}

軟體權利檔案服務監控(ESM)是以WOLAP （Web型）實作 [線上分析處理](https://en.wikipedia.org/wiki/Online_analytical_processing){target=_blank})專案。 ESM是由資料倉儲支援的通用業務報告Web API。 它用作HTTP查詢語言，可讓典型OLAP操作以RESTfully執行。

>[!NOTE]
>
>ESM API並非一般可用功能。 如需瞭解可用性相關問題，請聯絡您的Adobe代表。

ESM API提供基礎OLAP立方體的階層檢視。 每個資源([維度](#esm_dimensions) 在維度階層中，對應為URL路徑區段)會產生包含（彙總）的報表 [量度](#esm_metrics) 用於目前的選取範圍。 每個資源都指向其父資源（用於累計）及其子資源（用於向下鑽研）。 切片和切割是透過將維度釘選到特定值或範圍的查詢字串引數來達成。

REST API會根據維度路徑、提供的篩選器和選取的量度，在請求中指定的時間間隔內提供可用資料（如果未提供，則會退回預設值）。 時間範圍不會套用至不包含時間維度（年、月、日、小時、分鐘、秒）的報表。

端點URL根路徑會傳回單一記錄中的整體彙總量度，以及可用深入研究選項的連結。 API版本會對應為端點URI路徑的尾端區段。 例如， `https://mgmt.auth.adobe.com/*v2*` 表示使用者端將存取WOLAP第2版。

可用的URL路徑可透過回應中包含的連結來探索。 有效的URL路徑會被保留，以對應基礎向下鑽研樹狀結構中的路徑，該樹狀結構會保留（預先）彙總的量度。 表單中的路徑 `/dimension1/dimension2/dimension3` 將反映這三個維度的預先彙總(相當於SQL `clause GROUP` 作者： `dimension1`， `dimension2`， `dimension3`)。 如果這樣的預先彙總不存在，且系統無法即時計算，則API將傳回「404找不到」回應。

## 向下鑽研樹狀結構 {#drill-down-tree}

下列向下追溯樹狀結構說明ESM 2.0中可用的維度（資源） [程式設計師] (#esm_dimensions)和 [MVPDs](#esm_dimensions_mvpd).


### 程式設計師可用的Dimension {#progr-dimensions}

![](assets/esm-progr-dimensions.png)

### MVPD可用的Dimension {#mvpd-dimensions}

![](assets/esm-mvpd-dimensions.png)

的GET `https://mgmt.auth.adobe.com/v2` API端點將傳回包含以下內容的表示法：

* 可用根目錄向下鑽研路徑的連結：

   * `<link rel="drill-down" href="/v2/dimensionA"/>`

   * `<link rel="drill-down" href="/v2/dimensionB"/>`

* 所有量度的摘要（彙總值） （在預設間隔中，由於未提供查詢字串引數，請參閱下文）。


遵循向下鑽研路徑（逐步執行）：
`/dimensionA/year/month/day/dimensionX` 擷取下列回應：

* 連結至&quot;`dimensionY`「和」`dimensionZ`&quot;深入研究選項

* 包含每個值的每日彙總報表 `dimensionX`


### 篩選器

除了日期/時間維度之外，目前投影可用的任何維度（維度路徑）都可以使用其名稱作為查詢字串引數來篩選。

可使用下列篩選選項：

* **等於** 篩選器是透過將維度名稱設定為查詢字串中的特定值來提供。

* **在** 您可以透過多次新增具有不同值的相同dimension-name引數來指定篩選器： dimension=value1\&amp;dimension=value2

* **不等於** 篩選器必須使用「\！」 維度名稱后的符號，結果為「\！」=&#39; &quot;operator&quot;： dimension\！=value

* **不在……之內** 篩選器需要&#39;\！=&#39;運運算元使用多次，一次用於集合中的每個值： dimension\！=value1\&amp;dimension！=value2&amp;...

查詢字串中的維度名稱也有特殊用法：如果維度名稱用作無值的查詢字串引數，這會指示API傳回報表中包含該維度的投影。

### 範例ESM查詢

| *URL* | *SQL對應項* |
|---|---|
| /dimension1/dimension2/dimension3？dimension1=value1 | 從投影中選取*，其中dimension1 = &#39;value1&#39; </br> 依dimension1、dimension2、dimension3分組 |
| /dimension1/dimension2/dimension3？dimension1=value1&amp;dimension1=value2 | 從投影中選取*，其中dimension1 IN (&#39;value1&#39;， &#39;value2&#39;) </br> 依dimension1、dimension2、dimension3分組 |
| /dimension1/dimension2/dimension3？dimension1！=value1 | 從投影中選取*，其中dimension1 &lt;> &#39;value1&#39; | </br> 依dimension1、dimension2、dimension3分組 |
| /dimension1/dimension2/dimension3？dimension1！=value1&amp;dimension2！=value2 | 從投影中選取*，其中dimension1不在(&#39;value1&#39;， &#39;value2&#39;) | </br> 依dimension1、dimension2、dimension3分組 |
| 假設沒有直接路徑： /dimension1/dimension3 </br> 但有一個路徑： /dimension1/dimension2/dimension3 </br> </br> /dimension1？dimension3 | 選取*從投影群組，依dimension1， dimension3 |

>[!NOTE]
>
>這些篩選技術均無法用於 `date/time` 維度。 篩選的唯一方法 `date/time` 尺寸是用來設定 `start` 和 `end` 將查詢字串引數（如下所述）新增至所需的值。

下列查詢字串引數對API而言具有保留的意義（因此它們不能用作維度名稱，否則無法篩選此類維度）。

### ESM API保留的查詢字串引數

| 引數 | 可選 | 說明 | 預設值 | 範例 |
| --- | ---- | --- | ---- | --- |
| access_token | 是 | 如果已啟用IMS OAuth保護，IMS權杖可作為標準授權持有人權杖或查詢字串引數傳遞。 | 無 | access_token=XXXXXX |
| dimension-name | 是 | 任何維度名稱 — 包含於目前URL路徑或任何有效子路徑中；此值將視為等於篩選器。 如果未提供值，即使指定尺寸未包含或鄰近目前路徑，也會強制將其包含在輸出中 | 無 | someDimension=someValue&amp;someOtherDimension |
| 結束 | 是 | 報表結束時間（以毫秒為單位） | 伺服器的目前時間 | end=2012-07-30 |
| 格式 | 是 | 用於內容交涉（具有相同效果，但優先順序低於路徑「擴充功能」 — 請參閱下文）。 | 無：內容交涉將嘗試其他策略 | format=json |
| 限制 | 是 | 要傳回的最大列數 | 請求中未指定限制時，伺服器會在自我連結中報告的預設值 | limit=1500 |
| 量度 | 是 | 要傳回的以逗號分隔的量度名稱清單；這應該用於篩選可用量度的子集（以減少裝載大小），以及強制執行API以傳回包含請求量度的投影（而不是預設的最佳投影）。 | 若未提供此引數，將會傳回目前投影可用的所有量度。 | metrics=m1，m2 |
| 開始 | 是 | 報表的開始時間設為ISO8601；如果只提供字首，伺服器會填入剩餘的部分：例如，start=2012會產生start=2012-01-01:00:00:00 | 伺服器在其自我連結中報告；伺服器會嘗試根據選取的時間詳細程度提供合理的預設值 | start=2012-07-15 |

目前唯一可用的HTTP方法是GET。 未來版本可能會提供OPTIONS/HEAD方法的支援。

## ESM API狀態代碼 {#esm-api-status-codes}

| 狀態代碼 | 原因片語 | 說明 |
|---|---|---|
| 200 | 確定 | 回應將包含「統計」和「深入研究」連結（如果適用）。 報表將呈現為資源的屬性：巢狀的「report」元素/屬性。 |
| 400 | 錯誤請求 | 回應內文會包含簡訊，說明要求的問題。 </br> </br> 400 Bad Request狀態會在回應內文中隨附說明文字（純/文字媒體型別），提供有關使用者端錯誤的實用資訊。 除了套用至非現有維度的瑣碎情況（例如無效的日期格式或篩選器）外，系統還將拒絕回應需要即時返回或彙總大量資料的查詢。 |
| 401 | 未獲授權 | 由於請求未包含適當的OAuth標頭以便驗證使用者所導致 |
| 403 | 已禁止 | 指出目前的安全性內容不允許此要求；當使用者已驗證但不允許存取要求的資訊時，就會發生這種情況 |
| 404 | 找不到 | 當請求中提供了無效的URL路徑時發生。 如果使用者端依循隨200個回應提供的「深入研究」/「統計」連結，則絕不應該發生這種情況 |
| 405 | 不允許的方法 | 表示要求中使用不受支援的方法。 雖然目前僅支援GET方法，但未來版本可能允許HEAD或OPTIONS |
| 406 | 不可接受 | 代表使用者端要求了不支援的媒體型別 |
| 500 | 內部伺服器錯誤 | 「這絕不應該發生」 |
| 503 | 服務無法使用 | 代表應用程式或其相依性中的錯誤 |

## 資料格式 {#data-formats}

資料提供下列格式：

* JSON （預設）
* XML
* CSV
* HTML（供示範用途）

使用者端可使用以下內容交涉策略（優先順序由清單中的位置給出 — 首先）：

1. URL路徑的最後一個區段後面附加了「副檔名」：例如， `/esm/v2/media-company/year/month/day.xml`. 如果URL包含查詢字串，則擴充功能必須位於問號之前： `/esm/v2/media-company/year/month/day.csv?mvpd= SomeMVPD`
1. 格式查詢字串引數：例如， `/esm/report?format=json`
1. 標準HTTP Accept標頭：例如 `Accept: application/xml`

「擴充功能」和查詢引數都支援下列值：

* xml
* json
* csv
* html

如果任何策略未指定任何媒體型別，API預設會產生JSON內容。

## 超文字應用程式語言 {#hypertext-application-language}

針對JSON和XML，裝載將編碼為HAL，如下所述：  <http://stateless.co/hal_specification.html>.

實際報表（稱為「報表」的巢狀標籤/屬性）包含實際記錄清單，其中包含所有選定/適用的維度和量度及其值，編碼如下：

### JSON

```JSON
 "report": [
  {
    "dimension1": "d1",
    ...
    "metric1": "m1",
    ...
  }, {
    ...
  }
]
```

### XML

```XML
 <report>
  <record dimension1="d1" ... metric1="m1" ... />
  ...
</report
```

對於XML和JSON格式，記錄中的欄位（維度和量度）順序未指定 — 但一致（所有記錄的順序將相同）。 不過，使用者端不應依賴記錄中欄位的任何特定順序。

資源連結（JSON中的「self」rel和XML中的「href」資源屬性）包含內嵌報表使用的目前路徑和查詢字串。 查詢字串將會顯示所有隱含和明確的引數，因此裝載會明確指出使用的時間間隔、隱含的篩選器（如果有的話）等等。 資源內的其餘連結將包含可以依循的所有可用區段，以向下鑽研目前的資料。 也會提供彙總連結，且會指向父路徑（若有）。 此 `href` 向下切入/向上連結的值僅包含URL路徑（不包含查詢字串，因此使用者端需要視需要附加它）。 請注意，並非目前資源使用（或暗示）的所有查詢字串引數都適用於「向上彙整」或「向下鑽研」連結（例如，篩選條件可能不適用於子資源或超級資源）。

範例(假設有一個量度稱為 `clients` 而且有一個預先彙總 `year/month/day/...`)：

* https://mgmt.auth.adobe.com/esm/v2/year/month.xml

```XML
   <resource href="/esm/v2/year/month?start=2012-07-20T00:00:00&end=2012-08-20T14:35:21">
   <links>
   <link rel="roll-up" href="/esm/v2/year"/>
   <link rel="drill-down" href="/esm/v2/year/month/day"/>
   </links>
   <report>
   <record month="6" year="2012" clients="205"/>
   <record month="7" year="2012" clients="466"/>
   </report>
   </resource>
```

* https://mgmt.auth.adobe.com/esm/v2/year/month.json 

   ```JSON
       {
         "_links" : {
           "self" : {
             "href" : "/esm/v2/year/month?start=2012-07-20T00:00:00&end=2012-08-20T14:35:21"
           },
           "roll-up" : {
             "href" : "/esm/v2/year"
           },
           "drill-down" : {
             "href" : "/esm/v2/year/month/day"
           }
         },
         "report" : [ {
           "month" : "6",
           "year" : "2012",
           "clients" : "205"
         }, {
           "month" : "7",
           "year" : "2012",
           "clients" : "466"
         } ]
       }
   ```

### CSV

在CSV資料格式中，不會內嵌提供連結或其他中繼資料（標題列除外），而是會依照以下模式在檔案名稱中提供選取範圍中繼資料：

```CSV
    esm__<start-date>_<end-date>_<filter-values,...>.csv
```

CSV將包含標題列，然後報告資料作為後續列。 標題列會包含所有維度，後面接著所有量度。 報表資料的排序順序將反映在維度的順序中。 因此，如果資料排序依據 `D1` 然後由 `D2`，則CSV標頭看起來會像這樣： `D1, D2, ...metrics...`.

標題列中的欄位順序將反映表格資料的排序順序。


範例： https://mgmt.auth.adobe.com/v2/year/month.csv將產生一個名為的檔案 `report__2012-07-20_2012-08-20_1000.csv` ，內容如下：


| 年 | 月 | 使用者端 |
| ---- | :---: | ------- |
| 2012 | 6 | 580 |
| 2012 | 7 | 231 |

## 資料新鮮度 {#data-freshness}

成功的HTTP回應包含 `Last-Modified` 標頭，指出上次更新本文中報表的時間。 缺少Last-Modified標題表示報表資料會即時計算。

通常，粗粒度資料的更新頻率會低於細粒度資料(例如，以分鐘計數值或每小時數值可能比每日數值更新，尤其是無法根據較小粒度（例如不重複計數）計算的量度)。

未來版本的ESM可能會提供標準「If-Modified-Since」標頭，讓使用者端執行條件式GET。

## GZIP壓縮 {#gzip-compression}

Adobe強烈建議您在擷取ESM報表的使用者端中啟用gzip支援。 這樣做會大幅減少回應大小，進而減少您的回應時間。 （ESM資料的壓縮率在20到30之間。）

若要在您的使用者端中啟用gzip壓縮，請將 `Accept-Encoding:` 標題如下：

* Accept-Encoding： gzip， deflate


<!--
## Related Information {#related-information}

- [ESM Overview](/help/authentication/entitlement-service-monitoring-overview.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Understanding Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->
