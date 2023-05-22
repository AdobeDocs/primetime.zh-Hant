---
title: 權利服務監視API
description: 權利服務監視API
exl-id: a9572372-14a6-4caa-9ab6-4a6baababaa1
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '2026'
ht-degree: 0%

---

# 權利服務監視API {#entitlement-service-monitoring-api}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## API概述 {#api-overview}

權利服務監視(ESM)作為WOLAP（基於Web）實施 [聯機分析處理](https://en.wikipedia.org/wiki/Online_analytical_processing){target=_blank})項目。 ESM是由資料倉庫支援的通用業務報告Web API。 它充當HTTP查詢語言，使典型的OLAP操作能夠執行RESTfully。

>[!NOTE]
>
>ESM API通常不可用。 有關可用性問題，請與Adobe代表聯繫。

ESM API提供基礎OLAP多維資料集的分層視圖。 每個資源([尺寸](#esm_dimensions) 在維層次中，映射為URL路徑段)生成具有（聚合）的報告 [度量](#esm_metrics) 的子菜單。 每個資源都指向其父資源（用於匯總）及其子資源（用於向下鑽取）。 通過查詢字串參數將尺寸固定到特定值或範圍來實現切片和切割。

REST API根據維度路徑、提供的篩選器和所選度量在請求中指定的時間間隔內提供可用資料（如果未提供則回退到預設值）。 時間範圍不適用於不包含時間維度（年、月、日、小時、分鐘、秒）的報告。

終結點URL根路徑將返回單個記錄中的總體聚合度量以及指向可用深入查看選項的連結。 API版本被映射為終結點URI路徑的尾隨段。 比如說， `https://mgmt.auth.adobe.com/*v2*` 表示客戶端將訪問WOLAP版本2。

可用的URL路徑可通過響應中包含的連結發現。 保持有效URL路徑以映射保存（預）聚合度量的基礎下鑽樹中的路徑。 窗體中的路徑 `/dimension1/dimension2/dimension3` 將反映這三個維的預聚合(相當於SQL `clause GROUP` 按 `dimension1`。 `dimension2`。 `dimension3`)。 如果此類預聚合不存在，且系統無法即時計算，則API將返回404 Not Found（未找到）響應。

## 向下鑽取樹 {#drill-down-tree}

以下深入查找樹說明了ESM 2.0中可用的維（資源） [程式設計師] (#esm_dimensions和 [MVPD](#esm_dimensions_mvpd)。


### Dimension程式設計師 {#progr-dimensions}

![](assets/esm-progr-dimensions.png)

### Dimension可用於MVPD {#mvpd-dimensions}

![](assets/esm-mvpd-dimensions.png)

GET `https://mgmt.auth.adobe.com/v2` API終結點將返回包含以下內容的表示：

* 指向可用根向下鑽取路徑的連結：

   * `<link rel="drill-down" href="/v2/dimensionA"/>`

   * `<link rel="drill-down" href="/v2/dimensionB"/>`

* 所有度量的摘要（聚合值）（在預設間隔內，因為未提供查詢字串參數，請參閱下文）。


遵循向下鑽取路徑（逐步）:
`/dimensionA/year/month/day/dimensionX` 檢索以下響應：

* 到「」的連結`dimensionY`&quot;和&quot;`dimensionZ`&quot;向下鑽取選項

* 包含每個值的每日聚合的報表 `dimensionX`


### 篩選器

除日期/時間維外，可以使用當前投影（維路徑）的任何可用維名稱作為查詢字串參數進行篩選。

以下篩選選項可用：

* **等於** 篩選器是通過將維名稱設定為查詢字串中的特定值來提供的。

* **在** 可以通過多次添加相同dimension-name參數（使用不同的值）來指定篩選器：維=值1\&amp;dimension=值2

* **不等於** 篩選器必須使用「\！」 尺寸名稱后的符號，導致「\！」=&#39; &quot;運算子&quot;:維度\!=值

* **不在** 篩選器需要&#39;\!=&#39;運算子要多次使用，對於集中的每個值一次：維度\!=value1\&amp;dimension\=value2&amp;...

查詢字串中的維名稱也有特殊用法：如果維名稱用作查詢字串參數，且無值，則這將指示API返回在報告中包含該維的投影。

### ESM查詢示例

| *URL* | *SQL等效項* |
|---|---|
| /dimension1/dimension2/dimension3?dimension1=value1 | 從投影WHERE dimension1 = &#39;value1&#39;中選擇* </br> GROUP BY維1、維2、維3 |
| /dimension1/dimension2/dimension3?dimension1=value1=value2 | 從投影WHERE dimension1 IN(&#39;value1&#39;, &#39;value2&#39;)中選擇* </br> GROUP BY維1、維2、維3 |
| /dimension1/dimension2/dimension3?dimension1=value1 | 從投影WHERE dimension1 &lt;> &quot;value1&quot;中選擇* | </br> GROUP BY維1、維2、維3 |
| /dimension1/dimension2/dimension3?dimension1=value1&amp;dimension2=value2 | 從投影WHERE dimension1 NOT IN(&#39;value1&#39;, &#39;value2&#39;)中選擇* | </br> GROUP BY維1、維2、維3 |
| 假設沒有直接路徑：/dimension1/dimension3 </br> 但有一條路：/dimension1/dimension2/dimension3 </br> </br> /dimension1?dimension3 | 從投影GROUP BY dimension1, dimension3中選取* |

>[!NOTE]
>
>這些過濾技術都不適用 `date/time` 尺寸。 篩選的唯一方法 `date/time` 維是 `start` 和 `end` 查詢字串參數（如下所述）到所需值。

以下查詢字串參數對API具有保留的含義（因此不能將它們用作維名稱，否則不能對此類維進行篩選）。

### ESM API保留查詢字串參數

| 參數 | 可選 | 說明 | 預設值 | 示例 |
| --- | ---- | --- | ---- | --- |
| 訪問令牌 | 是 | 在啟用IMS OAuth保護的情況下，IMS令牌可以作為標準授權持有者令牌或作為查詢字串參數傳遞。 | 無 | access_token=XXXXX |
| 維名 | 是 | 任何維名稱 — 包含在當前URL路徑中或任何有效子路徑中；該值將被視為等於篩選器。 如果未提供值，則即使指定的尺寸未包括或與當前路徑相鄰，也會強制將其包括在輸出中 | 無 | someDimension=someValue&amp;someOtherDimension |
| 端 | 是 | 以米利斯為單位的報告的結束時間 | 伺服器的當前時間 | end=2012-07-30 |
| 格式 | 是 | 用於內容協商（效果相同，但優先順序低於路徑「擴展」 — 請參見下文）。 | 無：內容協商將嘗試其他策略 | 格式=json |
| 限 | 是 | 要返回的最大行數 | 如果請求中未指定限制，則伺服器在自連結中報告的預設值 | limit=1500 |
| 度量 | 是 | 要返回的度量名稱的逗號分隔清單；這應用於過濾可用度量的子集（以減小負載大小），還應用於強制API返回包含所請求度量的投影（而不是預設的最佳投影）。 | 如果未提供此參數，將返回當前投影的所有可用度量。 | 度量=m1,m2 |
| 開始 | 是 | ISO8601報告開始時間；如果僅提供前置詞，則伺服器將填寫剩餘部分：例如，start=2012將導致start=2012-01-01:00:00:00 | 伺服器在自連結中報告；伺服器嘗試根據所選時間粒度提供合理的預設值 | start=2012-07-15 |

當前唯一可用的HTTP方法是GET。 未來版本中可能提供對OPTIONS/HEAD方法的支援。

## ESM API狀態代碼 {#esm-api-status-codes}

| 狀態代碼 | 原因短語 | 說明 |
|---|---|---|
| 200 | 確定 | 響應將包含「上滾」和「下鑽」連結（如果適用）。 報告將作為資源的屬性呈現：嵌套的「report」元素/屬性。 |
| 400 | 錯誤請求 | 響應正文將包含一條文本消息，說明請求的錯誤。 </br> </br> 「400錯誤請求」狀態與響應正文（純/文本媒體類型）中的解釋文本相伴，該文本提供了有關客戶端錯誤的有用資訊。 除了諸如應用於非現有維的無效日期格式或篩選器等瑣碎情形外，系統還將拒絕響應需要即時返回或聚合大量資料的查詢。 |
| 401 | 未授權 | 由請求引起，該請求不包含正確的OAuth標頭以驗證用戶 |
| 403 | 禁止 | 指示在當前安全上下文中不允許請求；當用戶經過身份驗證但不允許訪問請求的資訊時發生 |
| 404 | 未找到 | 在隨請求提供無效的URL路徑時發生。 如果客戶端遵循隨200個響應提供的「向下鑽取」/「上滾」連結，則永遠不會發生這種情況 |
| 405 | 不允許使用方法 | 在請求中使用了不受支援方法的信號。 雖然目前只支援GET方法，但將來的版本可能允許HEAD或OPTIONS |
| 406 | 不可接受 | 表示客戶端請求了不支援的媒體類型 |
| 500 | 內部伺服器錯誤 | 「這永遠不應該發生」 |
| 503 | 服務不可用 | 向應用程式或其依賴項中的錯誤發出信號 |

## 資料格式 {#data-formats}

資料以下列格式提供：

* JSON（預設）
* XML
* CSV
* HTML（用於演示）

客戶端可以使用以下內容協商策略（優先順序由清單中的位置指定 — 首先）:

1. 附加到URL路徑最後一段的「檔案副檔名」：例如， `/esm/v2/media-company/year/month/day.xml`。 如果URL包含查詢字串，則副檔名必須位於問號之前： `/esm/v2/media-company/year/month/day.csv?mvpd= SomeMVPD`
1. 格式查詢字串參數：例如， `/esm/report?format=json`
1. 標準HTTP接受標頭：例如， `Accept: application/xml`

「extension」和查詢參數都支援以下值：

* xml
* jon
* csv
* html

如果任何策略都未指定媒體類型，則API將預設生成JSON內容。

## 超文本應用語言 {#hypertext-application-language}

對於JSON和XML，負載將編碼為HAL，如下所述：  <http://stateless.co/hal_specification.html>。

實際報告（稱為「report」的嵌套標籤/屬性）將由包含所有選定/適用維和度量及其值的記錄的實際清單組成，其編碼如下：

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

對於XML和JSON格式，記錄中欄位（維和度量）的順序未指定 — 但是一致（在所有記錄中順序將相同）。 但是，客戶端不應依賴記錄中欄位的任何特定順序。

資源連結（JSON中的&quot;self&quot; rel和XML中的&quot;href&quot;資源屬性）包含用於內聯報表的當前路徑和查詢字串。 查詢字串將顯示所有隱式和顯式參數，以便負載將顯式指出使用的時間間隔、隱式篩選器（如果有）等。 資源中的其餘連結將包含所有可用段，這些段可以隨後進行，以便在當前資料中進行細化。 還將提供用於匯總的連結，並指向父路徑（如果有）。 的 `href` 下鑽/上滾連結的值僅包含URL路徑（它不包含查詢字串，因此如果需要，客戶端需要附加該路徑）。 請注意，當前資源使用（或隱含）的查詢字串參數並非全部都適用於「匯總」或「下鑽」連結（例如，篩選器可能不適用於子資源或超級資源）。

示例(假設我們有一個稱為 `clients` 並且有一個預聚合 `year/month/day/...`):

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

在CSV資料格式中，不會以內聯方式提供連結或其他元資料（標題行除外）;相反，將在檔案名中提供選擇元資料，該檔案名將遵循以下模式：

```CSV
    esm__<start-date>_<end-date>_<filter-values,...>.csv
```

CSV將包含標題行，然後將報告資料作為後續行。 標題行將包含所有維，後面跟所有度量。 報表資料的排序順序將反映在維的順序中。 因此，如果資料按 `D1` 然後 `D2`,CSV標題將如下所示： `D1, D2, ...metrics...`。

標題行中欄位的順序將反映表資料的排序順序。


示例：https://mgmt.auth.adobe.com/v2/year/month.csv將生成名為 `report__2012-07-20_2012-08-20_1000.csv` 內容：


| 年 | 月 | 客戶端 |
| ---- | :---: | ------- |
| 2012 | 6 | 580 |
| 2012 | 7 | 231 |

## 資料新鮮度 {#data-freshness}

成功的HTTP響應包含 `Last-Modified` 標題，指示上次更新正文中的報表的時間。 缺少上次修改的報頭表示報表資料是即時計算的。

通常，粗粒度資料的更新頻率比細粒度資料低（例如，按分鐘值或小時值可能比每日值更新，特別是對於不能基於較小粒度計算的度量，如唯一計數）。

未來版本的ESM可能允許客戶端通過提供標準「If-Modified-Sine」標頭來執行條件GET。

## GZIP壓縮 {#gzip-compression}

Adobe強烈建議在獲取ESM報告的客戶端中啟用gzip支援。 這樣做將大大減少響應的大小，這反過來會縮短您的響應時間。 （ESM資料的壓縮比在20-30範圍內。）

要在客戶端中啟用gzip壓縮，請設定 `Accept-Encoding:` 標題如下：

* 接受編碼：gzip,defla


<!--
## Related Information {#related-information}

- [ESM Overview](/help/authentication/entitlement-service-monitoring-overview.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Understanding Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->
