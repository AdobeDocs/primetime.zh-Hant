---
title: 促銷臨時傳遞
description: 促銷臨時傳遞
exl-id: 705c1ba9-0430-4e3b-add1-d9e4da3f82d1
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1523'
ht-degree: 0%

---

# 促銷臨時傳遞 {#promotional-temp-pass}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 功能摘要 {#feature-summary}

促銷臨時通行證可讓程式設計師為沒有MVPD帳戶憑證的使用者提供對其受保護內容的暫時存取權。

促銷臨時通行證設計用於執行促銷活動，讓使用者在提供有效的識別資訊（例如電子郵件地址）給程式設計師之後，能夠使用 **預先定義的一段時間內不同VOD標題的預定義數量**.

>[!IMPORTANT]
>
>Adobe不會儲存任何個人識別資訊(PII)。 因此，程式設計師必須在唯一使用者提供的Primetime驗證API資訊上設定雜湊。

促銷臨時通行證是建立在 [暫時通過](/help/authentication/temp-pass.md) 功能，表示其中包含所有「暫時通過」功能。

一旦超過預先定義的最大VOD標題數量或預先定義的時間段，該使用者將無法存取相同裝置上的內容，或是使用相同的使用者識別碼資訊（例如，電子郵件地址），直到從Adobe Primetime驗證伺服器清除授權權杖為止。

>[!NOTE]
>
>Temp Pass是Premium Workflow封裝的一部分。 如果您有興趣使用此功能，請聯絡您的Primetime銷售代表。

## 暫時通過和促銷暫時通過比較 {#tp-ptp-comparison}

| 暫時通過 | 促銷臨時傳遞 |
|----------------------------------|----------------------------------------------------------------------------------------|
| 存取內容 <ul><li>基於時間</li></ul> | 存取內容 <ul><li>基於時間</li><li>根據資源數量</li></ul> |
| 存取安全性依據 <ul><li>裝置ID</li></ul> | 安全性依據 <ul><li>裝置ID</li><li>雜湊超過提供的使用者識別碼資訊（例如電子郵件）</li></ul> |
| 可用的使用者端錯誤API | 可用的使用者端錯誤API |
| 可重設/永久刪除 | 可重設/永久刪除 |

## 功能詳細資料 {#feature-details}

使用者在程式設計人員的應用程式中提供唯一資訊（例如電子郵件地址）後，可使用此功能從特定裝置（電話和平板電腦）存取促銷內容。

程式設計師將會在驗證和授權API上使用者的PII上提供雜湊。 此雜湊將與裝置ID搭配使用，以產生唯一索引鍵來識別使用者和裝置。

Adobe Primetime驗證會根據裝置ID和使用者提供的資訊，並依照下列邏輯判斷使用者是否處於新的試用期或現有試用期：

* 使用者提供資訊的新雜湊（例如電子郵件）、新裝置ID =>新試用版
* 現有雜湊覆蓋使用者提供的資訊（例如電子郵件）、新裝置ID =>現有試用版(搭配現有雜湊覆蓋使用者提供的資訊（例如電子郵件）)
* 透過使用者提供的資訊（例如電子郵件）新增雜湊、現有裝置ID =>現有試用版（含現有裝置ID）
* 現有雜湊會覆蓋使用者提供的資訊（例如電子郵件）、現有裝置ID =>現有試用版

>[!NOTE]
>使用者提供資訊的驗證和雜湊是由程式設計師處理，而非Adobe。

**可依據下列屬性來設定「促銷臨時通過」功能：**

* 使用者提供的資訊金鑰（例如電子郵件）
* 使用者有權使用的資源數
* TTL — 使用者有權使用已設定資源數的時間範圍

### 使用者中繼資料 {#user-metadata}

為了加速程式設計師應用程式的實作，請完成以下步驟 **使用者中繼資料資訊會公開** 在「促銷臨時通行證」上，使用對應的金鑰(若要啟用金鑰，請連絡tve-support@adobe.com)：

* **remain_resources**：目前使用者有權使用的剩餘資源數
* **used_assets**：目前使用者已使用的資源清單
* **expiration_date**：目前使用者的到期日

### 如何計算檢視時間？ {#compute-viewing-time}

臨時通行證保持有效的時間與使用者在程式設計人員應用程式上檢視內容所花費的時間無關。 在使用者透過「提升臨時通過」提出授權要求時，到期時間計算方式是將初始目前要求時間加到程式設計師指定的TTL （持續時間時間範圍）。

### 驗證和授權 {#authn-authz}

對於「促銷臨時通過」流程，驗證和授權不會與實際MVPD通訊， **所以所有授權要求都會成功** 只要符合以下所有條件：

* 授權權杖對指定資源有效
* 數量 **used_assets** 低於程式設計師設定的限制
* **expiration_date** 值在目前日期之後。

### 預檢行為 {#preflight-beh}

當針對「促銷臨時通過」MVPD提出預檢或預授權要求時，傳回的對應預檢回應將包含來自預檢要求的完整資源清單，因為預檢成功。

其背後的邏輯是：「促銷臨時通過」授權條件是根據時間和資源數量限制，而不是根據特定資源。 更具體地說，只要符合時間限制且未超過資源限制，呼叫的資源就會獲得授權。

### SSO {#sso}

Promotional Temp Pass的執行個體不會啟用SSO，此執行個體已設定為啟用「每個請求者的驗證」。 這表示當使用者從應用程式A切換至與同一促銷臨時傳遞整合的另一個應用程式B時，使用者不會自動登入。

