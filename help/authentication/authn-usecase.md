---
title: MVPD驗證
description: MVPD驗證
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1908'
ht-degree: 0%

---


# MVPD驗證 {#mvpd-authn}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 概述 {#mvpd-authn-overview}

實際的服務提供程式(SP)角色由程式設計師擔任，但Adobe Primetime身份驗證是該程式設計師的SP代理。 將Adobe Primetime驗證作為中介，可讓MVPD和程式設計人員避免根據個案自訂其權限程式。

當程式設計人員向支援SAML的MVPD要求驗證時，下列步驟會使用Adobe Primetime驗證呈現事件的順序。 請注意，Adobe Primetime身份驗證Access Enabler元件在用戶/訂閱者的客戶端上處於活動狀態。 從那裡，Access Enabler便於驗證流程的所有步驟。

1. 當用戶請求訪問受保護的內容時，Access Enabler代表程式設計師(SP)啟動身份驗證(AuthN)。
1. SP的應用程式會向使用者顯示「MVPD選取器」，以取得其付費電視提供者(MVPD)。 然後，SP會將使用者的瀏覽器重新導向至所選MVPD的身分提供者(IdP)服務。  這是「**程式設計師啟動的登錄**」。  MVPD會將IdP的回應傳送至Adobe的SAML斷言使用者服務，並於此處處理。
1. 最後，Access Enabler將瀏覽器重新定向回SP站點，向SP通知AuthN請求的狀態（成功/失敗）。

## 驗證要求 {#authn-req}

如上述步驟所示，在AuthN流程期間，MVPD必須同時接受以SAML為基礎的AuthN請求並傳送SAML AuthN回應。

