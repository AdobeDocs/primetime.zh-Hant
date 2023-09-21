---
title: 預先授權
description: JavaScript預先授權
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 0%

---

# 預先授權 {#js-preauthorize}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要Adobe的目前授權。 不允許未經授權的使用。

## 概觀 {#preauth-overview}

預先授權API方法可供應用程式用來取得一或多個資源的預先授權決定。 預先授權API要求應該用於UI提示和/或內容篩選。 在允許使用者存取指定的資源之前，必須先提出實際的授權API要求。

如果Adobe Primetime驗證服務處理預先授權API請求時發生未預期的錯誤（例如網路問題，以及MVPD授權端點無法使用），則受影響資源的一或多個個別錯誤資訊將會納入作為預先授權API回應結果的一部分。

### public preauthorize(請求： PreauthorizeRequest， callback： AccessEnablerCallback&lt;any>)：無效 {#preauth-method}

**說明：** 應用程式可使用此方法來從Adobe Primetime Authentication服務取得已驗證使用者的預先授權（資訊）決定，以檢視特定的受保護資源，主要目的是裝飾應用程式的UI （例如，以鎖定和解鎖圖示指示存取狀態）。

**可用性：** v4.4.0+

**引數：**

* `PreauthorizeRequest`：用於定義請求的產生器物件
* `AccessEnablerCallback`：用於傳回API回應的回呼
* `PreauthorizeResponse`：用來傳回API回應內容的物件

### 類別PreauthorizeRequestBuilder {#preath-req-builder-class}

#### setResources(resources：字串[])： PreauthorizeRequestBuilder {#set-res-preath-req-buildr}

* 設定您要取得預先授權決定的資源清單。
* 您必須將其設定為使用預先授權API。
* 清單中的每個元素都必須是字串，代表必須與MVPD協定的資源ID值或媒體RSS片段。
* 此方法只會設定目前內容中的資訊 `PreauthorizeRequestBuilder` 物件例項，此方法呼叫的接收者。

* 若要建置實際 `PreauthorizeRequest` 您可以檢視 `PreauthorizeRequestBuilder`的方法：

```JavaScript
  build(): PreauthorizeRequest
```

* `@param {string[]}` 資源。 您要取得預先授權決定的資源清單。
* `@returns {PreauthorizeRequestBuilder}` 對同一專案的參照 `PreauthorizeRequestBuilder` 物件例項，方法呼叫的接收者。
* 如此即可建立方法鏈結。

#### disableFeatures(...features： string[])： PreauthorizeRequestBuilder {#disabl-featres-preauth-req-buildr}

* 設定您要在取得預先授權決定時停用這些功能的功能。
* 此函式只設定目前內容中的資訊 `PreauthorizeRequestBuilder` 物件例項，此函式呼叫的接收者。
* 若要建置實際 `PreauthorizeRequest` 您可以檢視 `PreauthorizeRequestBuilder`的函式：

```JavaScript
public func build() -> PreauthorizeRequest
```

* `@param {string[]}` 功能。 您想要停用它們的一組功能。
* `@returns` 對同一專案的參照 `PreauthorizeRequestBuilder` 物件例項，函式呼叫的接收者。
* 它這樣做是為了允許建立函式鏈結。

#### build()： PreauthorizeRequest {#preauth-req}

* 建立及擷取新的參照 `PreauthorizeRequest` 物件例項。
* 此方法會例項化新的 `PreauthorizeRequest` 物件。
* 此方法會使用目前內容中預先設定的值 `PreauthorizeRequestBuilder` 物件例項，此方法呼叫的接收者。
* 請記住，此方法不會產生任何副作用，
* 因此，不會變更SDK的狀態或 `PreauthorizeRequestBuilder` 物件例項，此方法呼叫的接收者。
* 這表示此方法對相同接收器的後續呼叫將建立不同的新值 `PreauthorizeRequest` 物件例項，但具有相同的資訊，以防值設定為 `PreauthorizeRequestBuilder` 在兩次呼叫之間未修改的位置。
* 如果您不需要更新任何提供的資訊（資源與快取），您可以針對預先授權API的多重用途重複使用PreauthorizeRequest執行個體。
* `@returns {PreauthorizeRequest}`

