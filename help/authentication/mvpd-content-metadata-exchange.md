---
title: MVPD內容中繼資料交換
description: MVPD內容中繼資料交換
exl-id: d17e60dc-6c61-4ca2-bad8-1840c95261e0
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# MVPD內容中繼資料交換

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 概觀 {#content-metadat-exchange-overview}

本頁說明Adobe Primetime驗證用來在授權要求上傳送結構化資料至MVPD的兩個標準實作。  結構化資料代表提出請求的資源（程式設計師），可能還包括其他資料，例如內容評等。

在程式設計師方面，Adobe Primetime驗證支援結構化的MRSS資料資源，如下所示：

1. 程式設計師以MRSS字串形式傳送資源。 Adobe Primetime驗證不會在網頁或原生裝置的使用者端進行編碼。 MRSS會以一般字串的形式傳送至Adobe Primetime驗證伺服器。
1. 在伺服器端，MRSS會根據預先定義的結構描述進行驗證(http://search.yahoo.com/mrss/)。  如果驗證通過，Adobe Primetime驗證會從MRSS欄位中擷取資訊，包括：
   * 頻道標題
   * 專案標題
   * 資源識別碼
   * 評等值和型別
1. 從MRSS擷取的值用於建立傳遞給MVPD的授權請求。

Adobe Primetime驗證支援兩種將MRSS轉譯為MVPD所支援格式的方法：

* **XACML**.  第一種方式符合OLCA標準。  它使用XACML，其中擷取MRSS值，以建立具有對應到MRSS元素的屬性的XACMLResource。  然後傳遞至MVPD。
* **REST**.  第二種方法是以REST為基礎。  MRSS會進行base64編碼，並以URL引數的形式傳遞至REST呼叫。

在這兩種方法中，MVPD都會將擷取的值納入其本身的邏輯流程中，並傳回授權回應，以處理授權要求。

## 整合詳細資訊 {#integration-details}

* OLCA型XACML結構化資源
* REST型結構化資源

### OLCA型XACML結構化資源 {#olca-based-xacml-struc-resource}

大多數以纜線導向的MVPD都使用XACML型方法，但尚未支援完整的結構化資料方法。  其他支援XACML的MVPD會取得管道標題，並接受該標題作為ResourceID屬性。 以下範例顯示完整的結構化XACML型方法。 Adobe Primetime驗證團隊建議，對於使用XACML，但尚未支援家長監護等功能MVPD，他們應該根據以下範例調整其XACML整合：

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

### REST型結構化資源 {#rest-based-struct-resource}

有些MVPD已標準化下列REST型授權通訊協定。 此方法與XACML方法一樣功能齊全，但提供「較輕重量」實施。

`// The MRSS is base64 encoded by Adobe Primetime authentication, and passed in that format to the REST-based Authorization endpoint.`

`https://auth.somedomain.net/mediation/1/rest/client/authz?uuID=AC82CE4&mrss=base64encodedstring&IPAddress=123.456.78.901`

<!--
>[!RELATEDINFORMATION]
>* [User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Logout](/help/authentication/usecase-mvpd-logout.md)
>* [Programmer Integration Guide: Identifying Protected Resources](/help/authentication/identify-protected-resources.md)
>* [Programmer Integration Guide: User Metadata Exchange](/help/authentication/user-metadata.md)
-->
