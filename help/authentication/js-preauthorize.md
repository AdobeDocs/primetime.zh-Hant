---
title: 預先授權
description: JavaScript預先授權
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 0%

---


# 預先授權 {#js-preauthorize}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 概述 {#preauth-overview}

預授權API方法將被應用程式用於獲取一個或多個資源的預授權決策。 應將預先授權API要求用於UI提示和/或內容篩選。 必須先提出實際的授權API要求，才能允許使用者存取指定的資源。

如果Adobe Primetime驗證服務處理預先授權API請求時發生非預期錯誤（例如，網路問題，且MVPD授權端點無法使用），則作為預先授權API回應結果的一部分，將會為受影響的資源包含一或多個個別的錯誤資訊。

### 公共預授權（請求）PreauthorizeRequest，回呼：AccessEnablerCallback&lt;any>):void {#preauth-method}

**說明：** 此方法將供應用程式用來從Adobe Primetime驗證服務取得已驗證使用者的預先授權（資訊）決定，以檢視特定的受保護資源，以裝飾應用程式的UI（例如以鎖定和解鎖圖示指示存取狀態）。

**可用性：** v4.4.0+

**參數：**

* `PreauthorizeRequest`:用來定義請求的產生器物件
* `AccessEnablerCallback`:用來傳回API回應的回呼
* `PreauthorizeResponse`:用於傳回API回應內容的物件

### 類別PreauthorizeRequestBuilder {#preath-req-builder-class}

#### setResources(resources:字串[]):PreauthorizeRequestBuilder {#set-res-preath-req-buildr}

* 設定要獲取預授權決策的資源清單。
* 必須將其設定為使用預先授權API。
* 清單中的每個元素都必須是字串，代表資源ID值或必須與MVPD同意的媒體RSS片段。
* 此方法只會在目前的內容中設定資訊 `PreauthorizeRequestBuilder` 物件例項，此為此方法呼叫的接收器。

* 建置實際 `PreauthorizeRequest` 你可以看看 `PreauthorizeRequestBuilder`&#39;s方法：

```JavaScript
  build(): PreauthorizeRequest
```

* `@param {string[]}` 資源。 要獲得預授權決策的資源清單。
* `@returns {PreauthorizeRequestBuilder}` 對同一項的引用 `PreauthorizeRequestBuilder` 物件例項，此為方法呼叫的接收器。
* 這麼做可讓方法連結建立。

#### disableFeatures(...功能：字串[]):PreauthorizeRequestBuilder {#disabl-featres-preauth-req-buildr}

* 設定您要在取得預先授權決定時將其停用的功能。
* 此函式僅在目前的內容中設定資訊 `PreauthorizeRequestBuilder` 物件例項，此為此函式呼叫的接收者。
* 建置實際 `PreauthorizeRequest` 你可以看看 `PreauthorizeRequestBuilder`&#39;s函式：

```JavaScript
public func build() -> PreauthorizeRequest
```

* `@param {string[]}` 功能。 要禁用的功能集。
* `@returns` 對同一項的引用 `PreauthorizeRequestBuilder` 物件例項，此為函式呼叫的接收者。
* 它這麼做是為了允許建立函式連結。

#### build():PreauthorizeRequest {#preauth-req}

