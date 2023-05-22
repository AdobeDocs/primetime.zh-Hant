---
title: 預授權
description: JavaScript預授權
exl-id: b7493ca6-1862-4cea-a11e-a634c935c86e
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 0%

---

# 預授權 {#js-preauthorize}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 概述 {#preauth-overview}

該預授權API方法將由應用程式使用以獲得一個或多個資源的預授權決定。 預授權API請求應用於UI提示和/或內容過濾。 在允許用戶訪問指定資源之前，必須發出實際的授權API請求。

如果預授權API請求由Adobe Primetime認證服務處理時發生意外錯誤（例如，網路問題和MVPD授權終結點不可用），則作為預授權API響應結果的一部分，將包括受影響資源的一個或多個單獨的錯誤資訊。

### 公共預授權(請求：預授權請求，回調：AccessEnabler回調&lt;any>):虛 {#preauth-method}

**描述：** 該方法將被應用程式用於從Adobe Primetime認證服務獲得經過驗證的用戶的預授權（資訊性）決定，以查看特定的受保護資源，主要目的是裝飾應用程式的UI（例如用鎖和解鎖表徵圖指示訪問狀態）。

**可用性：** v4.4.0+

**參數：**

* `PreauthorizeRequest`:用於定義請求的生成器對象
* `AccessEnablerCallback`:用於返回API響應的回調
* `PreauthorizeResponse`:用於返回API響應內容的對象

### 類PreauthorizeRequestBuilder {#preath-req-builder-class}

#### setResources(資源：字串[]):預授權請求生成器 {#set-res-preath-req-buildr}

* 設定要獲取其預授權決定的資源清單。
* 必須將其設定為使用預授權API。
* 清單中的每個元素都必須是一個字串，它表示資源ID值或必須與MVPD一致的媒體RSS片段。
* 此方法僅在當前上下文中設定資訊 `PreauthorizeRequestBuilder` 對象實例，是此方法調用的接收方。

* 要構建實際 `PreauthorizeRequest` 你可以看看 `PreauthorizeRequestBuilder`s方法：

```JavaScript
  build(): PreauthorizeRequest
```

* `@param {string[]}` 資源。 要獲得預授權決定的資源清單。
* `@returns {PreauthorizeRequestBuilder}` 對同一項的引用 `PreauthorizeRequestBuilder` 對象實例，是方法調用的接收方。
* 它這樣做是為了允許建立方法連結。

#### 禁用功能(...功能：字串[]):預授權請求生成器 {#disabl-featres-preauth-req-buildr}

* 設定獲取預授權決定時要禁用的功能。
* 此函式僅在當前上下文中設定資訊 `PreauthorizeRequestBuilder` 對象實例，是此函式調用的接收方。
* 要構建實際 `PreauthorizeRequest` 你可以看看 `PreauthorizeRequestBuilder`&#39;s函式：

```JavaScript
public func build() -> PreauthorizeRequest
```

* `@param {string[]}` 功能。 要禁用的一組功能。
* `@returns` 對同一項的引用 `PreauthorizeRequestBuilder` 對象實例，是函式調用的接收方。
* 它這樣做是為了允許建立函式連結。

#### build():預授權請求 {#preauth-req}

* 建立和檢索新的參照 `PreauthorizeRequest` 對象實例。
* 此方法實例化新 `PreauthorizeRequest` 對象。
* 此方法使用當前上下文中預先設定的值 `PreauthorizeRequestBuilder` 對象實例，是此方法調用的接收方。
* 請記住，這種方法不會產生任何副作用，
* 因此，它不會更改SDK的狀態或 `PreauthorizeRequestBuilder` 對象實例，是此方法調用的接收方。
* 這意味著對同一接收方的連續調用將建立不同的新 `PreauthorizeRequest` 對象實例，但具有相同的資訊，以防值設定為 `PreauthorizeRequestBuilder` 未在調用之間修改。
* 如果您不需要更新任何提供的資訊（資源和快取），則可以將PreauthorizeRequest實例重新用於預授權API的多次使用。
* `@returns {PreauthorizeRequest}`

