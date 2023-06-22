---
title: 預檢授權
description: 預檢授權
exl-id: 036b1a8e-f2dc-4e9a-9eeb-0787e40c00d9
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 0%

---

# 預檢授權 {#preflight-authorization}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

</br>

## 概觀 {#overview}

此功能為多個資源提供輕量授權檢查。 此輕量級檢查的目的是裝飾UI （例如，使用鎖定和解鎖圖示指示存取狀態）。 預檢授權儘可能簡易和有效，因此單一API呼叫會產生資源清單的授權狀態。 請注意，此功能在授權資源方面並不權威。

A `getAuthorization(resource)` 或 `checkAuthorization(resource)` 在允許播放之前，仍須進行呼叫。

預檢授權也提供不同使用案例的支援，在這種情況下，程式設計師需要請求多個資源ID的授權，才能允許播放一個媒體內容。 程式設計師可以對所需資源執行初始預檢檢查，如果不符合業務條件，則視回應而定，可能會提前失敗。

如需支援預檢授權的MVPD清單，請參閱 [MVPD預檢授權](/help/authentication/mvpd-preflight-authz.md#preflight_support_list) 頁面。 

>[!NOTE]
>
> 請注意，此功能用於沒有完整預檢授權支援的MVPD時，需要事先與Adobe和MVPD商定。 在這些MVPD上使用預檢授權將屬於所述的「最壞情況」 [此處](/help/authentication/mvpd-preflight-authz.md#intro) 並可能導致效能問題和緩慢的回應時間。 </br>
> 此外，請注意，使用預檢授權 **需要Adobe明確同意5個以上的資源**.

## AccessEnabler Preflight API {#AE_pre_api}

AccessEnabler會公開API/回呼函式配對，以實作預檢授權。 API呼叫採用由資源清單組成的單一引數。 回呼函式會採用代表實際授權資源的單一引數。 以下範例為ActionScript，但所有型別的AccessEnabler都可以使用呼叫。

### checkPreauthorizedResources(Array：resources)：void {#checkPreauthRes}

在AccessEnabler物件上呼叫此函式，以請求資源清單的授權狀態。

resources引數是應檢查其授權的資源清單。 清單中的每個元素都應是代表資源ID的字串。 資源ID的限制與 `getAuthorization()` 呼叫，也就是說，程式設計師和MVPD或媒體RSS片段之間建立的值已商定。 請注意，Adobe Primetime驗證不會以任何方式管理資源，除了根據MVPD實際支援的內容來轉換資源格式的精簡中繼層。

### preauthorizedResources(Array：authorizedResources) {#preauthRes}

這是一個回呼函式，必須在程式設計人員的上層應用程式中實作。 AccessEnabler會在計算授權資源清單後呼叫此函式。


### JS範例

```javascript
    checkPreauthorizedResources(["CNBC","MSNBC"]);
    ...
    preauthorizedResources() {
        var resource = arguments[0];
        for(i in resources) {
            // Do things with resource list
            // such as decorate UI
            ...
        }
    }
```

## 實作資訊 {#details}

- [使用ChannelID預檢](#preflight_using_channelID)
- [POST/預先授權](#post)
- [儲存](#storage)

API呼叫會嘗試在使用者端的本機儲存空間中尋找目前使用者的已授權資源快取清單。 如果沒有快取清單，則會對AdobePass伺服器進行HTTPS呼叫，以擷取清單。

快取機制會透過完全略過網路呼叫來改善後續呼叫的效能時間。 此外，快取清單可在驗證程式中預先填入。  (如需設定此情境的相關資訊，請參閱 [Preflight授權整合](/help/authentication/authz-usecase.md#preflight_authz_int) （位於MVPD整合指南的授權區段）。

此外，快取的資源清單可能會用於最佳化授權流程，因為如果存在快取的資源清單， `checkAuthorization()` 可以在執行網路呼叫之前檢查它。 如果資源不在預先授權的資源清單中，則檢查可能會失敗，而無需呼叫Primetime驗證伺服器。


### 使用ChannelID預檢 {#preflight_using_channelID}

從Primetime驗證2.4.1版開始，Preflight流程的工作方式如下：

1. 驗證期間，Primetime驗證會讀取 `channelIID` 元素，並使用此值來設定 `authorizedResources` 個元素。
1. 內部 `checkPreauthorizedResources()` API函式，Primetime驗證會檢查 `authorizedResources` 元素已設定。
1. 如果 `authorizedResources` 元素已設定，Primetime驗證會讀取該值，並從以下位置執行資源清單之間的交集： `authorizedResources` 元素和從收到的資源清單 `checkPreauthorizedResources()` 引數。  此交集的結果是預先授權資源的最終清單。
1. 如果 `authorizedResources` 元素未設定，請執行先前實作的流程，其中會包含從以下來源收到的資源清單 `checkPreauthorizedResources()` 引數會傳遞至PreAuthorizationServlet。 此servlet會對MVPD端點執行授權呼叫，並傳回預先授權的資源清單。

### 使用ChannelID預檢的範例

以下範例顯示管道排列範例。 請注意，用於傳送管道清單的屬性名稱可能因一個MVPD而異：

```XML
    <saml:Attribute Name="visible_channels" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
        <saml:AttributeValue xsi:type="xs:string">MSNBC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">CNBC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">FBN</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">FNC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TNT</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TBS</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">CNN</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TRUTV</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TOON</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">HBO</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">MAX</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">EPIXHD</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">BTN-BTN2GO</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">SPEED-SPEED2</saml:AttributeValue>
    </saml:Attribute>
```
 

此 `authorizedResources` 驗證元素中的元素如下所示：

```JSON
    <authorizedResources>
        <authorizedResource resourceID="MSNBC"/>
        <authorizedResource resourceID="CNBC"/>
        <authorizedResource resourceID="FBN"/>
        <authorizedResource resourceID="FNC"/>
        <authorizedResource resourceID="TNT"/>
        <authorizedResource resourceID="TBS"/>
        <authorizedResource resourceID="CNN"/>
        <authorizedResource resourceID="TRUTV"/>
        <authorizedResource resourceID="TOON"/>
        <authorizedResource resourceID="HBO"/>
        <authorizedResource resourceID="MAX"/>
        <authorizedResource resourceID="EPIXHD"/>
        <authorizedResource resourceID="BTN-BTN2GO"/>
        <authorizedResource resourceID="SPEED-SPEED2"/>
    </authorizedResources>
```

程式設計師執行 `checkPreauthorizedResources()` API呼叫，傳遞下列引數清單：</span>

- &quot;MSNBC&quot; 
- &quot;FBN&quot; 
- 「訊通科技」
- &quot;fbc-fox&quot;

目前的「預檢」實作會使用來自下列專案的資源清單來執行交集： `authorizedResources` 元素並傳回此清單：

- &quot;MSNBC&quot;
- &quot;FBN&quot;
- 「訊通科技」

 

**注意：** 請注意，交集不區分大小寫。

 

### POST/預先授權 {#post}

當不存在快取、授權的資源清單時，AccessEnabler會自動執行此呼叫。 


#### 請求 {#req}

| 引數 | 型別 | 必填 | 說明 |
| --- | --- | --- | --- |
| `authentication_token` | 字串 | 是 | 驗證Token。 |
| `resource_id` | 字串 | 是 | 單一資源。 您可以針對中提供的資源陣列的每個元素指定多次，一次即可 `checkPreauthorizedResources()` API呼叫。 |


**注意：** 可設定請求資源的最大數量。
**最大預設值為5。**


#### 回應 {#resp}

預先授權servlet傳回的回應具有以下格式：

```XML
    <?xml version="1.0" encoding="UTF-8"?>
    <resources>
      <resource>
        <id>TNT</id>
        <authorized>true</authorized>
      </resource>
      <resource>
        <id>TBS</id>
        <authorized>true</authorized>
      </resource>
      <resource>
        <id>CNN</id>
        <authorized>false</authorized>
      </resource>
    </resources>
```

### 儲存 {#storage}

AccessEnabler從服務提供者取得的預先授權資源清單。 此資源清單：

- 會與AuthN和AuthZ權杖一起儲存
- 只要使用者位於相同網站，或直到AuthN權杖過期為止，即有效
- 每次使用者登陸新的Primetime驗證整合網站時都會重新擷取

每個專案都包含使用者預先授權的資源ID。

例如：


| 資源ID | 已授權 |
| ----------- | ---------- |
| CNN | true |
| TNT | false |
| ... | ... |


此清單名為「預先授權快取」。

#### 流量 {#flow}

1. 程式設計師的應用程式/網站製作 `checkPreauthorizedResources(resourceList)` 呼叫。
1. AccessEnabler會驗證授權資源的驗證Token：
   1. 如果驗證Token包含授權資源 — 此清單具有權威性，不應進行呼叫來取得此資訊。 在驗證Token上的授權資源清單中搜尋來自resourceList的資源，並且只傳回找到的資源。 `preauthorizedResources()` callback。
   1. 如果驗證Token DOES NOT contain authorized resources - `resourceList` 會與預先授權快取中的資源清單進行比較。
      1. 如果清單包含相同的資源 — 這表示已呼叫伺服器，而且回應已在預先授權快取中。 只有獲授權的資源才會由傳回 `preauthorizedResources()` callback。
      1. 如果清單不包含相同的資源 — 使用者端需要呼叫伺服器，才能取得resourceList中資源的授權狀態。 回應將會擷取並儲存在預先授權快取中，完全取代舊資源。 只有獲授權的資源才會由傳回 `preauthorizedResources()` callback。


#### 清單擷取 {#listRetrieve}

每當 `checkPreauthorizedResources()` 會呼叫，根據預先授權快取檢查要驗證授權的資源清單。 如果清單包含相同的資源集，則不會呼叫服務提供者，因為觸發 `preauthorizedResources()` 快取中已存在回呼。


#### logout() {#logout}

登出時會清空預先授權快取。


## 相依性 {#depends}

Preflight API的效能取決於特定的MVPD實作。  如需實作選項，請參閱 [Preflight授權整合](/help/authentication/authz-usecase.md#preflight_authz_int) MVPD整合指南的授權區段。


## 安全性 {#security}

使用者端API可供所有程式設計師使用。

實作使用HTTPS作為傳輸，但為了呼叫更輕，不採用其他安全性措施（無簽署、無FAXS）。

**注意：** 請勿以授權方式使用此API來判斷是否應授予使用者對受保護資源的存取權。 此API的用途是UI裝飾和/或預先決定業務決策。 此 `getAuthorization()` 和 `checkAuthorization()` 呼叫一律應在允許播放之前進行。


## 相容性 {#compat}

AccessEnabler的所有版本都支援此功能： AS、JS、AIR、iOS、Android、Xbox （在第2個畫面的AuthN流程中）。

預檢授權不支援包含CDATA區段的預先授權資源。 目前預檢系統的重點是支援頻道層級篩選。 包含CDATA區段的資源可能是資產層級的資源。 預檢不支援簡單操作 `mrss` 管道層級預先授權的資源，只要不包含CDATA即可。 

## 與其他功能整合 {#integ_w_other_features}

如果資源不在預先授權的資源清單中，授權流程可能會發生可能的最佳化，以便快速失敗。

在此最佳化中，伺服器預檢端點會與降級機制整合。  

如果MVPD和請求者的「AuthN All」規則已就緒，預檢端點只會映象回請求中收到的所有資源。

如果至少為請求中存在的其中一個資源啟用「AuthZ All」，則相同情況亦然。

<!--
## Related Information

  - `checkPreauthorizedResources()`
      - [iOS](#checkPreauth)
      - [Android](#checkPreauth)
      - [JavaScript](#checkPreauthRes)
      - [ActionScript](#checkPreauthRes)
  - [Xbox](#2nd%20Screen%20Authentication)
  - [MVPD Integration Guide: Preflight AuthZ](#)
-->
