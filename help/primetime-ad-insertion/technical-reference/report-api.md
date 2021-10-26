---
title: 報表API
description: Auditude報表API
source-git-commit: 7f958c83a4dd481221feb4a266440b920ac7d195
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---


# 報表API {#report-api}

使用者介面為客戶和啟用(Adobe)團隊管理角色。 客戶可以存取入口網站，然後建立和編輯其設定。 使用者也可以在使用者介面上查看其廣告曝光次數的報表。

API在幕後運作，以便客戶和管理員與後端基礎架構通訊。

## API端點 {#report-api-endpoint}

### 生產 {#production}

`https://dai-primetime.adobe.io/report`

### 沙箱 {#sandbox}

`https://dai-sandbox1-primetime.adobe.io/report`

## 查詢參數


| 名稱 | 顯著性 | 值類型 | 強制？ | 預設值 | 限制 | 範例/有效範例值 |
|----------|-----------------------------------------------------------------------------------------------|----------------|----------------|---------------------|------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| endDate | 報表資料的結束日期 | 日期 | Y | 無 | 在UTC-8中不比昨天更新 | ####### |
| 篩選器 | 篩選一或多欄 | 字串 | N | 無 | ad_config_id , zone_id | ad_config_id=990,900;state=active |
|  |  |  |  |  | 當請求中的metaData設為「true」時，您也可以依名稱篩選。 |  |
|  |  |  |  |  |  | 多個篩選鍵以分號分隔。 |
|  |  |  |  |  |  | 使用逗號分隔值來提供篩選索引鍵的值清單 |
| groupBy | 依時間（年\|月\|日）或ad_config_id分組。 Adconfig是AdRule的同義詞。 | 字串 | N | 無 | y \| m \| d , ad_config_id | m , ad_config_id |
|  |  |  |  |  |  |  |
|  |  |  |  |  |  | 對於groupBy，按時提供y或m或d之一 |
|  |  |  |  |  |  |  |



## 標題 {#headers}

| 名稱 | 值類型 | 必填 | 範例值 | 顯著性 |
|-----------------------|----------------|---------------|-------------------------------------|------------------------------------|
| 接受 | 字串 | Y | CSV的文字/CSV | 應從API傳回的回應類型 |
|  |  |  | application/json或&#39;*/*&#39; for JSON |  |
| 授權Token | 字串 | Y | xy | 授權令牌 |
| x-api-key | 字串 | Y | xy | API金鑰 |
| x-gw-ims-org-id | 字串 | Y | xyz12345 | 您帳戶的IMS組織ID |

* 您可以依照Adobe.io的JWT驗證說明頁面中詳述的步驟，產生授權Token（也稱為存取Token）。
   >[!NOTE]
   >授權Token的到期時間為24小時，因此如果您使用循環指令碼的報表API，請務必在Token到期前或收到有關Token無效的Oauth錯誤時產生驗證Token。

* 若要在要求標題中設定正確值並產生授權Token（使用JWT驗證），您必須知道帳戶的下列設定。 請聯絡Primetime支援團隊以取得這些值。
技術帳戶ID

   * 組織ID
   * Api_key
   * Client_secret

## 輸出 {#output}

依預設，報表API查詢的結果為JSON格式，會針對請求的維度的不同值(groupby param)指定曝光數。 輸出範例如下：

```JSON
[
    {
        "dates": "07-2020",
        "total_impressions": 213007041
    },
    {
        "dates": "08-2020",
        "total_impressions": 174711626
    },
    {
        "dates": "09-2020",
        "total_impressions": 102863153
    }
]
```

## 錯誤代碼和字串 {#error-codes-strings}

### 錯誤回應格式 {#error-response-format}

呈現宏「代碼」時出錯：為參數指定的值無效 `com.atlassian.confluence.ext.code.render.InvalidValueException`

```Shell
{
"error_code": "<ERROR_CODE>",
"message": "<ERROR_MESSAGE>"
}
```

