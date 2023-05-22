---
title: 印前檢查授權
description: 印前檢查授權
exl-id: 036b1a8e-f2dc-4e9a-9eeb-0787e40c00d9
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 0%

---

# 印前檢查授權 {#preflight-authorization}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>

## 概述 {#overview}

此功能為多個資源提供輕量授權檢查。 此輕量檢查的目的是裝飾UI（例如，使用鎖定和解鎖表徵圖指示訪問狀態）。 印前檢查授權盡可能輕巧和高效，使得單個API調用產生資源清單的授權狀態。 請注意，此功能在授權資源方面不具權威性。

A `getAuthorization(resource)` 或 `checkAuthorization(resource)` 在允許播放之前，仍必須進行呼叫。

印前檢查授權還為不同的使用情形提供支援，在該使用情形中，程式設計師需要請求對多個資源ID的授權，以便允許回放一項媒體內容。 程式設計師可以對所需資源進行初始印前檢查，如果不滿足業務條件，可能會提前失敗，具體取決於響應。

有關支援印前檢查授權的MVPD的清單，請參見 [MVPD印前檢查授權](/help/authentication/mvpd-preflight-authz.md#preflight_support_list) 的子菜單。 

>[!NOTE]
>
> 請注意，對於沒有完全飛行前授權支援的MVPD，需要事先與Adobe和MVPD商定使用此功能。 在這些MVPD上使用印前檢查授權將陷入描述的「最壞情況」 [這裡](/help/authentication/mvpd-preflight-authz.md#intro) 而且會導致效能問題和響應時間過慢。 </br>
> 另外，請注意，使用 **需要經Adobe明確同意5個以上的資源**。

## AccessEnabler預檢API {#AE_pre_api}

AccessEnabler公開API/回調函式對以實現印前檢查授權。 API調用採用由資源清單組成的單個參數。 回調函式採用一個表示實際授權資源的參數。 以下示例在ActionScript中，但AccessEnabler的所有類型都提供了這些調用。

### checkPreauthorizedResources(Array:resources):void {#checkPreauthRes}

在AccessEnabler對象上調用此函式以請求資源清單的授權狀態。

resources參數是應檢查其授權的資源清單。 清單中的每個元素都應是表示資源ID的字串。 資源ID受與 `getAuthorization()` 呼叫，即，在程式設計師和MVPD或媒體RSS片段之間建立的值上達成一致。 請注意，Adobe Primetime身份驗證不會以任何方式管理資源，但是只有一個細中介層可以根據MVPD實際支援的內容來轉換資源格式。

### preauthorizedResources(Array:authorizedResources) {#preauthRes}

這是一個回調函式，必須在程式設計師的上層應用程式中實現。 計算授權資源清單後，AccessEnabler將調用此函式。


### JS示例

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

## 實施資訊 {#details}

- [使用ChannelID進行印前檢查](#preflight_using_channelID)
- [POST/預授權](#post)
- [儲存](#storage)

API調用嘗試在客戶端的本地儲存中查找當前用戶的已授權資源的快取清單。 如果沒有快取清單，則會對AdobePass伺服器進行HTTPS調用以檢索清單。

該快取機制通過完全跳過網路呼叫來改善後續呼叫的效能時間。 另外，作為驗證過程的一部分，可預先填充快取清單。  (有關設定此方案的資訊，請參見 [印前檢查授權整合](/help/authentication/authz-usecase.md#preflight_authz_int) 在「MVPD整合指南」的「授權」部分。

此外，快取的資源清單可能被用於優化授權流，即如果存在快取的資源清單， `checkAuthorization()` 可以在進行網路呼叫前檢查。 如果該資源不在預授權資源清單中，則檢查可能會失敗，而無需調用黃金時段驗證伺服器。


### 使用ChannelID進行印前檢查 {#preflight_using_channelID}

從黃金時段驗證2.4.1版開始，印前檢查流的工作方式如下：

1. 在驗證期間，Mighide驗證會讀取 `channelIID` MVPD的SAML響應中的元素，並使用此值設定 `authorizedResources` 驗證令牌中的元素。
1. 在 `checkPreauthorizedResources()` API函式，Mogife身份驗證檢查 `authorizedResources` 元素已設定。
1. 如果 `authorizedResources` 元素被設定，黃金時段驗證讀取該值並執行資源清單之間的交叉 `authorizedResources` 元素和從 `checkPreauthorizedResources()` 的下界。  此交叉點的結果是預授權資源的最終清單。
1. 如果 `authorizedResources` 未設定元素，執行先前實現的流，在該流中從 `checkPreauthorizedResources()` 參數將傳遞給PreAuthorizationServlet。 此servlet執行對MVPD端點的授權調用並返回預授權資源清單。

### ChannelID的預檢示例

以下示例顯示了一個示例通道配置。 請注意，用於發送通道清單的屬性名稱可能不同於一個MVPD:

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
 

的 `authorizedResources` 驗證元素的元素如下所示：

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

程式設計師執行 `checkPreauthorizedResources()` API調用，傳遞以下參數清單：</span>

- &quot;MSNBC&quot; 
- &quot;FBN&quot; 
- &quot;TruTV&quot;
- &quot;fbc-fox&quot;

當前的印前檢查實現執行與 `authorizedResources` 元素並返回此清單：

- &quot;MSNBC&quot;
- &quot;FBN&quot;
- &quot;TruTV&quot;

 

**注：** 請注意，交叉點不區分大小寫。

 

### POST/預授權 {#post}

當不存在快取、授權、資源清單時，AccessEnabler將自動執行此調用。 


#### 請求 {#req}

| 參數 | 類型 | 必需 | 說明 |
| --- | --- | --- | --- |
| `authentication_token` | 字串 | 是 | 驗證令牌。 |
| `resource_id` | 字串 | 是 | 單個資源。 可以多次指定此值，一次是為中提供的資源陣列的每個元素 `checkPreauthorizedResources()` API調用。 |


**注：** 可配置請求的資源的最大數量。
**最大預設值為5。**


#### 響應 {#resp}

預授權servlet發回的響應具有以下格式：

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

AccessEnabler從服務提供商獲取的預授權資源清單。 此資源清單：

- 與AuthN和AuthZ令牌一起儲存
- 只要用戶位於同一網站上，或直到AuthN令牌過期為止，該功能有效
- 每次用戶登陸新的Gimphire驗證整合網站時都會重新檢索

每個條目都包含用戶預授權的資源ID。

例如：


| 資源ID | 授權 |
| ----------- | ---------- |
| 美國有線電視新聞網 | 真 |
| 梯恩梯 | 假 |
| ... | ... |


此清單名為「預授權快取」。

#### 流 {#flow}

1. 程式設計師應用/站點 `checkPreauthorizedResources(resourceList)` 呼叫。
1. AccessEnabler驗證授權資源的身份驗證令牌：
   1. 如果驗證令牌包含授權資源 — 此清單是授權的，則不應進行任何呼叫以獲取此資訊。 在驗證令牌上的授權資源清單中搜索resourceList中的資源，並且僅返回找到的資源 `preauthorizedResources()` 回叫。
   1. 如果驗證令牌不包含授權資源 —  `resourceList` 與預授權快取中的資源清單進行比較。
      1. 如果清單包含相同的資源 — 這意味著已對伺服器進行調用，並且響應已在預授權快取中。 只有已授權的資源將由 `preauthorizedResources()` 回叫。
      1. 如果清單不包含相同的資源，則客戶端需要調用伺服器以獲取resourceList中資源的授權狀態。 響應將被讀取並儲存在預授權快取中，完全替換舊資源。 只有已授權的資源將由 `preauthorizedResources()` 回叫。


#### 清單檢索 {#listRetrieve}

只要 `checkPreauthorizedResources()` 調用時，會根據預授權快取檢查要驗證授權的資源清單。 如果清單包含相同的一組資源，則不會調用服務提供商，因為觸發該資源所需的所有資源 `preauthorizedResources()` 回調已在快取中。


#### 註銷() {#logout}

註銷時，預授權快取被清空。


## 依賴項 {#depends}

印前檢查API的效能取決於特定的MVPD實現。  有關實施選項，請參見 [印前檢查授權整合](/help/authentication/authz-usecase.md#preflight_authz_int) 在「MVPD整合指南」的「授權」部分。


## 安全 {#security}

客戶端API可供所有程式設計師使用。

該實現使用HTTPS作為傳輸，但為了進行更輕的調用，不使用其他安全措施（不簽名，不使用FAXS）。

**注意：** 請勿以權威方式使用此API來確定是否應授予用戶對受保護資源的訪問權限。 此API的目的是UI裝飾和/或預先制定業務決策。 的 `getAuthorization()` 和 `checkAuthorization()` 在允許播放之前，應始終進行呼叫。


## 相容性 {#compat}

AccessEnabler的所有類型都支援此功能：AS、JS、AIR、iOS、Android、Xbox（在第2螢幕AuthN流中）。

印前檢查授權不支援包含CDATA節的預授權資源。 當前飛行前系統的重點是支援通道級濾波。 具有CDATA部分的資源可能是資產級資源。 印前檢查支援簡單 `mrss` 渠道級預授權的資源，只要它們不包含CDATA。 

## 與其他功能整合 {#integ_w_other_features}

如果資源不在預授權資源清單中，則可能在授權流上進行優化，以便快速失敗。

在此優化中，伺服器預檢端點與降級機制整合。  

如果MVPD和請求方有「AuthN全部」規則，則印前檢查終結點只需鏡像請求中接收的所有資源。

如果為請求中至少存在的一個資源啟用了「AuthZ全部」，則情況也相同。

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