此 [線上內容訪問(OLCA)驗證和授權介面規範](https://www.cablelabs.com/specifications/search?query=&amp;category=&amp;subcat=&amp;doctype=&amp;content=false&amp;archives=false){target=_blanck} 提供標準AuthN請求和回應。 雖然Adobe Primetime驗證不要求MVPD以此標準為基礎的權限訊息，但查看規格可提供AuthN交易所需之關鍵屬性的深入分析。

>[!NOTE]
>
>MVPD透過Adobe Primetime驗證接收的AuthN請求確實包含數位簽名。 不過，出於簡潔的原因，以下範例不顯示簽名。 如需顯示數位簽名的範例，請參閱 [驗證響應](#authn-response) 在以下章節中。

範例SAML驗證請求：

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

下表說明驗證請求中需要包含的屬性和標籤，以及預設的預期值。

**SAML驗證請求詳細資訊**

| samlp:AuthnRequest | &lt;authnrequest> 由服務提供者向身份提供者發出。 |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AssertionConsumerServiceURL | 這是後續回應中要使用的Adobe端點。 預設值： **http://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer** |
| 目的地 | URI引用，指示已向其發送此請求的地址。 這對於防止將請求惡意轉發給非預期的收件人非常有用，這是某些協定綁定所需的保護。 如果存在，則實際收件人必須檢查URI引用是否標識接收消息的位置。 若未這麼做，則必須捨棄要求。 某些協定綁定可能需要使用此屬性。 |
| ForceAuthn | 如果ForceAuthn屬性的值為true，則強制標識提供者新建立此標識，而不依賴於與主體可能存在的現有會話。 |
| ID | 請求的識別碼。 請參閱 [SAML核心2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} 1.3.4節，以了解詳情。 |
| IsPassive | 布林值。 如果為「true」，則身份提供者和用戶代理本身「不能」以明顯的方式從請求者處控制用戶介面，並以明顯的方式與演示者交互。 若未提供值，預設值為「false」。 |
| IssueInstant | 響應的問題的時刻。 時間值以UTC編碼，如 [SAML核心2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} 第1.3.3節。 |
| 協定綁定 | URI參考，用於識別傳回 &lt;response> 訊息。 請參閱 [SAMLBind] 有關為它們定義的協定綁定和URI引用的詳細資訊。 預設值：回歸:oasis:名稱:tc:SAML:2.0:bindings:HTTP-POST |
| 版本 | 此請求的版本。 |
| saml:Issuer | 標識生成響應消息的實體。 （如需此元素的詳細資訊，請參閱SAML核心2.0-os Section 2.2.5） |
| ds：簽名 | XML簽名，可保護聲明的完整性並驗證聲明的頒發者，如SAML core 2.0-os中第5節所述 |
| samlp:NameIDPolicy | 指定用於表示所請求主題的名稱標識符的約束。 |
| 允許建立 | 一個布爾值，用於指示在完成請求過程中是否允許標識提供程式建立表示承擔者的新標識符。 預設值：true |
| 格式 | 指定與名稱標識符格式對應的URI引用預設：回歸:oasis:名稱:tc:SAML:2.0:nameid-format:暫時Adobe建議：回歸:oasis:名稱:tc:SAML:2.0:nameid-format:永久性 |
| SPNameQualifier | 可選地指定在除請求者之外的服務提供商的命名空間中返回（或建立）斷言主體的標識符。 預設值：http://saml.sp.adobe.adobe.com |

## 驗證回應 {#authn-response}

MVPD收到並處理了驗證要求後，現在必須傳送驗證回應。

**SAML驗證回應範例**

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


在上述範例中，AdobeSP預期會從Subject/NameId中擷取使用者ID。 AdobeSP可配置為從自定義屬性中獲取用戶ID;回應應包含下列元素：

```XML
<saml:AttributeStatement>
     <saml:Attribute Name="guid" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
         <saml:AttributeValue xsi:type="xs:string">
               71C69B91-F327-F185-F29E-2CE20DC560F5
         </saml:AttributeValue>
    </saml:Attribute>
</saml:AttributeStatement>
```

**SAML驗證回應詳細資訊**
| samlp：響應 |Adobe Primetime驗證收到的回應。                                                                                                                                                                                                                                                                                                                                                                                                                       | |—|—| |目標 | URI引用，指明此請求已發送到的地址。 這對於防止將請求惡意轉發給非預期的收件人非常有用，這是某些協定綁定所需的保護。 如果存在，則實際收件人必須檢查URI引用是否標識接收消息的位置。 若未這麼做，則必須捨棄要求。 某些協定綁定可能需要使用此屬性。 | | ID |請求的識別碼。 其類型為xs:ID，且必須符合1.3.4節中指定的要求 [SAML核心2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} 識別碼唯一性。 請求中的ID屬性值與對應回應中的InResponseTo屬性值必須相符。                                                                                                                                                                                         | | InResponseTo | SAML通訊協定訊息的ID，以回應測試實體可呈現斷言。 值必須等於驗證請求中傳送之ID屬性中的值。 請參閱SAML核心2.0-os | |問題即時 |請求發出的立即時間。                                                                                                                                                                                                                                                                                                                                                                                                                                  | |版本 |請求的版本。                                                                                                                                                                                                                                                                                                                                                                                                                                                | | saml：頒發者 |識別產生請求訊息的實體。 （如需此元素的詳細資訊，請參閱2.2.5節。 SAML核心2.0-os） | | samlp：狀態 |代表對應要求狀態的程式碼。                                                                                                                                                                                                                                                                                                                                                                                                               | | samlp:StatusCode |代表回應對應要求而執行之活動的狀態的代碼。                                                                                                                                                                                                                                                                                                                                                                       | | saml：斷言 |此類型指定所有斷言通用的基本資訊。                                                                                                                                                                                                                                                                                                                                                                                                        | | ID |此斷言的標識符。                                                                                                                                                                                                                                                                                                                                                                                                                                         | |版本 |此斷言的版本。                                                                                                                                                                                                                                                                                                                                                                                                                                             | |問題即時 |請求發出的立即時間。                                                                                                                                                                                                                                                                                                                                                                                                                                  | | ds：簽名 | XML簽名，可保護聲明的完整性並驗證聲明的頒發者，如SAML core 2.0-os中第5節所述 | | ds:SignedInfo | SignedInfo的結構包括規範化算法、簽名算法和一個或多個引用。 SignedInfo元素可能包含可選的ID屬性，允許其他簽名和對象引用該屬性。 請參閱XML簽名語法和處理 | | ds:CanonicalizationMethod |規範化方法是必需的元素，它指定在執行簽名計算之前應用於SignedInfo元素的規範化算法。 請參閱XML簽名語法和處理 | | ds:SignatureMethod | SignatureMethod是指定用於簽名生成和驗證的算法的必需元素。 此演算法可識別簽名操作中涉及的所有加密函式（例如散列、公鑰算法、MAC、填充等） 請參閱XML簽名語法和處理 | | ds：引用 |參考是可能發生一或多次的元素。 它指定摘要算法和摘要值，以及可選地指定要簽名的對象的標識符、對象的類型和/或要在消化之前應用的轉換清單。 請參閱XML簽名語法和處理 | | ds：轉換 |選用的轉換元素包含有序的轉換元素清單；這些說明了簽名者如何獲得被消解的資料對象。 每個轉換的輸出作為下一個轉換的輸入。 第一個轉換的輸入是取消引用引用元素的URI屬性的結果。 最後一個轉換的輸出是DigestMethod算法的輸入。 請參閱XML簽名語法和處理 | | ds:DigestMethod | DigestMethod是標識要應用於簽名對象的摘要算法的必需元素。 請參閱XML簽名語法和處理 | | ds:DigestValue | DigestValue是包含摘要編碼值的元素。 摘要一律使用base64編碼。 請參閱XML簽名語法和處理 | | ds:SignatureValue | SignatureValue元素包含數字簽名的實際值；一律使用base64編碼。 請參閱XML簽名語法和處理 | | ds:KeyInfo | KeyInfo是選用元素，可讓收件者取得驗證簽名所需的金鑰。 請參閱XML簽名語法和處理 | | ds:X509Data | KeyInfo中的X509Data元素包含一或多個金鑰或X509憑證的識別碼。 請參閱XML簽名語法和處理 | | ds:X509C證書 | X509Certificate元素，包含base64編碼 [X509v3] 憑證 | | saml：主體 |聲明中的語句主題。                                                                                                                                                                                                                                                                                                                                                                                                                          | | saml:NameID | &lt;nameid> 元素的類型為NameIDType（請參閱SAML核心2.0-os中的2.2.2節），且用於各種SAML斷言結構，例如 &lt;subject> 和 &lt;subjectconfirmation> 元素，以及各種通訊協定訊息中。                                                                                                                                                                                                                                           | |格式 |表示字串型標識符資訊分類的URI引用。                                                                                                                                                                                                                                                                                                                                                                                    | | SPNameQualifier |進一步使用服務提供商的名稱或提供商的關聯來限定名稱。 此屬性提供了根據信賴方或交易方聯合名稱的附加方法。                                                                                                                                                                                                                                                                      | | saml:SubjectConfirmation |允許確認主題的資訊。 如果提供了多個主題確認，則滿足其中任何一個主題就足以確認主題以應用該斷言。                                                                                                                                                                                                                                                    | | saml:SubjectConfirmationData |要由特定確認方法使用的其他確認資訊。 例如，此元素的典型內容可能是 <!--<ds:KeyInfo>--> 在XML簽名語法和處理規範中定義的元素 | | NotOnOrAfter |無法再確認主題的一刻。                                                                                                                                                                                                                                                                                                                                                                                                            | |收件者 |一個URI，它指定測試實體可向其呈現斷言的實體或位置。 例如，此屬性可能表示必須將聲明傳遞到特定網路端點，以防止中介將其重定向到其他位置。                                                                                                                                                                                   | | saml：條件 | &lt;condition> 元素是新條件的擴充點。                                                                                                                                                                                                                                                                                                                                                                                                   | | NotBefore | NotBefore屬性指定有效間隔開始的時間瞬間。                                                                                                                                                                                                                                                                                                                                                                                  | | saml:AudienceRestriction | &lt;audiencerestriction> 元素會指定將斷言定址至由 &lt;audience> 元素。                                                                                                                                                                                                                                                                                                                           | | saml：對象 |標識目標對象的URI引用。                                                                                                                                                                                                                                                                                                                                                                                                                      | | saml:AuthnStatement |驗證語句。                                                                                                                                                                                                                                                                                                                                                                                                                                               | | AuthnInstant |指定驗證發生的時間。                                                                                                                                                                                                                                                                                                                                                                                                                 | |會話索引 |指定主體所標識的主體與驗證機構之間特定會話的索引。                                                                                                                                                                                                                                                                                                                                              | | saml:AuthnContext |驗證機構使用的上下文，直至生成此語句的驗證事件（包括該驗證事件）。                                                                                                                                                                                                                                                                                                                                                 | | saml:AuthnContextClassRef |標識驗證上下文類的URI引用，該類描述了下面的驗證上下文聲明。 |