### 介面AccessEnablerCallback&lt;t> {#interface-access-enablr-callback}

#### onResponse(result： T)； {#on-response-result}

* 完成預先授權API要求時，SDK呼叫的回應回呼。
* 結果為成功或包含狀態的錯誤結果。
* `@param {T} result`

#### onFailure（結果： T）； {#on-failure-result}

* 無法服務預先授權API請求時，SDK呼叫的失敗回呼。
* 結果會產生包含狀態的失敗結果。
* `@param {T} result`

### 類別PreauthorizeResponse {#preauth-response-class}

#### 公開狀態：狀態； {#public-status}

* 傳回：發生失敗時的其他狀態（狀態）資訊。
* 可容納 `null` 值。

#### 公開決定：決定[]； {#public-decisions}

* 傳回：預先授權決定的清單。 每個資源一個決策。
* 如果失敗，清單可能會是空的。

### 類別狀態 {#class-status}

#### 公開狀態：數字； {#public-status-numbr}

* RFC 7231中記錄的HTTP回應狀態代碼。
* 可能為0，以防出現 `Status` 來自SDK，而非Adobe Primetime驗證服務。

#### 公用代碼：號碼； {#public-code-numbr}

* 標準Adobe Primetime驗證服務錯誤代碼。
* 可能保留空字串或 `null` 值。

#### 公開訊息：字串； {#public-msg-string}

* 在某些情況下由MVPD授權端點或程式設計人員降級規則提供的詳細訊息。
* 可能保留空字串或 `null` 值。

#### 公開詳細資料：字串； {#public-details-strng}

* 儲存詳細訊息，在某些情況下，該訊息由MVPD授權端點或程式設計人員降級規則提供。
* 可能保留空字串或 `null` 值。


#### public helpUrl： string； {#public-help-url-string}

* 此URL會連結至關於為何發生此狀態/錯誤以及可能解決方案的詳細資訊。
* 可能保留空字串或 `null` 值。

#### 公用追蹤：字串； {#public-trace-string}

* 此回應的唯一識別碼，可在聯絡支援人員以識別更複雜案例中的特定問題時使用。
* 可能保留空字串或 `null` 值。

#### 公開動作：字串； {#public-action-string}

* 補救此情況的建議動作。
   * **無**：很抱歉，沒有預先定義的動作來修正此問題。 這可能表示對公用API的呼叫不正確
   * **設定**：需要透過TVE儀表板或連絡支援人員來變更設定。
   * **application-register**：應用程式必須再次登入自身。
   * **authentication**：使用者必須驗證或重新驗證。
   * **authorization**：使用者必須取得特定資源的授權。
   * **退化**：應套用某種形式的降級。
   * **重試**：重試請求或許可以解決問題
   * **之後重試**：在指定的時段後重試請求或許可以解決問題。
* 可能保留空字串或 `null` 值。

### 類別決定 {#class-decision}

#### 公用識別碼：字串； {#public-id-string}

* 取得決定的資源ID。

#### public authorized： boolean； {#public-auth-boolean}

* 表示決策是否成功的旗標值。

#### 公開錯誤：狀態； {#public-error-status}

* 發生某些錯誤時的其他狀態（狀態）資訊。 可容納 `null` 值。

## 使用者端實作範例 {#client-imp-example}

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

### 案例1：已授權所有請求的資源 {#all-req-res-auth}

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


