---
title: 返回註冊記錄
description: 返回註冊記錄
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# 返回註冊記錄 {#return-registration-record}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。


## 重設API端點 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 測試 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 測試 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

 </br>
 

## 說明 {#description}

傳回包含註冊代碼UUID、註冊代碼和雜湊裝置ID的註冊代碼記錄。 

 

<div>


| 端點 | 已呼叫  </br>依據 | 輸入   </br>Params | HTTP  </br>方法 | 回應 | HTTP  </br>回應 |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>;/reggie/v1/{requestorId}/regcode/{registrationCode}</br></br>例如：</br></br>&lt;reggie_fqdn>/reggie/v1/sampleRequestorId/regcode/TJJCFK?format=xml | 串流應用程式</br></br>或</br></br>程式設計人員服務 | 1.請求者  </br>    （路徑元件）</br>2.  註冊代碼  </br>    （路徑元件） | GET | 包含註冊代碼和資訊的XML或JSON。 請參閱下方的結構和範例。 | 200 |

{style="table-layout:auto"}

</br>

| 輸入參數 | 說明 |
| --- | --- |
| 請求者 | 此操作對其有效的程式設計師請求者ID。 |
| 註冊代碼 | 顯示在串流裝置上的註冊代碼值（要輸入驗證流程）。 |

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
| id | 註冊代碼服務產生的UUID |
| 代碼 | 註冊代碼服務生成的註冊代碼 |
| 請求者 | 請求者ID |
| mvpd | MVPD ID |
| 產生 | 註冊代碼建立時間戳記（自1970年1月1日以來的毫秒） |
| 過期 | 註冊代碼過期的時間戳記（自1970年1月1日以來的毫秒） |
| deviceId | 唯一裝置ID（或XSTS代號） |
| deviceType | 裝置類型 |
| deviceUser | 使用者登入裝置 |
| appId | 應用程式ID |
| appVersion | 應用程式版本 |
| registrationURL | 要向最終用戶顯示的登錄Web應用的URL |

{style="table-layout:auto"}

### 範例回應 {#sample-response}

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