### 登出 {#logout}

登出時會刪除裝置上的所有Token。 因此，從「促銷臨時傳遞」切換至一般使用者選取的MVPD不應依賴此實作。 建議使用 `setSelectedProvider(null)` 功能以清除應用程式狀態，然後重新啟動驗證流程，這樣會提供更佳的使用者體驗。

### 促銷暫存通過流程圖 {#promo-tempass-flowdia}

![促銷暫存通過流程圖](assets/promo-temp-pass-flow.png)

*圖：促銷暫存通過流程*

## 實作促銷臨時傳遞 {#impl-promo-tempass}

促銷臨時傳遞需要下列使用者端功能：

* **使用者識別碼資訊，例如電子郵件地址傳播** （在驗證和授權流程上傳送使用者的電子郵件地址）。 Adobe Primetime驗證需要電子郵件來繫結驗證和授權權杖(類似於 `device_ID`，在所有呼叫上為必要)。
* **強制驗證**  — 允許程式設計師在使用者已驗證時強制驗證流程。 若要強制使用者中繼資料重新整理（使用者中繼資料索引鍵），需要使用此功能 **used_assets** 包含可用資源的數量)。 由於使用者可在多部裝置上登入，因此應用程式啟動期間裝置上呈現的使用者中繼資料並不可靠，我們需要更新該中繼資料，以反映該特定使用者的目前狀態（以電子郵件地址識別）。


>[!IMPORTANT]
>僅可在iOS和Android上強制驗證。
>Primetime驗證沒有內建機制可在X分鐘後停止免費串流。 Primetime驗證將停止發行 **授權** 和 **短媒體** Token當使用者消耗Y可用資源時。 在「促銷臨時通過」過期後，由程式設計師來限制存取權。

## 安全性 {#security}

>[!IMPORTANT]
>Adobe不會儲存任何個人識別資訊(PII)。 因此，程式設計師必須在唯一使用者提供的Primetime驗證API資訊上設定雜湊。

**使用者識別碼資訊的雜湊處理**

Adobe建議使用 **SHA-2** 系列或其特定 **SHA-256**， **SHA-512** 會在資料傳送至Adobe前對其執行函式。

例如， **SHA-256** 超過 **&quot;user@domain.com&quot;** 是 **&quot;f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&quot;**.

## 重設或永久刪除促銷臨時傳遞 {#reset-promo-tempass}

某些商業規則需要定期清除「促銷臨時通行證」。 為了做到這一點，Primetime驗證向程式設計師提供 *公共* Web API，如下所述：

| `DELETE https://mgmt.auth.adobe.com/reset-tempass/v2/reset` |
|----|
| <ul><li>通訊協定： **https**</li><li>主機：<ul><li>發行版本： **mgmt.auth.adobe.com**</li><li>先決條件： **mgmt-prequal.auth.adobe.com**</li></ul></li><li>路徑： **/reset-tempass/v2/reset**</li><li>查詢引數： **device_id=all&amp;requestor_id=THE_REQUESTOR_ID&amp;mvpd_id=THE_TEMPASS_MVPD_ID**</li><li>標頭： ApiKey： **1232293681726481**</li> <li>回應：<ul><li>成功： **HTTP 204**</li><li>失敗： **HTTP 400** 對於不正確的請求， **HTTP 401** 如果未指定ApiKey， **HTTP 403** 如果ApiKey無效</li></ul></li></ul> |

除了永久刪除「臨時通過」的需求外，「促銷臨時通過」還會使用雜湊來取代傳送為的使用者識別碼資訊 **generic_data** 進行驗證和授權以便清除。

將會傳送雜湊，而非整個JSON：

```cURL
$ curl -X DELETE -H "Authorization:Bearer H4j7cF3GtJX81BrsgDa10GwSizVz" "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset/generic?key=f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&requestor_id=REF&mvpd_id=FlexibleTempPass"
```

### 支援的使用者端 {#supported-clients}

| Adobe Primetime驗證使用者端 | 促銷臨時傳遞 | 重設工具 | 支援專用回應代碼/使用者端錯誤 |
|:--------------------------------------:|:---------------------:|:----------:|:-----------------------------------------------:|
| JS Access Enabler | 是 | 是 | 是（從3.0.0版開始） |
| Native Client iOS | 是 | 是 | 是（從v 1.10開始） |
| Native Client Android | 是 | 是 | 是 |
| 無使用者端API | 是 | 是 | 否 |


## 限制 {#limitations}

本節說明適用於目前實作「促銷臨時通過」的限制。

### 無使用者端 {#lim-clientless}

**沒有唯一裝置ID的智慧裝置**

並非所有智慧型裝置應用程式都能提供不重複裝置ID。 若無裝置識別碼，Adobe Primetime驗證可使用Adobe註冊代碼服務產生的UUID作為唯一裝置ID。 這表示當使用者登出時，將會刪除驗證和授權Token。 一旦使用者將嘗試再次驗證，這次使用不同的使用者資訊（例如，電子郵件）使用者將能夠再次授權。 Adobe建議新增UI流程，該流程不允許使用者「愚弄」系統，並且新增邏輯來判斷它是新使用者請求試用版還是現有試用版。

**重設/永久刪除暫時傳遞**

Xbox360和Xbox One的特定情況下無法使用無使用者端的「重設暫存通道」，因為這些平台需要額外的裝置ID剖析，而「重設暫存通道」工具則無法使用。

<!--
>[!RELATEDINFORMATION]
>
>* [Preflight Authorization](/help/authentication/preflight-authz.md)
-->
