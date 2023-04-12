---
title: MVPD內容中繼資料交換
description: MVPD內容中繼資料交換
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# MVPD內容中繼資料交換

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 概述 {#content-metadat-exchange-overview}

本頁說明Adobe Primetime驗證用來在授權請求上傳送結構化資料至MVPD的兩種標準實作。  結構化資料表示提出請求的資源（程式設計師），並可能表示諸如內容分級之類的附加資料。

在程式設計人員端，Adobe Primetime驗證支援結構化MRSS資料資源，如下所示：

1. 程式設計師將資源作為MRSS字串發送。 Adobe Primetime驗證不會在用戶端為web或原生裝置編碼。 MRSS會以一般字串的形式傳送至Adobe Primetime驗證伺服器。
1. 在伺服器端，會根據預先定義的結構(http://search.yahoo.com/mrss/)來驗證MRSS。  如果驗證通過，Adobe Primetime驗證會從MRSS欄位擷取資訊，包括：
   * 頻道標題
   * 項目標題
   * 資源標識符
   * 評等值與類型
1. 從MRSS擷取的值會用來建置傳遞至MVPD的授權請求。

Adobe Primetime驗證支援兩種將MRSS轉譯為MVPD支援格式的方法：

* **XACML**.  第一種方法符合OLCA標準。  它使用XACML，在XACML中提取MRSS值，以構建具有映射到MRSS元素的屬性的XACMLResource。  接著會傳遞至MVPD。
* **REST**.  第二種方法是基於REST。  MRSS是base64編碼，並在REST呼叫中以URL參數傳遞。

在這兩種方法中，MVPD通過將提取的值包括在其自身邏輯流中並返回授權響應來處理授權請求。

## 整合詳細資訊 {#integration-details}

* 基於OLCA的XACML結構資源
* 基於REST的結構化資源

### 基於OLCA的XACML結構資源 {#olca-based-xacml-struc-resource}

大部分的有線MVPD都使用基於XACML的方法，但尚未支援完整的結構化資料方法。  其他支援XACML的MVPD會取用管道標題，並接受該標題作為ResourceID屬性。 以下範例說明完全結構化的XACML型方法。 Adobe Primetime驗證團隊建議，針對使用XACML但尚未支援父母控制等功能的MVPD，他們應根據下列範例調整其XACML整合：

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

有些MVPD已根據下列基於REST的授權協定進行標準化。 此方法與XACML方法一樣具有完整功能，但可提供「較輕的重量」實施。

`// The MRSS is base64 encoded by Adobe Primetime authentication, and passed in that format to the REST-based Authorization endpoint.`

`https://auth.somedomain.net/mediation/1/rest/client/authz?uuID=AC82CE4&mrss=base64encodedstring&IPAddress=123.456.78.901`

<!--
>[!RELATEDINFORMATION]
>* [User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Logout](/help/authentication/usecase-mvpd-logout.md)
>* [Programmer Integration Guide: Identifying Protected Resources](/help/authentication/identify-protected-resources.md)
>* [Programmer Integration Guide: User Metadata Exchange](/help/authentication/user-metadata.md)
-->