---
title: 報表API
description: 稽核報表API
exl-id: 50eb4869-3765-4591-8c41-794b29d50044
source-git-commit: 628544e38616715e83e0274ba26cf93302ce0e61
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 1%

---

# 報表API {#report-api}

使用者介面已管理客戶和啟用(Adobe)團隊的角色。 客戶可以存取入口網站，然後可以建立和編輯其設定。 他們也可以從使用者介面檢視其廣告印象的報告。

API會在幕後運作，方便客戶和管理員與後端基礎架構通訊。

若要探索 [!DNL Primetime Ad Insertion] API請參閱 [在swaggered使用者介面中Ad InsertionAPI端點](https://adconfigservice-va6.cloud.adobe.io/swagger-ui/index.html#/).

## API端點 {#report-api-endpoint}

### 生產 {#production}

`https://dai-primetime.adobe.io/report`

### Sandbox {#sandbox}

`https://dai-sandbox1-primetime.adobe.io/report`

## 查詢引數


| 名稱 | 重要性 | 值型別 | 強制？ | 預設值 | 限制 | 範例/有效的範例值 |
|----------|-----------------------------------------------------------------------------------------------|----------------|----------------|---------------------|------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| endDate | 報表資料的結束日期 | 日期 | Y | 無 | UTC-8中的時間不比昨天晚 | ######## |
| 篩選器 | 在一或多個欄上篩選 | 字串 | N | 無 | ad_config_id ， zone_id | ad_config_id=990,900；state=active |
|  |  |  |  |  | 當請求中的metaData設為「true」時，您也可以依名稱篩選。 |  |
|  |  |  |  |  |  | 多個篩選鍵以分號分隔。 |
|  |  |  |  |  |  | 使用逗號分隔值來提供篩選索引鍵的值清單 |
| groupBy | 分組依據：時間（年\|月\|日）或ad_config_id。 Adconfig是AdRule的同義字。 | 字串 | N | 無 | y \| m \| d ， ad_config_id | m ， ad_config_id |
|  |  |  |  |  |  |  |
|  |  |  |  |  |  | 若為groupBy on time，請提供y、m或d其中之一 |
|  |  |  |  |  |  |  |



## 標頭 {#headers}

| 名稱 | 值型別 | 強制 | 範例值 | 重要性 |
|-----------------------|----------------|---------------|-------------------------------------|------------------------------------|
| Accept | 字串 | Y | CSV適用的text/csv | API應有的回應型別 |
|  |  |  | application/json或&#39;*/*&#39;適用於JSON |  |
| 授權權杖 | 字串 | Y | xyz | 授權權杖 |
| x-api-key | 字串 | Y | xyz | API金鑰 |
| x-gw-ims-org-id | 字串 | Y | xyz12345 | 您帳戶的IMS組織ID |

* 您可以依照Adobe.io的JWT驗證說明頁面中詳述的步驟來產生授權權杖（也稱為存取權杖）。
   >[!NOTE]
   >授權權杖有24小時的到期日，因此，如果您使用週期性指令碼來使用Report API，則請確保在授權權杖到期前或當您收到有關權杖無效的Oauth錯誤時產生授權權杖。

* 若要在請求標頭中設定正確的值並產生授權權杖（使用JWT驗證），您需要知道您帳戶的以下設定。 請聯絡Primetime支援團隊以取得這些值。
技術帳戶ID

   * 組織ID
   * Api_key
   * Client_secret

## 輸出 {#output}

報表API查詢的結果預設為JSON格式，這會針對請求的維度（groupby引數）的不同值指定曝光次數。 範例輸出如下所示：

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

## 錯誤碼和字串 {#error-codes-strings}

### 錯誤回應格式 {#error-response-format}

產生巨集&#39;code&#39;時發生錯誤：為引數指定的值無效 `com.atlassian.confluence.ext.code.render.InvalidValueException`

```Shell
{
"error_code": "<ERROR_CODE>",
"message": "<ERROR_MESSAGE>"
}
```

下表列出Report API可傳回的錯誤碼和訊息。 有關授權層的相關錯誤，請參閱 [錯誤代碼檔案](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#errors-and-troubleshooting) 的Adobe.io.

| 錯誤代碼 | 錯誤訊息 |
|-----------------------|------------------------------------------|
| 4001007 | 使用者詳細資料無效。 |
| 4001008 | 所有區域並非來自相同帳戶。 |
| 5001010 | 發生內部錯誤。 |
| 4001011 | 日期未以要求的格式傳送。 |
| 4001012 | 日期超出範圍。 |
| 4001013 | 遺失必要引數。 |
| 4001014 | 帳戶的區域清單是空的。 |
| 4001015 | 請求中的篩選索引鍵無效。 |
| 4001016 | 請求中的GroupBy選項無效。 |
| 4001017 | 請求中提供了無效的ID |

## 呼叫範例和預期結果 {#sample-calls-expected-results}

以下是curl命令，可使用存取權杖來取得2020-07-01和2021-06-30之間的每月曝光計數：

**報表API呼叫範例**

```shell
curl --location --request GET 'https://dai-sandbox1-primetime.adobe.io/report?startDate=2020-07-01&endDate=2021-06-30&groupBy=m&unpaged=true' \
--header 'x-api-key: <API_KEY>' \
--header 'x-gw-ims-org-id: <ORG_ID>' \
--header 'Authorization: Bearer <ACCESS_TOKEN_STRING>' \
--header 'Accept: application/json'
```

| 呼叫/使用案例範例 | 預期結果 |
|---|---|
| 具有開始和結束日期GET的擷取報表： [API端點]/report？startDate=2020-01-01&amp;endDate=2021-01-01標頭：接受= application/json。 或 */* | Json及其下列引數，以及屬於此帳戶total_impressions的所有廣告 |
| 以GroupBy = d \| m \| yGET擷取報表： [API端點]//report？startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d \| m \| y標頭：接受= application/json。 或 */* | Json，包含下列引數以及屬於此帳戶日期(mm-dd-yyyy \| mm-yyyy \| yyyy format) total_impressions |
| 以GroupBy = ad_config_idGET擷取報表： [API端點]/report？startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=ad_config_id標頭：接受= application/json。 或 */* | Json及其下列引數，以及屬於此帳戶ad_config_id total_impressions的所有廣告 |
| 以GroupBy = d \| m \| y和ad_config_idGET擷取報表： [API端點]/report？startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d，ad_config_id標頭：接受= application/json。 或 */* | Json，包含下列引數以及屬於此帳戶ad_config_id日期的所有廣告(mm-dd-yyyy \| mm-yyyy \| yyyy format) total_impressions |
| Fetch Report with metaData=true and groupBy=d \| m \| yGET： [API端點]/report？startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=ad_config_id標頭：接受= application/json。 或 */* | Json包含下列引數，以及屬於此帳戶ad_config_id名稱total_impressions的所有廣告 |
| 使用groupBy=d \| m \| y和ad_config_idGET擷取報表： [API端點]/report？startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=d \| m \| y，ad_config_id標頭：接受= application/json。 或 */* | Json，包含下列引數以及屬於此帳戶ad_config_id名稱total_impressions日期（mm-dd-yyyy \| mm-yyyy \| yyyy格式） |
| 擷取報告以取得指定日期範圍的所有列（未分頁= true）GET： [API端點]/report？startDate=2020-01-01&amp;endDate=2020-01-31&amp;groupBy=d&amp;unpaged=true | 傳回Json陣列中的31個專案 |
| 使用有效頁面查詢引數擷取報表GET： [API端點]/report？startDate=2020-01-01&amp;endDate=2020-01-31&amp;page=0&amp;size=5&amp;groupBy=d | 傳回陣列中的5個專案 |
| 以csv格式GET擷取報表： [API端點]/report？startDate=2020-01-01&amp;endDate=2020-01-10標頭：接受=文字/csv | 傳回CSV字串，並帶有標題： total_impressions |
| 以csv格式擷取報表，且groupBy = d \| m \| yGET： [API端點]/report？startDate=2020-01-01&amp;endDate=2020-01-10&amp;groupBy=d\|m\|y標頭：接受=文字/csv | 傳回CSV字串，標頭： total_impressions日期（mm-dd-yyyy \| mm-yyyy \| yyyy格式） |
| 擷取報表（使用csv格式），且中繼資料= trueGET： [API端點]/report？startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true標頭：接受=文字/csv | 傳回CSV字串，並帶有標題： total_impressions |
| 擷取報表，使用csv格式、metadata = true和groupBy = d \| m \| yGET： [API端點]/report？startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true&amp;groupBy=d\|m\|y標頭：接受=文字/csv | 傳回CSV字串，標頭： total_impressions日期（mm-dd-yyyy \| mm-yyyy \| yyyy格式） |


## 報表API節流原則 {#report-api-throttling-policy}

* 每個使用者可在5秒的視窗內提出5個API請求。
* 如果使用者超過限制，回應會延遲5秒。
* 如果使用者在5秒的範圍內進行超過10次呼叫，他們將開始被拒絕並回應「429太多請求」。
