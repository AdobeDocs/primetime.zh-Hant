---
title: 報告API
description: 審核報告API
exl-id: 50eb4869-3765-4591-8c41-794b29d50044
source-git-commit: 628544e38616715e83e0274ba26cf93302ce0e61
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 1%

---

# 報告API {#report-api}

用戶介面為客戶和啟用(Adobe)團隊提供了托管角色。 客戶可以訪問門戶，然後可以建立和編輯其配置。 還可以在用戶介面上看到廣告印象的報告。

API在幕後工作，以便客戶和管理員與後端基礎架構通信。

瀏覽 [!DNL Primetime Ad Insertion] API請參見 [Ad Insertion配置用戶介面中的API端點](https://adconfigservice-va6.cloud.adobe.io/swagger-ui/index.html#/)。

## API終結點 {#report-api-endpoint}

### 生產 {#production}

`https://dai-primetime.adobe.io/report`

### 沙盒 {#sandbox}

`https://dai-sandbox1-primetime.adobe.io/report`

## 查詢參數


| 名稱 | 意義 | 值類型 | 強制？ | 預設值 | 約束 | 示例/有效示例值 |
|----------|-----------------------------------------------------------------------------------------------|----------------|----------------|---------------------|------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| 結束日期 | 報表資料的結束日期 | 日期 | Y | 無 | 不比UTC-8中的昨天新 | ###### |
| 篩選 | 篩選一個或多個列 | 字串 | N | 無 | ad_config_id,zone_id | ad_config_id=990,900;state=active |
|  |  |  |  |  | 在請求中將metaData設定為「true」時，您也可以按名稱進行篩選。 |  |
|  |  |  |  |  |  | 多個篩選器鍵以分號分隔。 |
|  |  |  |  |  |  | 使用逗號分隔的值來提供篩選器鍵的值清單 |
| 分組依據 | 按時間分組（年\|月\|天）或ad_config_id。 Adconfig是AdRule的同義詞。 | 字串 | N | 無 | y \| m \| d,ad_config_id | m,ad_config_id |
|  |  |  |  |  |  |  |
|  |  |  |  |  |  | 對於groupBy按時提供y或m或d之一 |
|  |  |  |  |  |  |  |



## 標題 {#headers}

| 名稱 | 值類型 | 強制 | 示例值 | 意義 |
|-----------------------|----------------|---------------|-------------------------------------|------------------------------------|
| 接受 | 字串 | Y | CSV文本/csv | 應從API響應的類型 |
|  |  |  | 應用程式/json或&#39;*/*&#39;用於JSON |  |
| 授權令牌 | 字串 | Y | x | 授權令牌 |
| x-api鍵 | 字串 | Y | x | API密鑰 |
| x-gw-ims-org-id | 字串 | Y | xyz12345 | 帳戶的IMS組織ID |

* 您可以按照Adobe.io的JWT驗證幫助頁中詳細介紹的步驟來生成授權令牌（也稱為訪問令牌）。
   >[!NOTE]
   >授權令牌的到期時間為24小時，因此，如果您使用的是循環指令碼的報表API，請確保在授權令牌到期之前或當您收到有關令牌無效的Oauth錯誤時生成授權令牌。

* 要在請求標頭中設定正確的值並生成授權令牌（使用JWT驗證），您需要瞭解帳戶的以下配置。 請與黃金時段支援團隊聯繫以獲取這些價值。
技術帳戶ID

   * 組織ID
   * API鍵(_K)
   * 客戶端密鑰

## 輸出 {#output}

預設情況下，Report API查詢的結果為JSON格式，它根據所請求的維(groupby param)的不同值指定印數。 輸出示例如下：

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

### 錯誤響應格式 {#error-response-format}

呈現宏「code」時出錯：為參數指定的值無效 `com.atlassian.confluence.ext.code.render.InvalidValueException`

```Shell
{
"error_code": "<ERROR_CODE>",
"message": "<ERROR_MESSAGE>"
}
```

下表列出了Report API可以返回的錯誤代碼和消息。 有關授權層的錯誤，請參閱 [錯誤代碼文檔](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#errors-and-troubleshooting) Adobe。

| 錯誤代碼 | 錯誤消息 |
|-----------------------|------------------------------------------|
| 4001007 | 用戶詳細資訊無效。 |
| 4001008 | 所有區域都不是來自同一帳戶。 |
| 5001010 | 發生內部錯誤。 |
| 4001011 | 日期未以所需格式發送。 |
| 4001012 | 日期超出範圍。 |
| 4001013 | 缺少必需參數。 |
| 4001014 | 帳戶的區域清單為空。 |
| 4001015 | 請求中的篩選器鍵無效。 |
| 4001016 | 請求中的GroupBy選項無效。 |
| 4001017 | 請求中提供了無效ID |

## 示例調用和預期結果 {#sample-calls-expected-results}

以下是使用訪問令牌獲取2020-07-01和2021-06-30之間月印度計數的curl命令：

**報告API調用示例**

```shell
curl --location --request GET 'https://dai-sandbox1-primetime.adobe.io/report?startDate=2020-07-01&endDate=2021-06-30&groupBy=m&unpaged=true' \
--header 'x-api-key: <API_KEY>' \
--header 'x-gw-ims-org-id: <ORG_ID>' \
--header 'Authorization: Bearer <ACCESS_TOKEN_STRING>' \
--header 'Accept: application/json'
```

| 示例呼叫/使用案例 | 預期結果 |
|---|---|
| 提取具有開始日期和結束日期的報告GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2021-01-01標頭：接受=應用程式/json。 或 */* | 具有以下參數的Json（所有廣告均屬於此帳戶total_impress） |
| GroupBy = d \| m \| yGET的讀取報告： [API_ENDPOINT]//report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d \| m \| y標頭：接受=應用程式/json。 或 */* | 具有以下參數的Json，所有廣告均屬於此帳戶日期（mm-dd-yyyy \|mm-yyyy \|yyyy格式）total_impression |
| GroupBy = ad_config_idGET的提取報告： [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=ad_config_id頭：接受=應用程式/json。 或 */* | 包含以下參數的Json（所有廣告均屬於此帳戶ad_config_id total_impressions） |
| GroupBy = d \| m \| y和ad_config_idGET的讀取報告： [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d,ad_config_id標頭：接受=應用程式/json。 或 */* | 具有以下參數的Json，所有廣告均屬於此帳戶ad_config_id日期（mm-dd-yyyy \|mm-yyyy \|yyyy格式）total_impression |
| metaData=true和groupBy=d \| m \| yGET的讀取報告： [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=ad_config_id頭：接受=應用程式/json。 或 */* | Json具有以下參數，所有廣告均屬於此帳戶ad_config_id name total_impress |
| groupBy=d \| m \| y和ad_config_idGET的獲取報告： [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=d \| m \| y,ad_config_id頭：接受=應用程式/json。 或 */* | 具有以下參數的Json，所有廣告均屬於此帳戶ad_config_id名稱total_impression日期（mm-dd-yyyy \|mm-yyyy \|yyyy格式） |
| 獲取報告以獲取給定日期範圍的所有行（未分頁= true）GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;groupBy=d&amp;unpaged=true | 返回的Json陣列中的31個條目 |
| 具有有效頁查詢參數的獲取報表GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;page=0&amp;size=5&amp;groupBy=d | 返回的陣列中有5個條目 |
| 獲取報告，採用csv格式GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10標頭：接受=文本/csv | 返回CSV字串，其標題為：總印象 |
| Fetch Report（csv格式）和groupBy = d \| m \| yGET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;groupBy=d\|m\|y標頭：接受=文本/csv | 返回CSV字串，其標題為：總印象日期（mm-dd-yyyy \|mm-yyyy \|yyyy格式） |
| 使用csv格式和元資料=真GET的獲取報告： [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true標頭：接受=文本/csv | 返回CSV字串，其標題為：總印象 |
| 使用csv格式、元資料=true和groupBy = d \| m \| yGET獲取報告： [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true&amp;groupBy=d\|m\|y標頭：接受=文本/csv | 返回CSV字串，其標題為：總印象日期（mm-dd-yyyy \|mm-yyyy \|yyyy格式） |


## 報告API限制策略 {#report-api-throttling-policy}

* 每個用戶在5秒的窗口內允許5個API請求。
* 如果用戶超出限制，則響應延遲5秒。
* 如果用戶在5秒內撥打了10個以上的呼叫，將開始以「429請求太多」的響應被拒絕。
