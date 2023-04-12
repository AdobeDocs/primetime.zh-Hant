---
title: 促銷臨時通道
description: 促銷臨時通道
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1523'
ht-degree: 0%

---


# 促銷臨時通道 {#promotional-temp-pass}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 功能摘要 {#feature-summary}

促銷臨時通行證可讓程式設計人員為沒有MVPD帳戶憑證的使用者，提供對其受保護內容的暫時存取權。

促銷臨時通行證設計用於運行促銷活動，其中用戶在向程式設計師提供有效標識資訊（例如，電子郵件地址）之後，將能夠使用 **預先定義的時段內不同VOD標題的預先定義數量**.

>[!IMPORTANT]
>
>Adobe不會儲存任何個人識別資訊(PII)。 因此，程式設計師必須對唯一用戶提供的關於Primetime驗證API的資訊設定哈希。

促銷臨時通道建置在 [臨時通道](/help/authentication/temp-pass.md) 功能，表示包含所有「臨時傳遞」功能。

一旦超出最大預先定義的VOD標題數或預先定義的時間段，該使用者將無法存取相同裝置上的內容，或使用相同的使用者識別碼資訊（例如，電子郵件地址），直到授權Token從Adobe Primetime驗證伺服器中清除為止。

>[!NOTE]
>
>Temp Pass是Premium Workflow package的一部分。 如果您有興趣使用此功能，請連絡您的Primetime銷售代表。

## 臨時通道和促銷臨時通道比較 {#tp-ptp-comparison}

| 臨時通道 | 促銷臨時通道 |
|----------------------------------|----------------------------------------------------------------------------------------|
| 內容存取 <ul><li>時間型</li></ul> | 內容存取 <ul><li>時間型</li><li>根據資源數</li></ul> |
| 基於的訪問安全 <ul><li>裝置ID</li></ul> | 基於 <ul><li>裝置ID</li><li>雜湊而提供的使用者識別碼資訊（例如電子郵件）</li></ul> |
| 可用的客戶端錯誤API | 可用的客戶端錯誤API |
| 重置/清除可用 | 重置/清除可用 |

## 功能詳細資訊 {#feature-details}

在程式設計師應用程式中提供了唯一資訊（如電子郵件地址）之後，此功能使用戶能夠從特定設備（電話和平板電腦）訪問促銷內容。

程式設計師將在驗證和授權API上提供使用者PII的雜湊。 此雜湊會與裝置ID搭配使用，以產生唯一金鑰來識別使用者和裝置。

Adobe Primetime驗證會根據裝置ID和使用者提供的資訊，並遵循下列邏輯，判斷使用者是否在新試用版或現有試用版中：

* 使用者提供的資訊（例如電子郵件）的新雜湊、新裝置ID =>新試用版
* 現有散列（如電子郵件），新設備ID =>現有試用版(含現有散列（如電子郵件），而非用戶提供的資訊)
* 新雜湊，而非使用者提供的資訊（例如電子郵件）、現有裝置ID =>現有試用版（連同現有裝置ID）
* 現有雜湊，而非使用者提供的資訊（例如電子郵件），現有裝置ID =>現有試用版

>[!NOTE]
>用戶提供的資訊的驗證和散列由程式設計師處理，而不是由Adobe處理。

**可以根據以下屬性來配置Promotion Temp Pass功能：**

* 用戶提供的資訊密鑰（例如電子郵件）
* 用戶有權使用的資源數
* TTL — 使用者有權使用已設定資源數的時間範圍

### 使用者中繼資料 {#user-metadata}

為便於程式設計師應用程式的實施，以下 **公開使用者中繼資料資訊** 在Promotion Temp Pass上，使用相應的鍵(要激活鍵，請聯繫tve-support@adobe.com):

* **remaining_resources**:當前用戶有權使用的剩餘資源數
* **used_assets**:當前用戶已使用的資源清單
* **expiration_date**:目前使用者的到期日

### 如何計算查看時間？ {#compute-viewing-time}

臨時通行證的有效時間與用戶在程式設計師應用程式上查看內容所花的時間無關。 在通過促銷臨時通道對初始用戶請求授權時，通過將初始當前請求時間加到由程式設計師指定的TTL（持續時間時間幀）來計算到期時間。

### 驗證和授權 {#authn-authz}

對於促銷臨時通行流，驗證和授權不會與實際MVPD通訊， **所以所有授權請求都會成功** 只要滿足以下條件：

* 授權令牌對指定資源有效
* 數目 **used_assets** 低於程式設計師設定的限制
* **expiration_date** 值在目前日期之後。

### 預檢行為 {#preflight-beh}

當對促銷臨時通道MVPD提出預檢或預授權請求時，當預檢成功時，返回的相應預檢響應將包含預檢請求中的整個資源清單。

其背後的邏輯是：促銷臨時通過授權條件基於時間和資源編號限制，而非特定資源。 更具體地說，只要滿足時間限制，並且只要不超過資源限制，則將授權被調用的資源。

### SSO {#sso}

促銷臨時傳遞的例項未啟用SSO，而設定為「每個請求者驗證」。 這表示當用戶從應用程式A切換到另一個應用程式B（兩者都與相同的促銷臨時通行證整合）時，用戶將不會自動登錄。

### 登出 {#logout}

