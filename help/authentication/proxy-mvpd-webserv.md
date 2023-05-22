---
title: 代理MVPD Web服務
description: 代理MVPD Web服務
exl-id: f75cbc4d-4132-4ce8-a81c-1561a69d1d3a
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---

# 代理MVPD Web服務 {#proxy-mvpd-wbservice}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 概述 {#overview-proxy-mvpd-webserv}

「代理MVPD」是MVPD，除了管理與Adobe Primetime身份驗證的整合外，還代表一組關聯的「代理MVPD」管理權利進程。 此安排對程式設計師是透明的。

為實現ProxyMVPD功能，Adobe Primetime身份驗證提供REST風格的Web服務，ProxyMVPD可通過這些服務提交和檢索ProxiedMVPD的清單。 此公共API使用的協定是REST HTTP ，其中假設如下：

* 代理MVPD使用HTTPGET方法檢索當前整合MVPD的清單。
* 代理MVPD使用HTTPPOST方法更新受支援MVPD的清單。

## 代理MVPD服務 {#proxy-mvpd-services}

* [檢索代理的MVPD](#retriev-proxied-mvpds)
* [提交代理的MVPD](#submit-proxied-mvpds)

### 檢索代理的MVPD {#retriev-proxied-mvpds}

檢索由apikey參數標識的ProxyMVPD的代理MVPD的當前清單。

| 端點 | 調用者 | 請求標題 | HTTP方法 | HTTP響應 |
|---|---|---|---|---|
| &lt;fqdn>/control/v1/proxiedMvpds | 代理MVPD | apikey（強制） | GET | <ul><li> 200（確定） — 已成功處理請求，響應包含XML格式的ProxidedMVPD清單</li><li>401（未授權） — 對提供的憑據要求用戶身份驗證或未授予授權。  指示以下操作之一：<ul><li>請求標頭中不存在apikey令牌</li><li>請求源於允許清單中不存在的IP地址</li><li>令牌無效</li></ul></li><li>403（禁止） — 表示所提供的參數不支援該操作，或者代理MVPD未設定為代理或缺少代理</li><li>405（不允許使用方法） — 使用了GET或POST以外的HTTP方法。 通常不支援HTTP方法，或者不支援此特定終結點。</li><li>500（內部伺服器錯誤） — 在請求過程中在伺服器端引發錯誤。</li></ul> |

捲曲示例：

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

推送與apikey參數標識的代理MVPD整合的MVPD陣列。

| 端點 | 調用者 | 請求標題 | HTTP方法 | HTTP響應 |
|:------------------------------:|:---------:|:--------------------------------------------:|:-----------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| &lt;fqdn>/control/v1/proxiedMvpds | 代理MVPD | apikey（強制）代理 — mvpds（強制） | POST | <ul><li>201（已建立） — 已成功處理推送</li><li>400（錯誤請求） — 伺服器不知道如何處理請求：<ul><li>傳入的XML不符合此規範中發佈的架構</li><li>代理的mvpds沒有唯一的ID</li><li>推送的requestorId不存在400響應代碼的其他Servlet容器原因</li></ul><li>401（未授權） — apikey無效或呼叫者IP不在允許清單中</li><li>403（禁止） — 表示所提供的參數不支援該操作，或者代理MVPD未設定為代理或缺少代理</li><li>405（不允許使用方法） — 使用了GET或POST以外的HTTP方法。 通常不支援HTTP方法，或者不支援此特定終結點。</li><li>500（內部伺服器錯誤） — 在請求過程中在伺服器端引發錯誤。</li></ul> |

捲曲示例：

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

Adobe Primetime驗證建議ProxyMVPD只在與上次推送相比發生更改時才推送其ProxiedMVPD清單。

### 刪除代理的MVPD {#delete-proxied-freqency}

如果ProxyMVPD推送具有空ProxiedMVPD清單的XML記錄，則該空清單將像任何清單一樣儲存在系統中，從而有效地刪除前一個清單。



## XSD格式 {#xsd-format}

Adobe定義了以下接受格式，用於將代理MVPD從公共Web服務過帳/檢索到公共Web服務：

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

**元素注釋：**

* `id` （必需） — 代理的MVPD ID必須是與MVPD名稱相關的字串，使用以下任何字元（因為為了跟蹤目的，程式設計師將會向其公開）:
   * 任何字母數字字元、下划線(&quot;_&quot;)和連字元(&quot;-&quot;)。
   * idID必須符合以下規則運算式：
      `(a-zA-Z0-9((-)|_)*)`

      因此，它必須至少包含一個字元，以字母開頭，並以任何字母、數字、短划線或下划線開頭。

* `iframeSize` （可選） — iframeSize元素是可選的，並定義如果MVPD身份驗證頁應位於iFrame中，則iFrame的大小。 否則，如果iframeSize元素不存在，則驗證將在完整的瀏覽器重定向頁中進行。
* `requestorIds` （可選） — 請求者IDS值將由Adobe提供。 要求代理的MVPD應與至少一個請求者ID整合。 如果代理的MVPD元素上不存在「requestorIds」標籤，則代理的MVPD將與在代理MVPD下整合的所有可用請求器整合。
* `ProviderID` （可選） — 當id元素上存在ProviderID屬性時，ProviderID的值將在SAML驗證請求上作為代理MVPD / SubMVPD ID（而不是id值）發送到代理MVPD。 在這種情況下，ID的值將僅用於「程式設計師」頁面上顯示的MVPD選取器，並在內部通過Adobe Primetime身份驗證使用。 ProviderID屬性的長度必須介於1到128個字元之間。

## 安全 {#security}

請求被視為有效，必須遵守下列規則：

* 請求標頭必須包含安全apikey參數。 （這是一個將唯一標識代理MVPD調用的應用程式密鑰。）
* 請求必須來自已允許的特定IP地址。
* 請求必須通過SSL協定發送。

Adobe將提供令牌的（靜態）值。 此值用於身份驗證和授權過程。  將忽略請求標頭中未列出的任何參數。

捲曲示例：

`curl -X GET -H "apikey: ???provided-by-adobe???" "https://mgmt-prequal.auth-staging.adobe.com/control/v1/proxiedMvpds"`

## 用於Adobe Primetime身份驗證環境的代理MVPD Web服務終結點 {#proxy-mvpd-wevserv-endpoints}

* **生產URL:** https://mgmt.auth.adobe.com/control/v1/proxiedMvpds
* **暫存URL:** https://mgmt.auth-staging.adobe.com/control/v1/proxiedMvpds
* **預定生產URL:** https://mgmt-prequal.auth.adobe.com/control/v1/proxiedMvpds
* **PreQual-Staging URL:** https://mgmt-prequal.auth-staging.adobe.com/control/v1/proxiedMvpds

<!--
>[!RELATEDINFORMATION]
>* [Proxy MVPD SAML integration](/help/authentication/proxy-mvpd-saml-int.md)
>* [User metadata exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Technical paper](/help/authentication/technical-paper.md)
>* [Adobe Primetime Authentication glossary](/help/authentication/glossary.md)
-->
