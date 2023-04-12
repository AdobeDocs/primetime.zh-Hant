---
title: 代理MVPD Web服務
description: 代理MVPD Web服務
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---


# 代理MVPD Web服務 {#proxy-mvpd-wbservice}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 概述 {#overview-proxy-mvpd-webserv}

「Proxy MVPD」是MVPD，除了管理本身與Adobe Primetime驗證的整合外，也代表一組相關聯的「代理MVPD」管理權限程式。 此安排對程式設計人員是透明的。

若要實作ProxyMVPD功能，Adobe Primetime驗證會提供RESTful Web服務，ProxyMVPD可透過此服務提交及擷取ProxidMVPD的清單。 此公用API使用的通訊協定為REST HTTP，假設如下：

* Proxy MVPD使用HTTPGET方法來擷取目前整合的MVPD清單。
* 代理MVPD使用HTTPPOST方法來更新支援的MVPD清單。

## 代理MVPD服務 {#proxy-mvpd-services}

* [擷取代理的MVPD](#retriev-proxied-mvpds)
* [提交代理的MVPD](#submit-proxied-mvpds)

### 擷取代理的MVPD {#retriev-proxied-mvpds}

檢索由apikey參數標識的ProxyMVPD的當前代理MVPD清單。

| 端點 | 呼叫者 | 請求標題 | HTTP方法 | HTTP回應 |
|---|---|---|---|---|
| &lt;fqdn>/control/v1/proxidedMvpds | ProxyMVPD | apikey（強制） | GET | <ul><li> 200（確定） — 已成功處理請求，且回應包含XML格式的ProxidedMVPD清單</li><li>401（未授權） — 提供的憑據需要用戶身份驗證或未授予授權。  指出下列其中一項：<ul><li>apikey Token不存在於請求標題中</li><li>請求源自未出現在允許清單中的IP位址</li><li>令牌無效</li></ul></li><li>403（禁止） — 表示提供的參數不支援操作，或者代理MVPD未設定為代理或缺少代理</li><li>405（不允許的方法） — 使用GET或POST以外的HTTP方法。 一般不支援HTTP方法，或此特定端點不支援。</li><li>500（內部伺服器錯誤） — 請求程式期間，伺服器端發生錯誤。</li></ul> |

curl範例：

`curl -X GET -H "apikey: ???provided-by-adobe???" "https://mgmt-prequal.auth-staging.adobe.com/control/v1/proxiedMvpds"`


XML響應示例：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<proxiedMvpds>
    <proxiedMvpd>
        <id>oneMvpdId</id>
        <displayName>MVPD Name</displayName>
        <logoURL></logoURL>
    </proxiedMvpd>
    <proxiedMvpd>
        <id ProviderID="ProviderID_Value_Sent_On_IdPEntry">mvpdPickerId</id>
        <displayName>MVPD Name Two</displayName>
        <logoURL></logoURL>
        <requestorIds>
            <requestorId>TheRequestorId_IntegratedWith</requestorId>
        </requestorIds>
    </proxiedMvpd>
    <proxiedMvpd>
        <id>anotherMvpdId</id>
        <displayName>Another MVPD</displayName>
        <logoURL></logoURL>
        <iframeSize>
            <iframeHeight>400</iframeHeight>
            <iframeWidth>340</iframeWidth>
        </iframeSize>
        <requestorIds>
            <requestorId>FirstIntegratedRequestorId</requestorId>
            <requestorId>SecondIntegratedRequestorId</requestorId>
        </requestorIds>
    </proxiedMvpd>
</proxiedMvpds>
```

### 提交代理的MVPD {#submit-proxied-mvpds}

推送與apikey參數所識別之Proxy MVPD整合的MVPD陣列。

| 端點 | 呼叫者 | 請求標題 | HTTP方法 | HTTP回應 |
|:------------------------------:|:---------:|:--------------------------------------------:|:-----------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| &lt;fqdn>/control/v1/proxidedMvpds | ProxyMVPD | apikey（強制）proxid-mvpds（強制） | POST | <ul><li>201（已建立） — 已成功處理推送</li><li>400（錯誤請求） — 伺服器不知道如何處理請求：<ul><li>傳入的XML不遵守此規範中發佈的架構</li><li>代理的mvpd沒有唯一ID</li><li>400回應代碼的推送請求者ID不存在其他Servlet容器原因</li></ul><li>401（未授權） — apikey無效或呼叫者IP不在允許清單上</li><li>403（禁止） — 表示提供的參數不支援操作，或者代理MVPD未設定為代理或缺少代理</li><li>405（不允許的方法） — 使用GET或POST以外的HTTP方法。 一般不支援HTTP方法，或此特定端點不支援。</li><li>500（內部伺服器錯誤） — 請求程式期間，伺服器端發生錯誤。</li></ul> |

curl範例：

`curl -X POST -H "apikey: <API_KEY>" "https://mgmt-prequal.auth.adobe.com/control/v1/proxiedMvpds" -d "proxied-mvpds=%3CproxiedMvpds%3E%3CproxiedMvpd%3E%3CdisplayName%3EFirst%20MVPD%20Name%3C%2FdisplayName%3E%3Cid%3EfirstMVPDId%3C%2Fid%3E%3ClogoURL%3E%3C%2FlogoURL%3E%3C%2FproxiedMvpd%3E%3CproxiedMvpd%3E%3Cid%20ProviderID%3D%22ProviderID_Value_Sent_On_IdPEntry%22%3EmvpdPickerId%3C%2Fid%3E%3CdisplayName%3EMVPD%20Name%20Two%3C%2FdisplayName%3E%3ClogoURL%3E%3C%2FlogoURL%3E%3CrequestorIds%3E%3CrequestorId%3ETHE_REQUESTOR_ID%3C%2FrequestorId%3E%3C%2FrequestorIds%3E%3C%2FproxiedMvpd%3E%3C%2FproxiedMvpds%3E"`



XML示例：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<proxiedMvpds>
    <proxiedMvpd>
        <id>oneMvpdId</id>
        <displayName>MVPD Name</displayName>
        <logoURL></logoURL>
    </proxiedMvpd>
    <proxiedMvpd>
        <id ProviderID="ProviderID_Value_Sent_On_IdPEntry">mvpdPickerId</id>
        <displayName>MVPD Name Two</displayName>
        <logoURL></logoURL>
        <requestorIds>
            <requestorId>TheRequestorId_IntegratedWith</requestorId>
        </requestorIds>
    </proxiedMvpd>
    <proxiedMvpd>
        <id>anotherMvpdId</id>
        <displayName>Another MVPD</displayName>
        <logoURL></logoURL>
        <iframeSize>
            <iframeHeight>400</iframeHeight>
            <iframeWidth>340</iframeWidth>
        </iframeSize>
        <requestorIds>
            <requestorId>FirstIntegratedRequestorId</requestorId>
            <requestorId>SecondIntegratedRequestorId</requestorId>
        </requestorIds>
    </proxiedMvpd>
</proxiedMvpds>
```


### 過帳頻率 {#posting-frequency}

Adobe Primetime驗證建議ProxyMVPDs只應在與先前的推播有所變更時，才推送其ProxiedMVPD清單。

### 刪除代理的MVPD {#delete-proxied-freqency}

如果ProxyMVPD推送含有空白ProxiedMVPD清單的XML記錄，該空白清單會像任何清單一樣儲存在我們的系統中，因此可以有效刪除先前的清單。



## XSD格式 {#xsd-format}

Adobe已定義下列接受的格式，可將代理的MVPD從公共網站服務張貼/擷取至公共網站服務：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
           xmlns:pxm="http://tve.adobe.com/data/proxiedmvpd"
           targetNamespace="http://tve.adobe.com/data/proxiedmvpd"
           elementFormDefault="qualified"
           version="1.0">
    <xs:complexType name="iframeSize">
        <xs:all>
            <xs:element name="iframeHeight" type="xs:int" minOccurs="1" maxOccurs="1" nillable="false"/>
            <xs:element name="iframeWidth" type="xs:int" minOccurs="1" maxOccurs="1" nillable="false"/>
        </xs:all>
    </xs:complexType>
    <xs:complexType name="requestorIds">
        <xs:annotation>
            <xs:documentation>List of requestors/programmers integrated with the proxied MVPD</xs:documentation>
        </xs:annotation>
        <xs:sequence>
            <xs:element name="requestorId" type="xs:string" minOccurs="1" maxOccurs="unbounded" nillable="false">
                <xs:annotation>
                    <xs:documentation>The requestor/programmer identifier recognized by Adobe</xs:documentation>
                </xs:annotation>
            </xs:element>
        </xs:sequence>
    </xs:complexType>
    <xs:complexType name="proxiedMvpd">
        <xs:all>
            <xs:element name="id" minOccurs="1" maxOccurs="1" nillable="false">
                <xs:annotation>
                    <xs:documentation>The id must conform to the regular expression: ([a-zA-Z0-9]+((\-)|[_])*)</xs:documentation>
                </xs:annotation>
                <xs:complexType>
                    <xs:simpleContent>
                        <xs:extension base="xs:string">
                            <xs:attribute name="ProviderID">
                                <xs:simpleType>
                                    <xs:restriction base="xs:string">
                                        <xs:minLength value="1"/>
                                        <xs:maxLength value="128"/>
                                    </xs:restriction>
                                </xs:simpleType>
                            </xs:attribute>
                        </xs:extension>
                    </xs:simpleContent>
                </xs:complexType>
            </xs:element>
            <xs:element name="displayName" type="xs:string" minOccurs="1" maxOccurs="1" nillable="false"/>
            <xs:element name="logoURL" type="xs:anyURI" minOccurs="1" maxOccurs="1" nillable="false"/>
            <xs:element name="iframeSize" type="pxm:iframeSize" minOccurs="0" maxOccurs="1"/>
            <xs:element name="requestorIds" type="pxm:requestorIds" minOccurs="0" maxOccurs="1"/>
        </xs:all>
    </xs:complexType>
    <xs:element name="proxiedMvpds">
        <xs:annotation>
            <xs:documentation>List of Proxied MVPD</xs:documentation>
        </xs:annotation>
        <xs:complexType>
            <xs:sequence>
                <xs:element name="proxiedMvpd" type="pxm:proxiedMvpd" minOccurs="0" maxOccurs="unbounded"/>
            </xs:sequence>
        </xs:complexType>
    </xs:element>
</xs:schema>
```

**元素附註：**

* `id` （必要） — 代理的MVPD ID必須是與MVPD名稱相關的字串，使用下列任一字元（因為為了追蹤目的，程式設計師將會看到它）:
   * 任何英數字元、底線(「_」)和連字型大小(「 — 」)。
   * idID必須符合下列規則運算式：
      `(a-zA-Z0-9((-)|_)*)`

      因此，它必須至少包含一個字元，以字母開頭，並以任何字母、數字、破折號或底線繼續。

* `iframeSize` （選用） — iframeSize元素為選用元素，並定義如果MVPD驗證頁面應位於iFrame中，iFrame的大小。 否則，如果iframeSize元素不存在，驗證將會在完整的瀏覽器重新導向頁面中發生。
* `requestorIds` （選用） — requestorIds值將由Adobe提供。 要求是，代理的MVPD應與至少一個requestorId整合。 如果代理的MVPD元素上沒有「requestorIds」標籤，則代理的MVPD將與整合在Proxy MVPD下的所有可用要求整合。
* `ProviderID` （選用） — 當id元素上存在ProviderID屬性時，在SAML驗證請求中，會將ProviderID的值以代理的MVPD/SubMVPD ID的形式（而非id值）傳送至Proxy MVPD。 在這種情況下，ID的值將僅用於程式設計人員頁面上顯示的MVPD選擇器，以及由Adobe Primetime驗證在內部使用。 ProviderID屬性的長度必須介於1到128個字元之間。

## 安全性 {#security}

若要將要求視為有效，必須遵守下列規則：

* 請求標題必須包含安全apikey參數。 （此應用程式金鑰將唯一識別Proxy MVPD的呼叫）。
* 請求必須來自允許的特定IP位址。
* 要求必須透過SSL通訊協定傳送。

Adobe會提供Token的（靜態）值。 此值用於驗證和授權程式中。  請求標題中出現且前述以外未列出的任何參數都會遭到忽略。

curl範例：

`curl -X GET -H "apikey: ???provided-by-adobe???" "https://mgmt-prequal.auth-staging.adobe.com/control/v1/proxiedMvpds"`

## Adobe Primetime驗證環境的代理MVPD Web服務端點 {#proxy-mvpd-wevserv-endpoints}

* **生產URL:** https://mgmt.auth.adobe.com/control/v1/proxiedMvpds
* **中繼URL:** https://mgmt.auth-staging.adobe.com/control/v1/proxiedMvpds
* **生產前URL:** https://mgmt-prequal.auth.adobe.com/control/v1/proxiedMvpds
* **測試前URL:** https://mgmt-prequal.auth-staging.adobe.com/control/v1/proxiedMvpds

<!--
>[!RELATEDINFORMATION]
>* [Proxy MVPD SAML integration](/help/authentication/proxy-mvpd-saml-int.md)
>* [User metadata exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Technical paper](/help/authentication/technical-paper.md)
>* [Adobe Primetime Authentication glossary](/help/authentication/glossary.md)
-->
