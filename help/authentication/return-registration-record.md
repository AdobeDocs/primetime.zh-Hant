---
title: 返回註冊記錄
description: 返回註冊記錄
source-git-commit: 4c3a0dd56b4ef99ac8c57cfde61f792088b0ff4d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 2%

---


# 返回註冊記錄 {#return-registration-record}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。


## REST API終結點 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暫存 —  [api.auth.staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暫存 —  [api.auth.staging.adobe.com](http://api.auth-staging.adobe.com/)

 </br>
 

## 說明 {#description}

返回包含註冊代碼UUID、註冊代碼和散列設備ID的註冊代碼記錄。 

 

<div>


| 端點 | 已調用  </br>按 | 輸入   </br>帕拉姆 | HTTP  </br>方法 | 響應 | HTTP  </br>響應 |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>;/reggie/v1/{requestorId}/regcode/{registrationCode}</br></br>例如：</br></br>&lt;reggie_fqdn>/reggie/v1/sampleRequestorId/regcode/TJJCFK?format=xml | 流式處理應用</br></br>或</br></br>程式設計師服務 | 1。請求  </br>    （路徑元件）</br>2.  註冊碼  </br>    （路徑元件） | GET | 包含註冊代碼和資訊的XML或JSON。 請參閱下面的架構和示例。 | 200 |

{style=&quot;table-layout:auto&quot;}

</br>

| 輸入參數 | 說明 |
| --- | --- |
| 請求 | 此操作對其有效的程式設計師請求者ID。 |
| 註冊碼 | 將顯示在流設備（要輸入到驗證流）上的註冊代碼值。 |

</br>

## 響應XML架構 {#response-xml-schema}

### 註冊代碼XSD

```XML
    <?xml version="1.0" encoding="UTF-8"?>
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns="model.mvc.reggie.pass.adobe.com"
            targetNamespace="model.mvc.reggie.pass.adobe.com"
            attributeFormDefault="unqualified"
            elementFormDefault="unqualified">
        <xs:element name="regcode">
            <xs:complexType>
                <xs:all>
                    <xs:element name="id" type="xs:string" />
                    <xs:element name="code" type="xs:string" />
                    <xs:element name="requestor" type="xs:string" minOccurs="1" maxOccurs="1"/>
                    <xs:element name="mvpd" type="xs:string" minOccurs="1" maxOccurs="1"/
                    <xs:element name="generated" type="xs:long" />
                    <xs:element name="expires" type="xs:long" />
                    <xs:element name="info" type="infoType" maxOccurs="1"/>
                </xs:all>
            </xs:complexType>
        </xs:element>
        <xs:complexType name="infoType">
            <xs:all>
                <xs:element name="deviceId" type="xs:base64Binary" minOccurs="1" maxOccurs="1"/>
                <xs:element name="deviceType" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="deviceUser" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="appId" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="appVersion" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="registrationURL" type="xs:anyURI" minOccurs="0" maxOccurs="1"/>
            </xs:all>
        </xs:complexType>
    </xs:schema>
```

| 元素名稱 | 說明 |
| --- | --- |
| ID | 註冊代碼服務生成的UUID |
| 代碼 | 註冊代碼服務生成的註冊代碼 |
| 請求 | 請求者ID |
| mvpd | MVPD ID |
| 生成 | 註冊代碼建立時間戳（自1970年1月1日以來以毫秒為單位） |
| 過期 | 註冊代碼過期的時間戳（自1970年1月1日以來以毫秒為單位） |
| 設備ID | 唯一設備ID（或XSTS令牌） |
| 設備類型 | 設備類型 |
| 設備用戶 | 用戶登錄到設備 |
| 應用ID | 應用程式ID |
| appVersion | 應用程式版本 |
| 註冊URL | 要顯示給最終用戶的登錄Web應用的URL |

{style=&quot;table-layout:auto&quot;&quot;

### 示例響應 {#sample-response}

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <ns2:regcode xmlns:ns2="model.mvc.reggie.pass.adobe.com">
        <id>678f9fea-a1cafec8-1ff0-4a26-8564-f6cd020acf13</id>
        <code>TJJCFK</code>
        <requestor>sampleRequestorId</requestor>
        <mvpd>sampleMvpdId</mvpd>
        <generated>1348039846647</generated>
        <expires>1348043446647</expires>
        <info>
            <deviceId>dGhpc0lkQUR1bW15RGV2aWNlSWQ=</deviceId>
            <deviceType>xbox</deviceType>
            <deviceUser>JD</deviceUser>
            <appId>2345</appId>
            <appVersion>2.0</appVersion>
            <registrationURL>http://loginwebapp.com</registrationURL>
        </info>
    </ns2:regcode>
```

[返回REST API參考](http://tve.helpdocsonline.com/rest-api-reference)