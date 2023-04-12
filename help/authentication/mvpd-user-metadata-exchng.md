---
title: MVPD用戶元資料交換
description: MVPD用戶元資料交換
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---


# MVPD用戶元資料交換

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 簡介 {#intro-user-metadata-exchange}

MVPD會維護與其客戶有關的使用者專屬中繼資料，在某些情況下會與程式設計人員共用。 Adobe Primetime驗證的目的是代理此「用戶元資料」的交換，但不是強制執行與交換相關的任何規則。 交換規則是讓MVPD與其程式設計師合作夥伴一起制定的。

可用於exchange的使用者中繼資料類型目前包含下列項目：

* 郵遞區號
* 最高評級（VChip或MPAA）
* 使用者ID
* 家庭ID
* 管道ID

使用此功能，MVPD和程式設計人員可實作特殊使用案例，例如家長控制。 例如，MVPD可以將父級評等資料傳遞給程式設計師，然後程式設計師使用該資料來篩選用戶可用的查看選擇。

用戶元資料關鍵點：

* 在驗證和授權流程期間，MVPD將用戶元資料傳遞給程式設計師的應用程式
* Adobe Primetime驗證會將中繼資料值儲存在AuthN和AuthZ代號中
* Adobe Primetime驗證可標準化以不同格式提供使用者中繼資料之MVPD的值
* 某些參數可以使用程式設計師的密鑰進行加密
* 特定值可由Adobe透過組態變更使用

>[!NOTE]
>
>使用者中繼資料是Adobe Primetime驗證中可用之靜態中繼資料（驗證Token TTL、授權Token TTL和裝置ID）的擴充功能。

## 範例 {#example-mvpd-user-metadata-exch}

### 家長控制 {#example-parental-control}

此範例顯示下列項目的交換：

* [MVPD元資料交換的程式設計師](#progr-mvpd-metadata-exch)

* [MVPD到程式設計師元資料交換流](#mvpd-progr-exchange-flow)

### MVPD元資料交換的程式設計師 {#progr-mvpd-metadata-exch}

目前，程式設計師API、Adobe Primetime驗證和MVPD授權程式均僅支援通道層級授權。 該通道在程式設計師的getAuthorization()API調用中被指定為純文字檔案字串。 此字串會一直傳播至MVPD的授權後端：

從程式設計師的應用程式或站點中，用戶選擇支援XACML的MVPD（在此示例中，為「TNT」）。 有關XACML的資訊，請參見 [擴展訪問控制標籤語言](https://en.wikipedia.org/wiki/XACML){target=_blank}.
程式設計師的應用程式會形成AuthZ請求，該請求包含資源及其元資料。  此範例包含通道元素之媒體屬性中的MPAA評等為&quot;pg&quot;:

```XML
var resource = '<rss version="2.0" xmlns:media="http://video.search.yahoo.com/mrss/">
                    <channel> 
                        <title>TNT</title> 
                        <media:rating scheme="urn:mpaa">pg</media:rating>
                    </channel>
                </rss>';
getAuthorization(resource);
```

Adobe Primetime驗證實際上支援更精細的授權，包括資產層級，只要同時受到MVPD和程式設計人員支援。 資源及其元資料不透明，無法Adobe;目的是建立標準格式，以標準化方式指定資源ID和元資料，以將資源ID發送到不同的MVPD。

>[!NOTE]
>
>如果使用者選擇僅能使用頻道的MVPD,Adobe Primetime驗證只會擷取頻道標題（上述範例中為「TNT」），並只將標題傳給MVPD。

### MVPD到程式設計師元資料交換流 {#mvpd-progr-exchange-flow}

Adobe Primetime驗證會進行下列假設：

* MVPD會在SAML回應中傳送最大評等
* 此資訊會儲存為驗證Token的一部分
* Adobe Primetime驗證提供API，讓程式設計人員可擷取此資訊
* 程式設計人員在其網站或應用程式上實作此功能（例如，隱藏超過使用者評分上限的視訊）

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

### 附註 {#notes-mvpd-progr-metadata-exch-flow}

**資源標準化和驗證。** 資源ID可以以純字串或MRSS字串的形式傳遞。 程式設計師可以決定使用純字串格式或MRSS，但需要先與MVPD達成協定，以便MVPD知道如何處理該資源。

**資源ID和元資料規範。** Adobe Primetime驗證使用具有Media RSS擴充功能的RSS標準來指定資源及其中繼資料。 Adobe Primetime驗證可與Media RSS擴充功能搭配使用，支援多種中繼資料，例如家長控制(透過 `<media:rating>`)或地理位置(`<media:location>`)。

Adobe Primetime驗證也可支援針對需要RSS的MVPD，從舊版通道字串透明轉換至對應的RSS資源。 另一方面，針對僅限頻道的MVPD,Adobe Primetime驗證支援從RSS+MRSS轉換為純頻道標題。

**Adobe Primetime驗證可確保與現有整合的完全回溯相容。** 也就是說，對於使用通道層級驗證的程式設計人員，Adobe Primetime驗證會在將通道ID傳送至了解該格式的MVPD之前，先注意將其封裝為必要的格式。 反過來，情況也同樣如此：如果程式設計師以新格式指定其所有資源，則如果僅對通道級別授權的MVPD進行授權，Adobe Primetime驗證會將新格式轉換為簡單通道字串。

## 使用者中繼資料使用案例 {#user-metadata-use-cases}

隨著越來越多的MVPD做出法律安排並新增功能，使用案例會不斷改變和擴展。 以下是可用於哪些使用者中繼資料的範例。

* [MVPD使用者ID](#mvpd-user-id)
* [家庭ID](#household-user-id)
* [郵遞區號](#zip-code)
* [最高評分（家長控制）](#max-rating-parental-control)
* [頻道陣列](#channel-line-up)

### MVPD使用者ID {#mvpd-user-id}

* 如MVPD所提供
* 不是使用者的實際登入資訊，因為這是由MVPD雜湊而成
* 可用於指出特定使用者或的問題
* 加密
* MVPD支援：所有MVPD

### 家庭用戶ID {#household-user-id}

* 允許良好的量度資訊
* 加密
* MVPD支援：某些MVPD

### 郵遞區號 {#zip-code}

* 使用者的帳單郵遞區號
* 主要用於強制執行體育賽事凍結期間規則
* 可隨AuthZ回應提供，以進行快速更新
* MVPD支援：某些MVPD

### 最高評分（家長控制） {#max-rating-parental-control}

* AuthN最初為，加上AuthZ重新整理
* 從UI中篩選內容
* MPAA或VChip評等
* MVPD支援：某些MVPD

### 頻道陣列 {#channel-line-up}

* MVPD可提供使用者有權檢視的頻道清單
* 允許快速繪製UI
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