* 建立並檢索新的 `PreauthorizeRequest` 物件例項。
* 此方法可實例化新 `PreauthorizeRequest` 物件。
* 此方法會使用目前內容中預先設定的值 `PreauthorizeRequestBuilder` 物件例項，此為此方法呼叫的接收器。
* 請記住，這種方法不會產生任何副作用，
* 因此，它不會變更SDK的狀態或 `PreauthorizeRequestBuilder` 物件例項，此為此方法呼叫的接收器。
* 這表示同一接收機的此方法的後續呼叫將建立不同的新 `PreauthorizeRequest` 物件例項，但有相同的資訊(若值設為 `PreauthorizeRequestBuilder` 中，未在呼叫之間修改。
* 如果您不需要更新任何提供的資訊（資源和快取），您可以重複使用PreauthorizeRequest例項，以多次使用預先授權API。
* `@returns {PreauthorizeRequest}`

### 介面AccessEnablerCallback&lt;t> {#interface-access-enablr-callback}

#### onResponse(結果：T); {#on-response-result}

* 完成預先授權API請求時，SDK會呼叫回應回呼。
* 結果為成功或包含狀態的錯誤結果。
* `@param {T} result`

#### onFailure(結果：T); {#on-failure-result}

* 當無法處理預先授權API請求時，SDK會呼叫失敗回呼。
* 結果是包含狀態的失敗結果。
* `@param {T} result`

### 類預授權響應 {#preauth-response-class}

#### 公用狀態：狀態； {#public-status}

* 傳回：失敗時的其他狀態（狀態）資訊。
* 可能會保留 `null` 值。

#### 公共決策：決策[]; {#public-decisions}

* 傳回：預先授權決定清單。 每個資源一個決策。
* 如果失敗，清單可能為空。

### 類狀態 {#class-status}

#### 公用狀態：數字； {#public-status-numbr}

* RFC 7231中記錄的HTTP回應狀態代碼。
* 可能為0，以防 `Status` 來自SDK而非Adobe Primetime驗證服務。

#### 公開代碼：數字； {#public-code-numbr}

* 標準Adobe Primetime驗證服務錯誤碼。
* 可能會保留空白字串或 `null` 值。

#### 公開訊息：字串； {#public-msg-string}

* 在某些情況下由MVPD授權端點或程式設計師降級規則提供的詳細消息。
* 可能會保留空白字串或 `null` 值。

#### 公開詳細資訊：字串； {#public-details-strng}

* 保留一個詳細消息，在某些情況下，該消息由MVPD授權端點或程式設計師降級規則提供。
* 可能會保留空白字串或 `null` 值。


#### 公共helpUrl:字串； {#public-help-url-string}

* 連結至詳細資訊的URL，說明為何發生此狀態/錯誤，以及可能的解決方案。
* 可能會保留空白字串或 `null` 值。

#### 公共跟蹤：字串； {#public-trace-string}

* 此回應的唯一識別碼，可在聯絡支援人員以在更複雜的情境中識別特定問題時使用。
* 可能會保留空白字串或 `null` 值。

#### 公共行動：字串； {#public-action-string}

* 修正此情況的建議操作。
   * **無**:很可惜，沒有預先定義的動作可修正此問題。 這可能表示公用API的呼叫不當
   * **配置**:需要通過TVE儀表板或聯繫支援人員進行配置更改。
   * **應用註冊**:應用程式必須重新註冊。
   * **驗證**:用戶必須進行身份驗證或重新驗證。
   * **授權**:用戶必須獲得特定資源的授權。
   * **降解**:應採用某種形式的退化。
   * **重試**:重試請求可能解決問題
   * **重試後**:在指定的時段後重試請求可能會解決問題。
* 可能會保留空白字串或 `null` 值。

### 類決策 {#class-decision}

#### 公共id:字串； {#public-id-string}

* 獲得決策的資源ID。

#### 公共授權：布林值； {#public-auth-boolean}

* 指出決策是否成功的旗標值。

#### 公用錯誤：狀態； {#public-error-status}

* 其他狀態（狀態）資訊，以防發生錯誤。 可能會保留 `null` 值。

## 用戶端實作範例 {#client-imp-example}

```JavaScript
let accessEnablerApi = new window.AccessEnabler.AccessEnabler("software statement");
let accessEnablerModels = window.AccessEnabler.models;



// Build request
let requestBuilder = new accessEnablerModels.PreauthorizeRequest.getBuilder();
let request = requestBuilder
    .setResources(["RES01", "RES02", "RES03"])
    .disableFeatures("LOCAL_CACHE")
    .build();



// Create callback
let callback = {
    onResponse(response) {
        // Handle onResponse
    },
    onFailure(response) {
        // Handle onFailure
    }
};

// Invoke call
accessEnablerApi.preauthorize(request, callback);
```


## 案例範例 {#scenario-examples}

### 方案1:所有請求的資源都已獲得授權 {#all-req-res-auth}

<table>
<thead>
  <tr>
    <th>增強的錯誤碼標幟</th>
    <th>回應</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>已停用</td>
    <td>

```JavaScript
        {
    "decisions": [
        {
        "id": "RES01",
        "authorized": true
        },
        {
        "id": "RES02",
        "authorized": true
        },
        {
        "id": "RES03",
        "authorized": true
        }
    ]
    }    
```

</td>
  </tr>
</tbody>


### 方案2:已核准一些請求的資源。 {#sm-req-res-auth}

<table>
<thead>
  <tr>
    <th>增強的錯誤碼標幟</th>
    <th>回應</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>已停用</td>
    <td>

    &quot;&#39;JavaScript
    
    {
    &quot;decisions&quot;:[
    {
    &quot;id&quot;:&quot;RES01&quot;,
    「已授權」：true
    },
    {
    &quot;id&quot;:&quot;RES02&quot;,
    「已授權」：false
    },
    {
    &quot;id&quot;:&quot;RES03&quot;,
    「已授權」：true
    }
    ]
    }
    
    &quot;

</td>
  </tr>

<tr>
    <td>已啟用</td>
    <td>

    &quot;&#39;JavaScript
    {
    &quot;decisions&quot;:[
    {
    &quot;id&quot;:&quot;RES01&quot;,
    「已授權」：true
    },
    {
    &quot;id&quot;:&quot;RES02&quot;,
    「已授權」：false,
    &quot;error&quot;:{
    &quot;status&quot;:403,
    &quot;code&quot;:&quot;preauthorization_denied_by_mvpd&quot;,
    &quot;message&quot;:&quot;請求指定資源的預授權時，MVPD已傳回\&quot;拒絕\&quot;決定。&quot;,
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;:&quot;none&quot;
    }
    },
    {
    &quot;id&quot;:&quot;RES03&quot;,
    「已授權」：true
    },
    ]
    }
    
    &quot;

</td>
  </tr>
</tbody>


### 方案3:所請求的資源均未獲得授權。 {#none-req-res-auth}

<table>
<thead>
  <tr>
    <th>增強的錯誤碼標幟</th>
    <th>回應</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>已停用</td>
    <td>

    &quot;&#39;JavaScript
    
    {
    &quot;decisions&quot;:[
    {
    &quot;id&quot;:&quot;RES01&quot;,
    「已授權」：false
    },
    {
    &quot;id&quot;:&quot;RES02&quot;,
    「已授權」：false
    },
    {
    &quot;id&quot;:&quot;RES03&quot;,
    「已授權」：false
    }
    ]
    }
    
    &quot;

</td>
  </tr>

<tr>
    <td>已啟用</td>
    <td>

    &quot;&#39;JavaScript
    
    {
    &quot;decisions&quot;:[
    {
    &quot;id&quot;:&quot;RES01&quot;,
    「已授權」：false,
    &quot;error&quot;:{
    &quot;status&quot;:403,
    &quot;code&quot;:&quot;preauthorization_denied_by_mvpd&quot;,
    &quot;message&quot;:&quot;請求指定資源的預授權時，MVPD已傳回\&quot;拒絕\&quot;決定。&quot;,
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;:&quot;none&quot;
    }
    },
    {
    &quot;id&quot;:&quot;RES02&quot;,
    「已授權」：false,
    &quot;error&quot;:{
    &quot;status&quot;:403,
    &quot;code&quot;:&quot;preauthorization_denied_by_mvpd&quot;,
    &quot;message&quot;:&quot;請求指定資源的預授權時，MVPD已傳回\&quot;拒絕\&quot;決定。&quot;,
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;:&quot;none&quot;
    }
    },
    {
    &quot;id&quot;:&quot;RES03&quot;,
    「已授權」：false,
    &quot;error&quot;:{
    &quot;status&quot;:403,
    &quot;code&quot;:&quot;maximum_execution_time_exceeded&quot;,
    &quot;message&quot;:「請求未在允許的最大時間內完成。 重試請求可能會解決問題。」，
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;:&quot;retry&quot;
    }
    }
    ]
    }
    
    &quot;

</td>
  </tr>
</tbody>


### 方案4:客戶端請求錯誤 — 未指定任何資源。 {#bad-cl-req-no-res-sp}

<table>
<thead>
  <tr>
    <th>增強的錯誤碼標幟</th>
    <th>回應</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>禁用/啟用</td>
    <td>

    &quot;&#39;JavaScript
    {
    &quot;status&quot;:{
    &quot;status&quot;:400,
    &quot;code&quot;:&quot;internal_error&quot;,
    &quot;message&quot;:&quot;由於內部錯誤，請求失敗。&quot;,
    「詳細資訊」：&quot;必需的字串[]參數&#39;resource&#39;不存在&quot;,
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;:&quot;none&quot;
    },
    &quot;decisions&quot;:[]
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### 方案5:客戶端請求錯誤 — 指定了空資源。 {#bad-cl-req-empt-res-sp}

<table>
<thead>
  <tr>
    <th>增強的錯誤碼標幟</th>
    <th>回應</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>禁用/啟用</td>
    <td>

    &quot;&#39;JavaScript
    {
    &quot;status&quot;:{
    &quot;status&quot;:412,
    &quot;code&quot;:&quot;missing_resource&quot;,
    &quot;message&quot;:&quot;缺少資源參數&quot;,
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;:&quot;none&quot;
    },
    &quot;decisions&quot;:[]
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### 方案6:網路錯誤。 {#ntwrk-error}

<table>
<thead>
  <tr>
    <th>增強的錯誤碼標幟</th>
    <th>回應</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>已啟用</td>
    <td>

    &quot;&#39;JavaScript
    {
    &quot;decisions&quot;:[
    {
    &quot;id&quot;:&quot;RES01&quot;,
    「已授權」：false,
    &quot;error&quot;:{
    &quot;status&quot;:403,
    &quot;code&quot;:&quot;network_received_error&quot;,
    &quot;message&quot;:「從關聯的合作夥伴服務檢索響應時出現讀取錯誤。 重試請求可能會解決問題。」，
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;:&quot;retry&quot;
    }
    },
    {
    &quot;id&quot;:&quot;RES02&quot;,
    「已授權」：false,
    &quot;error&quot;:{
    &quot;status&quot;:403,
    &quot;code&quot;:&quot;network_received_error&quot;,
    &quot;message&quot;:「從關聯的合作夥伴服務檢索響應時出現讀取錯誤。 重試請求可能會解決問題。」，
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;:&quot;retry&quot;
    }
    }
    ]
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### 方案7:在沒有有效AuthN會話的情況下調用了預授權流。

<table>
<thead>
  <tr>
    <th>增強的錯誤碼標幟</th>
    <th>回應</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>禁用/啟用</td>
    <td>

    &quot;&#39;JavaScript
    {
    &quot;status&quot;:{
    &quot;status&quot;:0,
    &quot;code&quot;:&quot;authentication_session_missing&quot;,
    &quot;message&quot;:&quot;無法檢索與此請求關聯的驗證會話。 用戶必須使用支援的MVPD重新驗證才能繼續。」，
    &quot;action&quot;:&quot;authentication&quot;
    },
    &quot;decisions&quot;:[]
    }
    
    &quot;

</td>
  </tr>
</tbody>
</table>



### 方案8:在setRequestor調用完成之前調用了預授權流

<table>
<thead>
  <tr>
    <th>增強的錯誤碼標幟</th>
    <th>回應</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>禁用/啟用</td>
    <td>

    &quot;&#39;JavaScript
    {
    &quot;status&quot;:{
    &quot;status&quot;:0,
    &quot;code&quot;:&quot;requestor_not_configured&quot;,
    &quot;message&quot;:&quot;請求者尚未設定，這是使用除setRequestor API外的任何API的先決條件。&quot;,
    &quot;action&quot;:&quot;retry&quot;
    },
    &quot;decisions&quot;:[]
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