註銷時，將刪除設備上的所有令牌。 因此，從促銷臨時傳遞切換至一般使用者選取的MVPD時，不應依賴此實作。 建議使用 `setSelectedProvider(null)` 功能，以便清除應用程式狀態，然後重新啟動驗證流程，有更好的使用者體驗。

### 提升臨時通行證流程圖 {#promo-tempass-flowdia}

![提升臨時通行證流程圖](assets/promo-temp-pass-flow.png)

*圖：提升臨時流*

## 實作促銷臨時傳遞 {#impl-promo-tempass}

促銷臨時通行證需要下列用戶端功能：

* **用戶標識符資訊，例如電子郵件地址傳播** （在驗證和授權流程上傳送使用者的電子郵件地址）。 Adobe Primetime驗證需要電子郵件來系結驗證和授權Token(類似於 `device_ID`，所有呼叫都為必要)。
* **強制驗證**  — 允許程式設計師在用戶已經通過身份驗證時強制進行身份驗證流程。 若要強制重新整理使用者中繼資料（使用者中繼資料索引鍵），需要此功能 **used_assets** 包含可用資源的數量)。 由於使用者可以在多部裝置上登入，因此應用程式啟動期間裝置上顯示的使用者中繼資料不可靠，因此我們需要更新，以反映該特定使用者的目前狀態（以電子郵件地址識別）。


>[!IMPORTANT]
>只有iOS和Android才能強制驗證。
>Primetime驗證沒有內建機制可在X分鐘過後停止免費串流。 Primetime驗證將停止發行 **授權** 和 **短媒體** 使用者取用Y可用資源時代號。 升級臨時通行證過期後，程式設計師就可以限制訪問。

## 安全性 {#security}

>[!IMPORTANT]
>Adobe不會儲存任何個人識別資訊(PII)。 因此，程式設計師必須對唯一用戶提供的關於Primetime驗證API的資訊設定哈希。

**用戶標識符資訊的散列**

Adobe建議使用 **SHA-2** 家庭或特定 **SHA-256**, **SHA-512** 函式，再傳送至Adobe。

例如， **SHA-256** over **&quot;user@domain.com&quot;** is **&quot;f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&quot;**.

## 重置或清除促銷臨時通道 {#reset-promo-tempass}

某些業務規則需要定期清除促銷臨時通行證。 為此，Primetime驗證為程式設計人員提供 *公共* 網頁API，說明如下：

| `DELETE https://mgmt.auth.adobe.com/reset-tempass/v2/reset` |
|----|
| <ul><li>協定： **https**</li><li>主機：<ul><li>發行： **mgmt.auth.adobe.com**</li><li>前置詞： **mgmt-prequal.auth.adobe.com**</li></ul></li><li>路徑： **/reset-tempass/v2/reset**</li><li>查詢參數： **device_id=all&amp;requestor_id=THE_REQUESTOR_ID&amp;mvpd_id=THE_TEMPASS_MVPD_ID**</li><li>標題：ApiKey: **1232293681726481**</li> <li>回應：<ul><li>成功： **HTTP 204**</li><li>失敗： **HTTP 400** 對於錯誤的請求， **HTTP 401** 如果未指定ApiKey, **HTTP 403** 如果ApiKey無效</li></ul></li></ul> |

除了清除臨時通行證的要求外，促銷臨時通行證還使用雜湊，而不使用傳送為 **generic_data** 驗證和清除授權。

會傳送雜湊，而非整個JSON:

```cURL
$ curl -X DELETE -H "Authorization:Bearer H4j7cF3GtJX81BrsgDa10GwSizVz" "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset/generic?key=f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&requestor_id=REF&mvpd_id=FlexibleTempPass"
```

### 支援的用戶端 {#supported-clients}

| Adobe Primetime驗證用戶端 | 促銷臨時通道 | 重設工具 | 支援專用的響應代碼/客戶端錯誤 |
|:--------------------------------------:|:---------------------:|:----------:|:-----------------------------------------------:|
| JS Access Enabler | 是 | 是 | 是（從3.0.0版開始） |
| 本機用戶端iOS | 是 | 是 | 是（從1.10版開始） |
| 原生用戶端Android | 是 | 是 | 是 |
| 無用戶端API | 是 | 是 | 否 |


## 限制 {#limitations}

本節說明適用於目前實施促銷臨時通行證的限制。

### 無用戶端 {#lim-clientless}

**沒有唯一裝置ID的智慧型裝置**

並非所有智慧裝置應用程式都能提供唯一裝置ID。 如果沒有UUID,Adobe Primetime驗證可使用Adobe註冊程式碼服務產生的UUID做為唯一裝置ID。 這表示當使用者登出時，驗證和授權Token將會刪除。 一旦用戶嘗試再次驗證，這一次，用戶將能夠再次授權使用不同的用戶資訊（例如，電子郵件）。 Adobe建議新增UI流程，不允許使用者「愚弄」系統，並新增邏輯以判斷其為要求試用的新使用者或現有試用。

**重置/清除臨時通道**

在Xbox360和Xbox One的特定情況下，無法對無客戶端進行重置臨時傳遞，因為這些平台需要額外的設備ID解析，而在重置臨時傳遞工具中是不可能的。

<!--
>[!RELATEDINFORMATION]
>
>* [Preflight Authorization](/help/authentication/preflight-authz.md)
-->