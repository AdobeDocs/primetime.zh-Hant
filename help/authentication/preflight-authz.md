---
title: 預檢授權
description: 預檢授權
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 0%

---



# 預檢授權 {#preflight-authorization}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

</br>

## 概述 {#overview}

此功能提供適用於多個資源的輕量型授權檢查。 此輕量型檢查的目的是裝飾UI（例如，使用鎖定和解除鎖定圖示指示存取狀態）。 預檢授權盡可能輕巧且有效，因此單一API呼叫會產生資源清單的授權狀態。 請注意，此功能在授權資源方面並不權威。

A `getAuthorization(resource)` 或 `checkAuthorization(resource)` 在允許播放前，仍必須進行呼叫。

預檢授權還支援不同的使用案例，其中程式設計師需要請求對多個資源ID的授權，以便允許播放一個媒體內容項。 程式設計師可以對所需資源進行初始預檢檢查，如果不滿足業務條件，則根據響應情況可能會過早失敗。

如需支援預檢授權的MVPD清單，請參閱 [MVPD預檢授權](/help/authentication/mvpd-preflight-authz.md#preflight_support_list) 頁面。 

>[!NOTE]
>
> 請注意，若MVPD未具備完整的飛行前授權支援，必須事先與Adobe和MVPD同意使用此功能。 在這些MVPD上使用飛行前授權將屬於描述的「最壞情況」 [此處](/help/authentication/mvpd-preflight-authz.md#intro) 而且會導致效能問題和回應時間緩慢。 </br>
> 此外，請注意，使用預檢授權時， **需要由Adobe明確同意5個以上的資源**.

## AccessEnabler預檢API {#AE_pre_api}

AccessEnabler公開API/回撥函式對，以實施預檢授權。 API呼叫會採用由資源清單組成的單一參數。 回呼函式會採用單一參數，代表實際授權資源。 以下示例在ActionScript中，但調用在AccessEnabler的所有類型中都可用。

### checkPreauthorizedResources(Array:resources):void {#checkPreauthRes}

在AccessEnabler對象上調用此函式，以請求資源清單的授權狀態。

資源參數是應檢查授權的資源清單。 清單中的每個元素都應是代表資源ID的字串。 資源ID受與 `getAuthorization()` 呼叫，即在程式設計師和MVPD或媒體RSS片段之間建立的值上達成一致。 請注意，Adobe Primetime驗證不會以任何方式管理資源，但精簡中介層除外，該中介層可根據MVPD實際支援的內容來轉換資源格式。

### preauthorizedResources(Array:authorizedResources) {#preauthRes}

這是一個回調函式，必須在程式設計師的上層應用程式中實現。 計算授權資源清單後，AccessEnabler將調用此函式。


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

API呼叫會嘗試在用戶端的本機儲存體中，尋找目前使用者的已授權資源快取清單。 如果沒有快取清單，會對AdobePass伺服器發出HTTPS呼叫以擷取清單。

快取機制會完全略過網路呼叫，以改善後續呼叫的效能時間。 此外，快取清單可作為驗證程式的一部分預先填入。  (如需設定此案例的詳細資訊，請參閱 [預檢授權整合](/help/authentication/authz-usecase.md#preflight_authz_int) （位於MVPD整合指南的授權區段）。

此外，快取的資源清單可能可用於優化授權流程，即如果存在快取的資源清單， `checkAuthorization()` 可以在執行網路呼叫前先進行檢查。 如果資源不在預先授權的資源清單中，則檢查可能會失敗，而不需要呼叫Primetime驗證伺服器。


### 使用ChannelID預檢 {#preflight_using_channelID}

從Primetime驗證2.4.1版開始，預檢流程的運作方式如下：

1. 在驗證期間，Primetime驗證會讀取 `channelIID` 元素，並使用此值來設定 `authorizedResources` 元素。
1. 內 `checkPreauthorizedResources()` API函式，Primetime驗證會檢查 `authorizedResources` 元素已設定。
1. 若 `authorizedResources` 元素已設定，Primetime驗證會讀取該值，並從中執行資源清單之間的交集 `authorizedResources` 元素和從 `checkPreauthorizedResources()` 參數。  此交集的結果是預授權資源的最終清單。
1. 若 `authorizedResources` 元素未設定，請執行先前實作的流程，其中接收自 `checkPreauthorizedResources()` 參數會傳遞至PreAuthorizationServlet。 此Servlet會執行對MVPD端點的授權呼叫，並傳回預先授權資源清單。

### 使用ChannelID進行預檢的範例

以下範例顯示範例管道陣列。 請注意，用於傳送頻道清單的屬性名稱可能會因一個MVPD而異：

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
 

此 `authorizedResources` 驗證元素中的元素顯示如下：

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

程式設計師執行 `checkPreauthorizedResources()` API呼叫，傳遞下列參數清單：</span>

- &quot;MSNBC&quot; 
- &quot;FBN&quot; 
- &quot;TruTV&quot;
- &quot;fbc-fox&quot;

目前的Preflight實施會執行與 `authorizedResources` 元素並傳回此清單：

- &quot;MSNBC&quot;
- &quot;FBN&quot;
- &quot;TruTV&quot;

 

**注意：** 請注意，交集區不區分大小寫。

 

### POST/預先授權 {#post}

當不存在快取、授權的資源清單時，AccessEnabler將自動執行此調用。 


#### 要求 {#req}

| 參數 | 類型 | 必填 | 說明 |
| --- | --- | --- | --- |
| `authentication_token` | 字串 | 是 | 驗證Token。 |
| `resource_id` | 字串 | 是 | 單一資源。 可以多次指定，一次適用於 `checkPreauthorizedResources()` API呼叫。 |


**注意：** 可配置請求的資源的最大數量。
**預設值上限為5。**


#### 回應 {#resp}

預先授權servlet傳回的回應格式如下：

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

AccessEnabler從服務提供程式獲取的預授權資源清單。 此資源清單：

- 會與AuthN和AuthZ代號一起儲存
- 只要使用者位於相同的網站，或直到AuthN代號過期為止，都有效
- 每次使用者登陸新的Primetime驗證整合網站時，都會重新擷取

每個條目都包含用戶預授權的資源ID。

例如：


| 資源ID | 已授權 |
| ----------- | ---------- |
| CNN | true |
| TNT | false |
| ... | ... |


此清單名為「預授權快取」。

#### 流量 {#flow}

1. 程式設計師的應用程式/站點使 `checkPreauthorizedResources(resourceList)` 呼叫。
1. AccessEnabler驗證授權資源的驗證令牌：
   1. 如果驗證Token包含授權資源 — 此清單為授權，則不應進行呼叫以取得此資訊。 在驗證Token上的授權資源清單內，會搜尋resourceList中的資源，而只會傳回找到的資源 `preauthorizedResources()` 回呼。
   1. 如果驗證Token DOES NOT contain authorized resources - `resourceList` 會與預先授權快取中的資源清單進行比較。
      1. 如果清單包含相同的資源，這表示已對伺服器進行呼叫，且回應已在預先授權快取中。 只有已授權的資源才會由 `preauthorizedResources()` 回呼。
      1. 如果清單DOES NOT包含相同的資源，則客戶端需要對伺服器進行調用，才能獲得resourceList中資源的授權狀態。 回應會擷取並儲存在預先授權快取中，完全取代舊資源。 只有已授權的資源才會由 `preauthorizedResources()` 回呼。


#### 清單檢索 {#listRetrieve}

每當 `checkPreauthorizedResources()` 調用時，根據預授權快取檢查要驗證授權的資源清單。 如果清單包含同一組資源，則不會對服務提供商進行調用，因為觸發 `preauthorizedResources()` 回呼已在快取中。


#### logout() {#logout}

註銷時，預授權快取被清空。


## 相依性 {#depends}

預檢API的效能取決於特定MVPD實作。  如需實作選項，請參閱 [預檢授權整合](/help/authentication/authz-usecase.md#preflight_authz_int) （位於MVPD整合指南的授權區段）。


## 安全性 {#security}

客戶端API可供所有程式設計師使用。

實作使用HTTPS作為傳輸，但為了讓呼叫更輕，不採用其他安全措施（無簽署、無FAXS）。

**注意：** 請勿以授權方式使用此API，以判斷是否應將使用者授與受保護資源的存取權。 此API的用途為UI裝飾及/或預先進行業務決策。 此 `getAuthorization()` 和 `checkAuthorization()` 一律應在允許播放前進行呼叫。


## 相容性 {#compat}

AccessEnabler的所有類型均支援此功能：AS、JS、AIR、iOS、Android、Xbox（在第2螢幕AuthN流程中）。

預檢授權不支援包含CDATA節的預授權資源。 當前預飛系統的重點是支援通道級濾波。 具有CDATA部分的資源可能是資產級資源。 預檢支援簡單 `mrss` 用於通道級預授權的資源，只要它們不包含CDATA。 

## 與其他功能整合 {#integ_w_other_features}

如果資源不在預授權資源清單中，則可能的優化可以發生在授權流程上，以便快速失敗。

在此最佳化中，伺服器預檢端點與退化機制整合。  

如果MVPD和請求者已採用「AuthN全部」規則，預檢端點只會鏡像回請求中收到的所有資源。

如果至少為請求中存在的一個資源啟用「AuthZ全部」，則情況相同。

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