### 案例2：已授權部分請求的資源。 {#sm-req-res-auth}

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
    &quot;decisions&quot;： [
    {
    &quot;id&quot;： &quot;RES01&quot;，
    &quot;authorized&quot;： true
    }，
    {
    &quot;id&quot;： &quot;RES02&quot;，
    &quot;authorized&quot;： false
    }，
    {
    &quot;id&quot;： &quot;RES03&quot;，
    &quot;authorized&quot;： true
    }
    ]
    }
    
    ```

</td>
  </tr>

<tr>
    <td>已啟用</td>
    <td>

    ```JavaScript
    {
    &quot;decisions&quot;： [
    {
    &quot;id&quot;： &quot;RES01&quot;，
    &quot;authorized&quot;： true
    }，
    {
    &quot;id&quot;： &quot;RES02&quot;，
    &quot;authorized&quot;： false，
    &quot;error&quot;： {
    &quot;status&quot;：403，
    &quot;code&quot;： &quot;preauthorization_denied_by_mvpd&quot;，
    &quot;message&quot;： &quot;MVPD在要求指定資源的預先授權時傳回\&quot;Deny\&quot;決定。&quot;，
    &quot;helpUrl&quot;： &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;，
    &quot;action&quot;： &quot;none&quot;
    }
    }，
    {
    &quot;id&quot;： &quot;RES03&quot;，
    &quot;authorized&quot;： true
    }，
    ]
    }
    
    ```

</td>
  </tr>
</tbody>


### 案例3：沒有授權請求的資源。 {#none-req-res-auth}

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
    &quot;decisions&quot;： [
    {
    &quot;id&quot;： &quot;RES01&quot;，
    &quot;authorized&quot;： false
    }，
    {
    &quot;id&quot;： &quot;RES02&quot;，
    &quot;authorized&quot;： false
    }，
    {
    &quot;id&quot;： &quot;RES03&quot;，
    &quot;authorized&quot;： false
    }
    ]
    }
    
    ```

</td>
  </tr>

<tr>
    <td>已啟用</td>
    <td>

    ```JavaScript
    
    {
    &quot;decisions&quot;： [
    {
    &quot;id&quot;： &quot;RES01&quot;，
    &quot;authorized&quot;： false，
    &quot;error&quot;： {
    &quot;status&quot;：403，
    &quot;code&quot;： &quot;preauthorization_denied_by_mvpd&quot;，
    &quot;message&quot;： &quot;MVPD在要求指定資源的預先授權時傳回\&quot;Deny\&quot;決定。&quot;，
    &quot;helpUrl&quot;： &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;，
    &quot;action&quot;： &quot;none&quot;
    }
    }，
    {
    &quot;id&quot;： &quot;RES02&quot;，
    &quot;authorized&quot;： false，
    &quot;error&quot;： {
    &quot;status&quot;：403，
    &quot;code&quot;： &quot;preauthorization_denied_by_mvpd&quot;，
    &quot;message&quot;： &quot;MVPD在要求指定資源的預先授權時傳回\&quot;Deny\&quot;決定。&quot;，
    &quot;helpUrl&quot;： &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;，
    &quot;action&quot;： &quot;none&quot;
    }
    }，
    {
    &quot;id&quot;： &quot;RES03&quot;，
    &quot;authorized&quot;： false，
    &quot;error&quot;： {
    &quot;status&quot;：403，
    &quot;code&quot;： &quot;maximum_execution_time_exceeded&quot;，
    &quot;message&quot;：&quot;請求未在允許的最長時間內完成。 重試請求或許可以解決此問題。」，
    &quot;helpUrl&quot;： &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;，
    &quot;action&quot;： &quot;retry&quot;
    }
    }
    ]
    }
    
    ```

</td>
  </tr>
</tbody>


### 案例4：錯誤的使用者端請求 — 未指定資源。 {#bad-cl-req-no-res-sp}