### 介面AccessEnablerCallback&lt;t> {#interface-access-enablr-callback}

#### onResponse(結果：T); {#on-response-result}

* 完成預授權API請求時，SDK調用了響應回調。
* 結果是成功或包含狀態的錯誤結果。
* `@param {T} result`

#### onFailure(結果：T); {#on-failure-result}

* 當無法為預授權API請求提供服務時，SDK調用失敗回調。
* 結果是包含狀態的失敗結果。
* `@param {T} result`

### 類預授權響應 {#preauth-response-class}

#### 公共狀態：狀態； {#public-status}

* 返回：失敗時的其他狀態（狀態）資訊。
* 可能 `null` 值。

#### 公共決策：決定[]; {#public-decisions}

* 返回：預授權決定清單。 每個資源一個決定。
* 如果失敗，清單可能為空。

### 類狀態 {#class-status}

#### 公共狀態：數字； {#public-status-numbr}

* RFC 7231中記錄的HTTP響應狀態代碼。
* 可能為0，以防 `Status` 來自SDK，而不是Adobe Primetime身份驗證服務。

#### 公共代碼：數字； {#public-code-numbr}

* 標準Adobe Primetime身份驗證服務錯誤代碼。
* 可能包含空字串或 `null` 值。

#### 公共消息：字串； {#public-msg-string}

* 在某些情況下，MVPD授權端點或程式設計師降級規則提供的詳細消息。
* 可能包含空字串或 `null` 值。

#### 公共詳細資訊：字串； {#public-details-strng}

* 保存詳細消息，在某些情況下，MVPD授權端點或程式設計師降級規則提供該消息。
* 可能包含空字串或 `null` 值。


#### 公共幫助URL:字串； {#public-help-url-string}

* 連結到有關此狀態/錯誤發生原因的詳細資訊和可能解決方案的URL。
* 可能包含空字串或 `null` 值。

#### 公共跟蹤：字串； {#public-trace-string}

* 此響應的唯一標識符，在與支援部門聯繫以確定更複雜情形中的特定問題時可以使用此標識符。
* 可能包含空字串或 `null` 值。

#### 公共操作：字串； {#public-action-string}

* 建議的糾正此情況的操作。
   * **無**:很遺憾，沒有預定義的操作來修正此問題。 這可能表示對公共API的調用不正確
   * **配置**:需要通過TVE儀表板或聯繫支援人員來更改配置。
   * **應用註冊**:應用程式必須重新註冊自身。
   * **認證**:用戶必須進行身份驗證或重新進行身份驗證。
   * **授權**:用戶必須獲得特定資源的授權。
   * **退化**:應採用某種形式的退化。
   * **重試**:重試請求可能會解決問題
   * **重試後**:在指定的時間段後重試請求可能會解決此問題。
* 可能包含空字串或 `null` 值。

### 類決策 {#class-decision}

#### 公共ID:字串； {#public-id-string}

* 獲取決定的資源ID。

#### 公共授權：布爾值； {#public-auth-boolean}

* 指示決策是否成功的標誌值。

#### 公共錯誤：狀態； {#public-error-status}

* 發生錯誤時，其他狀態（狀態）資訊。 可能 `null` 值。

## 客戶端實現示例 {#client-imp-example}

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


## 方案示例 {#scenario-examples}

### 方案1:已授權所有請求的資源 {#all-req-res-auth}

<table>
<thead>
  <tr>
    <th>增強的錯誤代碼標誌</th>
    <th>響應</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>已禁用</td>
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


### 方案2:已授權一些請求的資源。 {#sm-req-res-auth}

