---
title: MVPD內容元資料交換
description: MVPD內容元資料交換
exl-id: d17e60dc-6c61-4ca2-bad8-1840c95261e0
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# MVPD內容元資料交換

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 概述 {#content-metadat-exchange-overview}

本頁介紹Adobe Primetime身份驗證在授權請求上將結構化資料發送到MVPD時使用的兩種標準實現。  所述結構化資料表示發出所述請求的資源（程式設計師），並且可能還表示諸如內容分級之類的附加資料。

在程式設計師方面，Adobe Primetime身份驗證支援結構化MRSS資料資源，如下所示：

1. 程式設計師將資源作為MRSS字串發送。 Adobe Primetime身份驗證不會在客戶端對web或本機設備進行編碼。 MRSS作為常規字串發送到Adobe Primetime驗證伺服器。
1. 在伺服器端，MRSS將根據預定義的模式(http://search.yahoo.com/mrss/)進行驗證。  如果驗證通過，Adobe Primetime驗證會從MRSS欄位中提取資訊，包括：
   * 頻道標題
   * 項目標題
   * 資源標識符
   * 評級值和類型
1. 從MRSS提取的值用於構建傳遞到MVPD的授權請求。

Adobe Primetime驗證支援兩種將MRSS轉換為MVPD支援的格式的方法：

* **XACML**。  第一種方法與OLCA標準一致。  它使用XACML，在XACML中提取MRSS值，用映射到MRSS元素的屬性構建XACMLResource。  然後將此項傳遞給MVPD。
* **休息**。  第二種方法是基於REST。  MRSS是base64編碼的，並作為REST調用的URL參數傳遞。

在這兩種方法中，MVPD通過將提取的值包括在其自身的邏輯流中並返回授權響應來處理授權請求。

## 整合詳細資訊 {#integration-details}

* 基於OLCA的XACML結構化資源
* 基於REST的結構化資源

### 基於OLCA的XACML結構化資源 {#olca-based-xacml-struc-resource}

大多數面向電纜的MVPD都使用基於XACML的方法，但尚未支援完整的結構化資料方法。  支援XACML的其他MVPD將獲取「通道標題」，並接受該「通道標題」作為ResourceID屬性。 以下示例顯示了基於XACML的完整結構化方法。 Adobe Primetime身份驗證團隊建議，對於使用XACML但尚不支援家長控制等功能的MVPD，他們應將其XACML整合調整為以下示例：

```XML
<?xml version="1.0" encoding="UTF-8"?>
<soap11:Envelope xmlns:soap11=">
    <soap11:Header/>
    <soap11:Body>
        <xacml-samlp:XACMLAuthzDecisionQuery
                xmlns:xacml-samlp="urn:oasis:names:tc:xacml:2.0:profile:saml2.0:v2:schema:protocol"
                Destination="
                ID="_f1dd34469c5aeac016760e51dbba007d" IssueInstant="2012-06-26T16:30:24.879Z" Version="2.0">
            <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
                https://saml.sp.auth.adobe.com/
            </saml:Issuer>
            <ds:Signature xmlns:ds=">.......</ds:Signature>
            <xacml-context:Request xmlns:xacml-context="urn:oasis:names:tc:xacml:2.0:context:schema:os">
                [....info skipped for brevity....]
                <xacml-context:Resource>
 
        // The MRSS item GUID is passed as the XACML Resource resource-id
                    <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id">
                        <xacml-context:AttributeValue>DISNEY_GUID_12345</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
        // The MRSS channel title is passed as the XACML Resource tv-network
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:tv-network">
                        <xacml-context:AttributeValue>Disney</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // Adobe doesn't yet support an explicit namespace for the GUID, so we reuse the channel title as the GUID.  
        // We expect to add an explicit namespace later next year pulling it from the GUID scheme attribute.
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:id:namespace">
                        <xacml-context:AttributeValue>Disney</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // The MRSS item title is passed as the XACML Resource content title
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:title">
                        <xacml-context:AttributeValue>Disney Program X</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // The MRSS media rating is passed as the XACML Resource content rating 
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:rating:vchip">
                        <xacml-context:AttributeValue>TV-Y</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
                </xacml-context:Resource>
 
                <xacml-context:Action>
                    <xacml-context:Attribute>
                        <xacml-context:AttributeValue>VIEW</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
                </xacml-context:Action>
 
                [.....info skipped for brevity....]
            </xacml-context:Request>
        </xacml-samlp:XACMLAuthzDecisionQuery>
    </soap11:Body>
</soap11:Envelope>
 
//formatted for readability
```

### 基於REST的結構化資源 {#rest-based-struct-resource}

一些MVPD已經對以下基於REST的授權協定進行了標準化。 此方法與XACML方法一樣全面，但提供了「輕量」實施。

`// The MRSS is base64 encoded by Adobe Primetime authentication, and passed in that format to the REST-based Authorization endpoint.`

`https://auth.somedomain.net/mediation/1/rest/client/authz?uuID=AC82CE4&mrss=base64encodedstring&IPAddress=123.456.78.901`

<!--
>[!RELATEDINFORMATION]
>* [User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Logout](/help/authentication/usecase-mvpd-logout.md)
>* [Programmer Integration Guide: Identifying Protected Resources](/help/authentication/identify-protected-resources.md)
>* [Programmer Integration Guide: User Metadata Exchange](/help/authentication/user-metadata.md)
-->
