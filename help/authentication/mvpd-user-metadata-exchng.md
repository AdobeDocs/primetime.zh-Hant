---
title: MVPD用戶元資料交換
description: MVPD用戶元資料交換
exl-id: 8bce6acc-cd33-476c-af5e-27eb2239cad1
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---

# MVPD用戶元資料交換

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 導言 {#intro-user-metadata-exchange}

MVPD維護與其客戶有關的用戶特定元資料，在某些情況下，這些元資料與程式設計師共用。 Adobe Primetime認證的目的是代理此&quot;用戶元資料&quot;的交換，但不是強制執行任何有關交換的規則。 交換規則是讓MVPD與其程式設計師合作夥伴合作。

可用於交換的用戶元資料類型當前包括以下內容：

* 郵遞區號
* 最大額定值（VChip或MPAA）
* 用戶ID
* 家庭ID
* 通道ID

使用此功能，MVPD和程式設計師可以實施特殊的使用情形，如家長控制。 例如，MVPD可以將家長評級資料傳遞給程式設計師，程式設計師隨後使用該資料篩選用戶的可用查看選項。

用戶元資料關鍵點：

* 在驗證和授權流程期間，MVPD將用戶元資料傳遞給程式設計師的應用程式
* Adobe Primetime身份驗證將元資料值保存在AuthN和AuthZ令牌中
* Adobe Primetime身份驗證可以標準化MVPD的值，這些值以不同格式提供用戶元資料
* 使用程式設計師密鑰可以加密某些參數
* 通過配置更改，Adobe提供特定值

>[!NOTE]
>
>用戶元資料是以前在Adobe Primetime驗證中可用的靜態元資料（驗證令牌TTL、授權令牌TTL和設備ID）的擴展。

## 示例 {#example-mvpd-user-metadata-exch}

### 家長控制 {#example-parental-control}

此示例顯示了以下內容的交換：

* [程式設計師到MVPD元資料交換](#progr-mvpd-metadata-exch)

* [MVPD到程式設計師元資料交換流](#mvpd-progr-exchange-flow)

### 程式設計師到MVPD元資料交換 {#progr-mvpd-metadata-exch}

目前程式設計師API、Adobe Primetime身份驗證和MVPD授權程式都只支援通道級授權。 該通道在Programmer&#39;s getAuthorization()API調用中被指定為純文字檔案字串。 此字串一直傳播到MVPD的授權後端：

在程式設計師應用或站點中，用戶選擇支援XACML的MVPD（在本例中為「TNT」）。 有關XACML的資訊，請參見 [可擴展訪問控制標籤語言](https://en.wikipedia.org/wiki/XACML){target=_blank}。
程式設計師應用程式形成包括資源及其元資料的AuthZ請求。  此示例包括通道元素媒體屬性中「pg」的MPAA分級：

```XML
var resource = '<rss version="2.0" xmlns:media="http://video.search.yahoo.com/mrss/">
                    <channel> 
                        <title>TNT</title> 
                        <media:rating scheme="urn:mpaa">pg</media:rating>
                    </channel>
                </rss>';
getAuthorization(resource);
```

Adobe Primetime身份驗證實際上支援更細粒度的授權，如果MVPD和程式設計師都支援，則可以直到資產級別。 資源及其元資料不透明，無法Adobe;目的是建立標準格式，用於以規範化方式指定資源ID和元資料，以便將資源ID發送到不同的MVPD。

>[!NOTE]
>
>如果用戶選擇只支援通道的MVPD，則Adobe Primetime驗證只提取通道標題（上例中的「TNT」），並僅將標題傳遞給MVPD。

### MVPD到程式設計師元資料交換流 {#mvpd-progr-exchange-flow}

Adobe Primetime驗證作如下假設：

* MVPD將最大評級作為SAML響應的一部分發送
* 此資訊作為驗證令牌的一部分保存
* Adobe Primetime驗證提供API，使程式設計師能夠檢索此資訊
* 程式設計師在其站點或應用上實施此功能（例如，隱藏超出用戶最大分級的視頻）

```XML
<saml:Assertion ID="pfxec5f92e0-8589-3fc3-c708-f4fb8e2fad59"
                 IssueInstant="2010-07-20T10:05:41Z" Version="2.0"
                 xmlns:xs="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <saml:AttributeStatement>
        <saml:Attribute
                Name="MaxTVRating"
                NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
            <saml:AttributeValue xsi:type="xs:string">tv-ma</saml:AttributeValue>
        </saml:Attribute>
        <saml:Attribute
                Name="MaxMovieRating"
                NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
            <saml:AttributeValue xsi:type="xs:string">nc-17</saml:AttributeValue>
        </saml:Attribute>
    </saml:AttributeStatement>
</saml:Assertion>
```

### 注釋 {#notes-mvpd-progr-metadata-exch-flow}

**資源規範化和驗證。** 資源ID可以作為純字串或MRSS字串傳遞。 程式設計師可以決定使用純字串格式或MRSS，但需要與MVPD達成事先協定，以便MVPD知道如何處理該資源。

**資源ID和元資料規範。** Adobe Primetime身份驗證使用RSS標準和媒體RSS擴展來指定資源及其元資料。 與媒體RSS擴展結合，Adobe Primetime身份驗證支援多種元資料，如家長控制(通過 `<media:rating>`)或地理位置(`<media:location>`)。

Adobe Primetime身份驗證還支援將傳統通道字串透明地轉換為需要RSS的MVPD的相應RSS資源。 在另一方面，Adobe Primetime認證支援從RSS+MRSS轉換為純通道標題（對於僅通道的MVPD）。

**Adobe Primetime身份驗證確保與現有整合完全向後相容。** 即，對於使用通道級身份驗證的程式設計師，Adobe Primetime身份驗證會在將通道ID發送到理解該格式的MVPD之前，注意將其打包為必要格式。 相反的情況也適用：如果程式設計師以新格式指定其所有資源，則Adobe Primetime驗證將新格式轉換為簡單的通道字串（如果僅對MVPD授權）。

## 用戶元資料使用案例 {#user-metadata-use-cases}

隨著越來越多的MVPD做出法律安排並添加功能，使用案例不斷變化和擴展。 以下是可用於哪些用戶元資料的示例。

* [MVPD用戶ID](#mvpd-user-id)
* [家庭ID](#household-user-id)
* [郵遞區號](#zip-code)
* [最大評級（家長控制）](#max-rating-parental-control)
* [頻道陣容](#channel-line-up)

### MVPD用戶ID {#mvpd-user-id}

* MVPD提供
* 不是用戶的實際登錄資訊，因為MVPD對它進行了散列
* 可用於指示特定用戶或特定用戶的問題
* 加密
* MVPD支援：所有MVPD

### 家庭用戶ID {#household-user-id}

* 允許提供良好的度量資訊
* 加密
* MVPD支援：某些MVPD

### 郵遞區號 {#zip-code}

* 用戶的帳單郵遞區號
* 主要用於強制實施體育賽事凍結期間規則
* 可以提供AuthZ響應以快速更新
* MVPD支援：某些MVPD

### 最大評級（家長控制） {#max-rating-parental-control}

* 初始AuthN加上AuthZ刷新
* 從UI中篩選內容
* MPAA或VChip評級
* MVPD支援：某些MVPD

### 頻道陣容 {#channel-line-up}

* MVPD可以提供用戶有權查看的頻道清單
* 允許快速UI繪畫
* OLCA規範允許在AuthN響應中將其作為AttributeStatement
* 支援MVPD:某些MVPD

<!--
>[!RELATEDINFORMATION]
>
>* [Proxy MVPD Web Service](/help/authentication/proxy-mvpd-webserv.md)
>* [Content Metadata Exhange](/help/authentication/mvpd-content-metadata-exchange.md)
>* [OLCA AuthN / AuthZ Specification](https://www.cablelabs.com/specifications/CL-SP-AUTH1.0-I04-120621.pdf){target=_blank}
>* [User Metadata (Programmer Integration Guide)](/help/authentication/user-metadata-feature.md)
-->