<table>
<thead>
  <tr>
    <th>增強的錯誤代碼標誌</th>
    <th>響應</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>已禁用</td>
    <td>

    &quot;`JavaScript
    
    { 0}
    「決定」：[
    { 0}
    &quot;id&quot;:&quot;RES01&quot;,
    &quot;已授權&quot;:真
    },
    { 0}
    &quot;id&quot;:&quot;RES02&quot;,
    &quot;已授權&quot;:假
    },
    { 0}
    &quot;id&quot;:&quot;RES03&quot;,
    &quot;已授權&quot;:真
    }
    ]
    }
    
    「」

</td>
  </tr>

<tr>
    <td>已啟用</td>
    <td>

    &quot;`JavaScript
    { 0}
    「決定」：[
    { 0}
    &quot;id&quot;:&quot;RES01&quot;,
    &quot;已授權&quot;:真
    },
    { 0}
    &quot;id&quot;:&quot;RES02&quot;,
    &quot;已授權&quot;:假的，
    &quot;錯誤&quot;:{ 0}
    &quot;狀態&quot;:403,
    &quot;代碼&quot;:&quot;preauthorization_denied_by_mvpd&quot;,
    &quot;消息&quot;:&quot;MVPD在請求指定資源的預授權時返回\ &quot;拒絕\&quot;決定。&quot;,
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;操作&quot;:&quot;無&quot;
    }
    },
    { 0}
    &quot;id&quot;:&quot;RES03&quot;,
    &quot;已授權&quot;:真
    },
    ]
    }
    
    「」

</td>
  </tr>
</tbody>


### 方案3:未授權請求的資源。 {#none-req-res-auth}

<table>
<thead>
  <tr>
    <th>增強的錯誤代碼標誌</th>
    <th>響應</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>已禁用</td>
    <td>

    &quot;`JavaScript
    
    { 0}
    「決定」：[
    { 0}
    &quot;id&quot;:&quot;RES01&quot;,
    &quot;已授權&quot;:假
    },
    { 0}
    &quot;id&quot;:&quot;RES02&quot;,
    &quot;已授權&quot;:假
    },
    { 0}
    &quot;id&quot;:&quot;RES03&quot;,
    &quot;已授權&quot;:假
    }
    ]
    }
    
    「」

</td>
  </tr>

<tr>
    <td>已啟用</td>
    <td>

    &quot;`JavaScript
    
    { 0}
    「決定」：[
    { 0}
    &quot;id&quot;:&quot;RES01&quot;,
    &quot;已授權&quot;:假的，
    &quot;錯誤&quot;:{ 0}
    &quot;狀態&quot;:403,
    &quot;代碼&quot;:&quot;preauthorization_denied_by_mvpd&quot;,
    &quot;消息&quot;:&quot;MVPD在請求指定資源的預授權時返回\ &quot;拒絕\&quot;決定。&quot;,
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;操作&quot;:&quot;無&quot;
    }
    },
    { 0}
    &quot;id&quot;:&quot;RES02&quot;,
    &quot;已授權&quot;:假的，
    &quot;錯誤&quot;:{ 0}
    &quot;狀態&quot;:403,
    &quot;代碼&quot;:&quot;preauthorization_denied_by_mvpd&quot;,
    &quot;消息&quot;:&quot;MVPD在請求指定資源的預授權時返回\ &quot;拒絕\&quot;決定。&quot;,
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;操作&quot;:&quot;無&quot;
    }
    },
    { 0}
    &quot;id&quot;:&quot;RES03&quot;,
    &quot;已授權&quot;:假的，
    &quot;錯誤&quot;:{ 0}
    &quot;狀態&quot;:403,
    &quot;代碼&quot;:&quot;maximum_execution_time_exceeded&quot;,
    &quot;消息&quot;:&quot;請求未在允許的最大時間內完成。 重試請求可能會解決問題。」，
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;操作&quot;:&quot;重試&quot;
    }
    }
    ]
    }
    
    「」

</td>
  </tr>
</tbody>


### 方案4:客戶端請求錯誤 — 未指定資源。 {#bad-cl-req-no-res-sp}