下表列出報表API可傳回的錯誤碼和訊息。 有關授權層的錯誤，請參閱 [錯誤代碼檔案](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#errors-and-troubleshooting) Adobe.io。

| 錯誤代碼 | 錯誤訊息 |
|-----------------------|------------------------------------------|
| 4001007 | 用戶詳細資訊無效。 |
| 4001008 | 所有區域都不是來自同一帳戶。 |
| 5001010 | 發生內部錯誤。 |
| 4001011 | 日期不會以必要格式傳送。 |
| 4001012 | 日期超出範圍。 |
| 4001013 | 缺少強制參數。 |
| 4001014 | 帳戶的區域清單為空。 |
| 4001015 | 請求中的篩選器密鑰無效。 |
| 4001016 | 請求中的GroupBy選項無效。 |
| 4001017 | 請求中提供的ID無效 |

## 呼叫範例和預期結果 {#sample-calls-expected-results}

以下是curl命令，可使用存取權杖取得2020-07-01和2021-06-30之間的每月曝光計數：

**報表API呼叫範例**

```shell
curl --location --request GET 'https://dai-sandbox1-primetime.adobe.io/report?startDate=2020-07-01&endDate=2021-06-30&groupBy=m&unpaged=true' \
--header 'x-api-key: <API_KEY>' \
--header 'x-gw-ims-org-id: <ORG_ID>' \
--header 'Authorization: Bearer <ACCESS_TOKEN_STRING>' \
--header 'Accept: application/json'
```

| 呼叫範例/使用案例 | 預期結果 |
|---|---|
| 以開始和結束日期擷取報表GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2021-01-01 header :接受= application/json。 或 */* | Json，包含下列參數，以及屬於此帳戶total_impressions的所有廣告 |
| 使用GroupBy = d \| m \| yGET擷取報表： [API_ENDPOINT]//report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d \| m \| y標題：接受= application/json。 或 */* | Json，包含下列參數，且所有廣告均屬於此帳戶日期（mm-dd-yyyy \| mm-yyyy \| yyyy格式）total_impressions |
| 使用GroupBy = ad_config_id擷取報表GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=ad_config_id標題：接受= application/json。 或 */* | Json，具有下列參數，以及屬於此帳戶ad_config_id total_impressions的所有廣告 |
| 使用GroupBy = d \| m \| y和ad_config_idGET擷取報表： [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d,ad_config_id標題：接受= application/json。 或 */* | Json，包含下列參數，且所有廣告均屬於此帳戶ad_config_id日期（mm-dd-yyyy \| mm-yyyy \| yyyy格式）total_impressions |
| 擷取含有metaData=true和groupBy=d \| m \| yGET的報表： [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=ad_config_id標題：接受= application/json。 或 */* | Json，具有下列參數，以及屬於此帳戶ad_config_id名稱total_impressions的所有廣告 |
| 以groupBy=d \| m \| y和ad_config_idGET擷取報表： [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=d \| m \| y,ad_config_id標題：接受= application/json。 或 */* | Json，包含下列參數，且所有廣告均屬於此帳戶ad_config_id名稱total_impressions日期（mm-dd-yyyy \| mm-yyyy \| yyyy格式） |
| 擷取報表以取得指定日期範圍內的所有列（未分頁= true）GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;groupBy=d&amp;unpaged=true | 傳回Json陣列中的31個項目 |
| 使用有效的頁面查詢參數擷取報表GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;page=0&amp;size=5&amp;groupBy=d | 傳回陣列中的5個項目 |
| 以csv格式擷取報表GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10 header :接受=文字/csv | 會傳回CSV字串，並帶有標題：total_impressions |
| 以csv格式擷取報表，而groupBy = d \| m \| yGET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;groupBy=d\|m\|y標題：接受=文字/csv | 會傳回CSV字串，並帶有標題：total_impressions日期（mm-dd-yyyy \| mm-yyyy \| yyyy格式） |
| 以csv格式擷取報表，而中繼資料= trueGET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true header :接受=文字/csv | 會傳回CSV字串，並帶有標題：total_impressions |
| 以csv格式擷取報表，中繼資料= true，而groupBy = d \| m \| yGET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true&amp;groupBy=d\|m\|y標題：接受=文字/csv | 會傳回CSV字串，並帶有標題：total_impressions日期（mm-dd-yyyy \| mm-yyyy \| yyyy格式） |


## 報告API限制策略 {#report-api-throttling-policy}

* 每個使用者在5秒的期間內，允許5個API請求。
* 如果使用者超過上限，回應會延遲5秒。
* 如果使用者在5秒內發出超過10個呼叫，就會開始以「429個請求太多」回應拒絕。