<table>
<thead>
  <tr>
    <th>增強的錯誤碼標幟</th>
    <th>回應</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>已停用/已啟用</td>
    <td>

    ```JavaScript
    {
    &quot;status&quot;： {
    &quot;status&quot;：400，
    &quot;code&quot;： &quot;internal_error&quot;，
    &quot;message&quot;： &quot;由於內部錯誤，請求失敗。&quot;，
    &quot;details&quot;： &quot;Required String[]引數&#39;resource&#39;不存在&quot;，
    &quot;helpUrl&quot;： &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;，
    &quot;action&quot;： &quot;none&quot;
    }，
    &quot;decisions&quot;： []
    }
    ```

</td>
  </tr>
</tbody>
</table>

### 案例5：錯誤的使用者端請求 — 指定的資源是空的。 {#bad-cl-req-empt-res-sp}

<table>
<thead>
  <tr>
    <th>增強的錯誤碼標幟</th>
    <th>回應</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>已停用/已啟用</td>
    <td>

    ```JavaScript
    {
    &quot;status&quot;： {
    &quot;status&quot;：412，
    &quot;code&quot;： &quot;missing_resource&quot;，
    &quot;message&quot;：&quot;缺少資源引數&quot;，
    &quot;helpUrl&quot;： &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;，
    &quot;action&quot;： &quot;none&quot;
    }，
    &quot;decisions&quot;： []
    }
    ```

</td>
  </tr>
</tbody>
</table>

### 案例6：網路錯誤。 {#ntwrk-error}

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

    ```JavaScript
    {
    &quot;decisions&quot;： [
    {
    &quot;id&quot;： &quot;RES01&quot;，
    &quot;authorized&quot;： false，
    &quot;error&quot;： {
    &quot;status&quot;：403，
    &quot;code&quot;： &quot;network_received_error&quot;，
    &quot;message&quot;：&quot;從關聯的合作夥伴服務擷取回應時發生讀取錯誤。 重試請求或許可以解決此問題。」，
    &quot;helpUrl&quot;： &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;，
    &quot;action&quot;： &quot;retry&quot;
    }
    }，
    {
    &quot;id&quot;： &quot;RES02&quot;，
    &quot;authorized&quot;： false，
    &quot;error&quot;： {
    &quot;status&quot;：403，
    &quot;code&quot;： &quot;network_received_error&quot;，
    &quot;message&quot;：&quot;從關聯的合作夥伴服務擷取回應時發生讀取錯誤。 重試請求或許可以解決此問題。」，
    &quot;helpUrl&quot;： &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;，
    &quot;action&quot;： &quot;retry&quot;
    }
    }
    ]
    }
    ```

</td>
  </tr>
</tbody>
</table>

### 案例7：叫用的預先授權流程沒有有效的AuthN工作階段。

<table>
<thead>
  <tr>
    <th>增強的錯誤碼標幟</th>
    <th>回應</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>已停用/已啟用</td>
    <td>

    ```JavaScript
    {
    &quot;status&quot;： {
    &quot;status&quot;： 0，
    &quot;code&quot;： &quot;authentication_session_missing&quot;，
    &quot;message&quot;： &quot;無法擷取與此要求相關聯的驗證工作階段。 使用者必須使用支援的MVPD重新驗證才能繼續。」，
    &quot;action&quot;： &quot;authentication&quot;
    }，
    &quot;decisions&quot;： []
    }
    
    ```

</td>
  </tr>
</tbody>
</table>



### 案例8：在setRequestor呼叫完成之前叫用預先授權流程

<table>
<thead>
  <tr>
    <th>增強的錯誤碼標幟</th>
    <th>回應</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>已停用/已啟用</td>
    <td>

    ```JavaScript
    {
    &quot;status&quot;： {
    &quot;status&quot;： 0，
    &quot;code&quot;： &quot;requestor_not_configured&quot;，
    &quot;message&quot;：&quot;要求者尚未設定，這是使用setRequestor API以外的任何API的必要條件。&quot;，
    &quot;action&quot;： &quot;retry&quot;
    }，
    &quot;decisions&quot;： []
    }
    ```

</td>
  </tr>
</tbody>
</table>
