---
title: MVPD身份驗證
description: MVPD身份驗證
exl-id: 9ff4a46e-a37b-414c-a163-9e586252a9c3
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1908'
ht-degree: 0%

---

# MVPD身份驗證 {#mvpd-authn}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 概述 {#mvpd-authn-overview}

實際的服務提供商(SP)角色由程式設計師擔任，但Adobe Primetime身份驗證是該程式設計師的SP代理。 使用Adobe Primetime身份驗證作為中介使MVPD和程式設計師都能夠避免逐個定製其權利流程。

下面的步驟顯示了當程式設計師從支援SAML的MVPD請求驗證時，使用Adobe Primetime驗證的事件序列。 請注意，Adobe Primetime驗證Access Enabler元件在用戶/訂戶的客戶端上處於活動狀態。 從那裡，Access Enabler便於驗證流的所有步驟。

1. 當用戶請求訪問受保護的內容時，Access Enabler會代表程式設計師(SP)啟動身份驗證(AuthN)。
1. SP的應用向用戶顯示「MVPD選取器」，以獲取其付費電視提供商(MVPD)。 然後，SP將用戶的瀏覽器重定向到所選MVPD的標識提供程式(IdP)服務。  這是「」**程式設計師啟動的登錄**。  MVPD將IdP的響應發送到Adobe的SAML斷言使用者服務，並在該服務中對其進行處理。
1. 最後，Access Enabler將瀏覽器重定向回SP站點，並通知SP AuthN請求的狀態（成功/失敗）。

## 驗證請求 {#authn-req}

如上述步驟所示，在AuthN流程期間，MVPD必須同時接受基於SAML的AuthN請求併發送SAML AuthN響應。