<table>
<thead>
  <tr>
    <th>增強的錯誤代碼標誌</th>
    <th>響應</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>已禁用/已啟用</td>
    <td>

    &quot;`JavaScript
    { 0}
    &quot;狀態&quot;:{ 0}
    &quot;狀態&quot;:400,
    &quot;代碼&quot;:&quot;internal_error&quot;,
    &quot;消息&quot;:&quot;由於內部錯誤，請求失敗。&quot;,
    「詳細資訊」：&quot;所需的String[]參數&#39;resource&#39;不存在&quot;,
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;操作&quot;:&quot;無&quot;
    },
    「決定」：[]
    }
    「」

</td>
  </tr>
</tbody>
</table>

### 方案5:錯誤的客戶端請求 — 指定的資源為空。 {#bad-cl-req-empt-res-sp}

<table>
<thead>
  <tr>
    <th>增強的錯誤代碼標誌</th>
    <th>響應</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>已禁用/已啟用</td>
    <td>

    &quot;`JavaScript
    { 0}
    &quot;狀態&quot;:{ 0}
    &quot;狀態&quot;:412,
    &quot;代碼&quot;:&quot;missing_resource&quot;,
    &quot;消息&quot;:&quot;缺少資源參數&quot;,
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;操作&quot;:&quot;無&quot;
    },
    「決定」：[]
    }
    「」

</td>
  </tr>
</tbody>
</table>

### 方案6:網路錯誤。 {#ntwrk-error}

<table>
<thead>
  <tr>
    <th>增強的錯誤代碼標誌</th>
    <th>響應</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>已啟用</td>
    <td>

    &quot;`JavaScript
    { 0}
    「決定」：[
    { 0}
    &quot;id&quot;:&quot;RES01&quot;,
    &quot;已授權&quot;:假的，
    &quot;錯誤&quot;:{ 0}
    &quot;狀態&quot;:403,
    &quot;代碼&quot;:&quot;network_received_error&quot;,
    &quot;消息&quot;:&quot;從關聯的夥伴服務檢索響應時出現讀取錯誤。 重試請求可能會解決問題。」，
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;操作&quot;:&quot;重試&quot;
    }
    },
    { 0}
    &quot;id&quot;:&quot;RES02&quot;,
    &quot;已授權&quot;:假的，
    &quot;錯誤&quot;:{ 0}
    &quot;狀態&quot;:403,
    &quot;代碼&quot;:&quot;network_received_error&quot;,
    &quot;消息&quot;:&quot;從關聯的夥伴服務檢索響應時出現讀取錯誤。 重試請求可能會解決問題。」，
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;操作&quot;:&quot;重試&quot;
    }
    }
    ]
    }
    「」

</td>
  </tr>
</tbody>
</table>

### 方案7:在沒有有效AuthN會話的情況下調用了預授權流。

<table>
<thead>
  <tr>
    <th>增強的錯誤代碼標誌</th>
    <th>響應</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>已禁用/已啟用</td>
    <td>

    &quot;`JavaScript
    { 0}
    &quot;狀態&quot;:{ 0}
    &quot;狀態&quot;:0,
    &quot;代碼&quot;:&quot;authentication_session_missing&quot;,
    &quot;消息&quot;:&quot;無法檢索與此請求關聯的驗證會話。 用戶必須使用支援的MVPD重新驗證才能繼續。&quot;,
    &quot;操作&quot;:&quot;驗證&quot;
    },
    「決定」：[]
    }
    
    「」

</td>
  </tr>
</tbody>
</table>



### 方案8:在setRequestor調用完成之前調用了預授權流

<table>
<thead>
  <tr>
    <th>增強的錯誤代碼標誌</th>
    <th>響應</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>已禁用/已啟用</td>
    <td>

    &quot;`JavaScript
    { 0}
    &quot;狀態&quot;:{ 0}
    &quot;狀態&quot;:0,
    &quot;代碼&quot;:&quot;requestor_not_configured&quot;,
    &quot;消息&quot;:&quot;尚未配置請求者，該請求者是使用除setRequestor API之外的任何API的先決條件。&quot;,
    &quot;操作&quot;:&quot;重試&quot;
    },
    「決定」：[]
    }
    「」

</td>
  </tr>
</tbody>
</table>