的 [線上內容訪問(OLCA)驗證和授權介面規範](https://www.cablelabs.com/specifications/search?query=&amp;category=&amp;subcat=&amp;doctype=&amp;content=false&amp;archives=false){target=_blanck} 顯示標準AuthN請求和響應。 雖然Adobe Primetime身份驗證不要求MVPD將其權利消息傳遞基於此標準，但查看規範可以深入瞭解AuthN事務所需的關鍵屬性。

>[!NOTE]
>
>MVPD通過Adobe Primetime身份驗證接收的AuthN請求確實包含數字簽名。 但是，以下示例由於簡單原因沒有顯示簽名。 有關顯示數字簽名的示例，請參見中的示例 [驗證響應](#authn-response) 中。

SAML驗證請求示例：

```XML
<?xml version="1.0" encoding="UTF-8"?>
<samlp:AuthnRequest  
    AssertionConsumerServiceURL=http://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer          
    Destination=http://idp.com/SSOService
    ForceAuthn="false"
    ID="_c0fc667e-ad12-44d6-9cae-bc7cf04688f8"
    IsPassive="false"
    IssueInstant="2010-08-03T14:14:54.372Z"
    ProtocolBinding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"
    Version="2.0"
    xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
        http://saml.sp.adobe.adobe.com
    </saml:Issuer>
    <ds:Signature xmlns:ds=_signature_block_goes_here_
    </ds:Signature>
    <samlp:NameIDPolicy
        AllowCreate="true"
        Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"
        SPNameQualifier="http://saml.sp.adobe.adobe.com"/>
</samlp:AuthnRequest> 
```

下表說明了驗證請求中需要包含的屬性和標籤，其值為預設預期值。

**SAML驗證請求詳細資訊**

| samlp:AuthnRequest | &lt;authnrequest> 由服務提供商頒發給身份提供商。 |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 斷言ConsumerServiceURL | 這是在後續響應中使用的Adobe終結點。 預設值： **http://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer** |
| 目標 | URI引用，指示此請求已發送到的地址。 這對於防止將請求惡意轉發到意外收件人非常有用，這是某些協定綁定所需的保護。 如果存在，則實際收件人必須檢查URI引用是否標識接收消息的位置。 否則，必須丟棄該請求。 某些協定綁定可能需要使用此屬性。 |
| 福克奧森 | ForceAuthn屬性（如果值為true），將強制標識提供程式重新建立此標識，而不依賴於它可能與主體存在的現有會話。 |
| ID | 請求的標識符。 請參閱 [SAML核心2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} 1.3.4部分。 |
| 被動 | 布爾值。 如果為&quot;true&quot;，則身份提供者和用戶代理本身不得明顯地從請求者手中控制用戶介面，並以明顯的方式與演示者進行交互。 如果未提供值，則預設值為「false」。 |
| 問題即時 | 響應問題的時間瞬間。 時間值以UTC格式編碼，如中所述 [SAML核心2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} 第1.3.3節。 |
| 協定綁定 | URI引用，它標識在返回SAML時要使用的SAML協定綁定 &lt;response> 。 請參閱 [三磅] 的子菜單。 預設值：甕:oasis:名稱:tc:SAML:2.0:bindings:HTTPPOST |
| 版本 | 此請求的版本。 |
| saml：頒發者 | 標識生成響應消息的實體。 (有關此元素的詳細資訊，請參閱SAML core 2.0-os Section 2.2.5) |
| ds：簽名 | XML簽名，它保護斷言的完整性並驗證斷言的頒發者，如SAML core 2.0-os中第5節所述 |
| samlp：名稱IDPolicy | 指定用於表示所請求主題的名稱標識符的約束。 |
| 允許建立 | 一個布爾值，用於指示在滿足請求過程中是否允許身份提供程式建立新標識符以表示承擔者。 預設值：真 |
| 格式 | 指定與名稱標識符格式對應的URI引用預設值：甕:oasis:名稱:tc:SAML:2.0:nameid-format:臨時Adobe建議：甕:oasis:名稱:tc:SAML:2.0:nameid-format:持久 |
| SPNameQualifier | 可選地指定在除請求者之外的服務提供商的命名空間中返回（或建立）斷言主題的標識符。 預設：http://saml.sp.adobe.adobe.com |

## 驗證響應 {#authn-response}

MVPD已接收並處理了身份驗證請求，現在必須發送身份驗證響應。

**示例SAML驗證響應**

```XML
<?xml version="1.0" encoding="UTF-8"?> 
<samlp:Response Destination="https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer"
                ID="_0ac3a9dd5dae0ce05de20912af6f4f83a00ce19587"                             
                InResponseTo="_c0fc667e-ad12-44d6-9cae-bc7cf04688f8"
                IssueInstant="2010-08-17T11:17:50Z" Version="2.0"              
                xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion"
                xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"
                xmlns:xs="http://www.w3.org/2001/XMLSchema"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
             http://idp.com/SSOService
    </saml:Issuer>
    <samlp:Status>
       <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
    </samlp:Status>
    <saml:Assertion ID="pfxb0662d76-17a2-a7bd-375f-c11046a86742"
                   IssueInstant="2010-08-17T11:17:50Z"
                   Version="2.0">
        <saml:Issuer>http://idp.com/SSOService</saml:Issuer>
        <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
          <ds:SignedInfo>
            <ds:CanonicalizationMethod
                     Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>
            <ds:SignatureMethod
                     Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>
            <ds:Reference URI="#pfxb0662d76-17a2-a7bd-375f-c11046a86742">
              <ds:Transforms>
                 <ds:Transform
                    Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>        
                 <ds:Transform
                            Algorithm=http://www.w3.org/2001/10/xml-exc-c14n#"/>
              </ds:Transforms>
              <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>
              <ds:DigestValue>LgaPI2ASx/fHsoq0rB15Zk+CRQ0=</ds:DigestValue>
            </ds:Reference>
          </ds:SignedInfo>
          <ds:SignatureValue>
                POw/mCKF__shortened_for_brevity__9xdktDu+iiQqmnTs/NIjV5dw==
          </ds:SignatureValue>
          <ds:KeyInfo>
            <ds:X509Data>
                <ds:X509Certificate>
                 MIIDVDCCAjygAwIBA__shortened_for_brevity_utQ==
                </ds:X509Certificate>
            </ds:X509Data>
          </ds:KeyInfo>
      </ds:Signature>
      <saml:Subject>
        <saml:NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"
                     SPNameQualifier="https://saml.sp.auth.adobe.com">
            _5afe9a437203354aa8480ce772acb703e6bbb8a3ad
        </saml:NameID>
        <saml:SubjectConfirmation
                     Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
            <saml:SubjectConfirmationData
                  InResponseTo="_c0fc667e-ad12-44d6-9cae-bc7cf04688f8"
                  NotOnOrAfter="2010-08-17T11:22:50Z"                                          
                  Recipient="https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer"/>
           </saml:SubjectConfirmation>
       </saml:Subject>
       <saml:Conditions NotBefore="2010-08-17T11:17:20Z"
                        NotOnOrAfter="2010-08-17T19:17:50Z">
           <saml:AudienceRestriction>
              <saml:Audience>https://saml.sp.auth.adobe.com</saml:Audience>
           </saml:AudienceRestriction>
       </saml:Conditions>
       <saml:AuthnStatement AuthnInstant="2010-08-17T11:17:50Z"
                   SessionIndex="_1adc7692e0fffbb1f9b944aeafce62aaa7d770cd9e">
        <saml:AuthnContext>
            <saml:AuthnContextClassRef>
                   urn:oasis:names:tc:SAML:2.0:ac:classes:Password
            </saml:AuthnContextClassRef>
        </saml:AuthnContext>
    </saml:AuthnStatement>
  </saml:Assertion>
</samlp:Response>
```


在上面的示例中，AdobeSP希望從Subject/NameId中提取用戶ID。 AdobeSP可以配置為從自定義屬性獲取用戶ID;響應應包含如下元素：

```XML
<saml:AttributeStatement>
     <saml:Attribute Name="guid" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
         <saml:AttributeValue xsi:type="xs:string">
               71C69B91-F327-F185-F29E-2CE20DC560F5
         </saml:AttributeValue>
    </saml:Attribute>
</saml:AttributeStatement>
```

**SAML驗證響應詳細資訊**
| samlp：響應 |由Adobe Primetime身份驗證接收的響應。                                                                                                                                                                                                                                                                                                                                                                                                                       | |—| |目標 | URI引用，指示此請求已發送到的地址。 這對於防止將請求惡意轉發到意外收件人非常有用，這是某些協定綁定所需的保護。 如果存在，則實際收件人必須檢查URI引用是否標識接收消息的位置。 否則，必須丟棄該請求。 某些協定綁定可能需要使用此屬性。 | | ID |請求的標識符。 它的類型為xs:ID和MUST，符合第1.3.4節中指定的要求 [SAML核心2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} 標識符唯一性。 請求中ID屬性的值與相應響應中的InResponseTo屬性的值匹配。                                                                                                                                                                                         | | InResponseTo | SAML協定消息的ID，驗證實體可以響應該消息來顯示斷言。 該值必須等於「驗證請求」中發送的ID屬性中的值。 請參見SAML核心2.0-os | |問題即時 |請求發出的時間即刻。                                                                                                                                                                                                                                                                                                                                                                                                                                  | |版本 |請求的版本。                                                                                                                                                                                                                                                                                                                                                                                                                                                | | saml：頒發者 |標識生成請求消息的實體。 (有關此元素的詳細資訊，請參見2.2.5節。SAML核心2.0-os) | | samlp：狀態 |代表相應請求狀態的代碼。                                                                                                                                                                                                                                                                                                                                                                                                               | | samlp:StatusCode |代表響應相應請求而執行的活動狀態的代碼。                                                                                                                                                                                                                                                                                                                                                                       | | saml：斷言 |此類型指定所有斷言通用的基本資訊。                                                                                                                                                                                                                                                                                                                                                                                                        | | ID |此斷言的標識符。                                                                                                                                                                                                                                                                                                                                                                                                                                         | |版本 |此斷言的版本。                                                                                                                                                                                                                                                                                                                                                                                                                                             | |問題即時 |請求發出的時間即刻。                                                                                                                                                                                                                                                                                                                                                                                                                                  | | ds：簽名 | XML簽名，它保護斷言的完整性並驗證斷言的頒發者，如SAML core 2.0-os中第5節所述 | | ds：簽名資訊 | SignedInfo的結構包括規範化算法、簽名算法和一個或多個引用。 SignedInfo元素可能包含可選的ID屬性，該屬性將允許其被其他簽名和對象引用。 請參閱XML-Signature語法和處理 | | ds:CanonicalizationMethod | CanonicalizationMethod是指定在執行簽名計算之前應用於SignedInfo元素的規範化算法的必需元素。 請參閱XML-Signature語法和處理 | | ds:SignatureMethod | SignatureMethod是指定用於生成和驗證簽名的算法的必需元素。 此算法標識簽名操作中涉及的所有加密函式（例如散列、公鑰算法、MAC、填充等） 請參閱XML-Signature語法和處理 | | ds：引用 |引用是可能發生一次或多次的元素。 它指定摘要算法和摘要值，以及可選地指定正在簽名的對象的標識符、對象的類型和/或在分解之前要應用的轉換的清單。 請參閱XML-Signature語法和處理 | | ds：轉換 |可選的轉換元素包含轉換元素的有序清單；這些描述了簽名者如何獲得被消化的資料對象。 每個轉換的輸出都用作下一個轉換的輸入。 第一個轉換的輸入是取消引用引用元素的URI屬性的結果。 最後一個Transform的輸出是DigestMethod算法的輸入。 請參閱XML-Signature語法和處理 | | ds:DigestMethod | DigestMethod是標識要應用於簽名對象的摘要算法的必需元素。 請參閱XML-Signature語法和處理 | | ds:DigestValue | DigestValue是包含摘要的編碼值的元素。 摘要始終使用base64進行編碼。 請參閱XML-Signature語法和處理 | | ds：簽名值 | SignatureValue元素包含數字簽名的實際值；它總是使用base64編碼。 請參閱XML-Signature語法和處理 | | ds:KeyInfo | KeyInfo是一個可選元素，它使收件人能夠獲得驗證簽名所需的密鑰。 請參閱XML-Signature語法和處理 | | ds:X509資料 | KeyInfo中的X509Data元素包含一個或多個密鑰或X509證書的標識符。 請參閱XML-Signature語法和處理 | | ds:X509證書 | X509Certificate元素，包含base64編碼 [X509v3] 證書 | | saml：主題 |斷言中語句的主題。                                                                                                                                                                                                                                                                                                                                                                                                                          | | saml:NameID | &lt;nameid> 元素的類型為NameIDType(請參見SAML core 2.0-os中的2.2.2節)，它用於各種SAML斷言結構，如 &lt;subject> 和 &lt;subjectconfirmation> 元素和各種協定消息中。                                                                                                                                                                                                                                           | |格式 |表示基於字串的標識符資訊分類的URI引用。                                                                                                                                                                                                                                                                                                                                                                                    | | SPNameQualifier |進一步使用服務提供商名稱或提供商的隸屬關係限定名稱。 此屬性提供了根據信賴方或當事方聯合名稱的附加方法。                                                                                                                                                                                                                                                                      | | saml:SubjectConfirmation |允許確認主題的資訊。 如果提供了多個主題確認，則滿足其中任何一個主題就足以確認主題以便應用斷言。                                                                                                                                                                                                                                                    | | saml:SubjectConfirmationData |特定確認方法使用的其他確認資訊。 例如，此元素的典型內容可能是 <!--<ds:KeyInfo>--> 在XML簽名語法和處理規範中定義的元素 | | NotOnOrAfter |無法再確認主題的時間。                                                                                                                                                                                                                                                                                                                                                                                                            | |收件人 |一個URI，它指定驗證實體可以向其顯示斷言的實體或位置。 例如，此屬性可能表示必須將斷言傳遞到特定網路端點，以防止中介將斷言重定向到其他端點。                                                                                                                                                                                   | | saml：條件 | &lt;condition> 元素用作新條件的擴展點。                                                                                                                                                                                                                                                                                                                                                                                                   | |之前 | NotBefore屬性指定有效間隔開始的時間瞬間。                                                                                                                                                                                                                                                                                                                                                                                  | | saml:AudienceRestriction | &lt;audiencerestriction> 元素指定將斷言定址到由 &lt;audience> 元素。                                                                                                                                                                                                                                                                                                                           | | saml：受眾 |標識目標受眾的URI引用。                                                                                                                                                                                                                                                                                                                                                                                                                      | | saml:AuthnStatement |驗證語句。                                                                                                                                                                                                                                                                                                                                                                                                                                               | | AuthnInstant |指定進行身份驗證的時間。                                                                                                                                                                                                                                                                                                                                                                                                                 | |會話索引 |指定由主體標識的主體與驗證機構之間的特定會話的索引。                                                                                                                                                                                                                                                                                                                                              | | saml:AuthnContext |驗證機構在生成此語句的驗證事件之前使用的上下文。                                                                                                                                                                                                                                                                                                                                                 | | saml:AuthnContextClassRef | URI引用，用於標識描述後面的驗證上下文聲明的驗證上下文類。 |
