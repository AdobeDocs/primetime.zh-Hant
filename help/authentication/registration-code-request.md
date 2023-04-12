---
title: 註冊頁面
description: 註冊頁面
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---


# 註冊頁面 {#registration-page}

## 重設API端點 {#clientless-endpoints}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

&lt;reggie_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 測試 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 測試 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

 </br>

## 說明 {#create-reg-code-svc}

返回隨機生成的註冊代碼和登錄頁URI。

| 端點 | 已呼叫  </br>依據 | 輸入   </br>參數 | HTTP  </br>方法 | 回應 | HTTP  </br>回應 |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>/reggie/v1/{requestor/regcode</br>例如：</br>REGGEI_FQDN/reggie/v1/sampleRequestorId/regcode | 串流應用程式</br>或</br>程式設計人員服務 | 1.請求者  </br>    （路徑元件）</br>2.  deviceId（雜湊）   </br>    （強制）</br>3.  device_info/X-Device-Info（強制）</br>4.  mvpd（選用）</br>5。  ttl（可選）</br>6.  _deviceType_</br> 7.  _deviceUser_ （已過時）</br>8.  _appId_ （已過時） | POST | XML或JSON包含註冊代碼和資訊，若失敗則顯示錯誤詳細資訊。 請參閱下方的結構和範例。 | 201 |

{style="table-layout:auto"}

| 輸入參數 | 說明 |
| --- | --- |
| 請求者 | 此操作對其有效的程式設計師請求者ID。 |
| deviceId | 設備id位元組。 |
| device_info/</br>X-Device-Info | 串流裝置資訊。</br>**附註**:此URL可以作為URL參數傳遞，但由於此參數的可能大小及GETURL長度的限制，因此URL應以X-Device-Info在http標題中傳遞。 </br>請參閱 [傳遞裝置和連線資訊](/help/authentication/passing-client-information-device-connection-and-application.md). |
| mvpd | 此操作對其有效的MVPD ID。 |
| ttl | 此規則程式碼的存留時間應以秒為單位。</br>**附註**:允許的ttl最大值為36000秒（10小時）。 值較高會導致400 HTTP回應（錯誤要求）。 若 `ttl` 保留為空白，則Primetime驗證會設定30分鐘的預設值。 |
| _deviceType_ | 裝置類型（例如Roku、PC）。</br>如果此參數設定正確，ESM將提供以下量度： [按設備類型劃分](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) 使用無用戶端時，以便執行不同類型的分析，例如Roku、AppleTV和Xbox。</br>看， [在傳遞量度中使用無用戶端裝置類型參數的優點&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br>**附註**:device_info將替換此參數。 |
| _deviceUser_ | 裝置使用者識別碼。 |
| _appId_ | 應用程式ID/名稱。 </br>**附註**:device_info會取代此參數。 |

{style="table-layout:auto"}


>[!CAUTION]
>
>**串流裝置IP位址**
></br>
>對於用戶端對伺服器實作，串流裝置IP位址會以此呼叫隱式傳送。  針對伺服器對伺服器實作，其中 **regcode** 呼叫是程式設計員服務而不是流式設備，需要以下標題才能傳遞流式設備IP地址：
>
>
>
```
>X-Forwarded-For : <streaming_device_ip> 
>```
>
>where `<streaming\_device\_ip>` 是串流裝置的公用IP位址。
></br></br>
>範例：</br>
>
>
```
>POST /reggie/v1/{req_id}/regcode HTTP/1.1</br>X-Forwarded-For:203.45.101.20
>```
</br>

### 響應XML架構 {#xml-schema}


#### 註冊代碼XSD {#registration-code-xsd}

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

 </br>

| 元素名稱 | 說明 |
| --------------- | ------------------------------------------------------------------------------------ |
| id | 註冊代碼服務產生的UUID |
| 代碼 | 註冊代碼服務生成的註冊代碼 |
| 請求者 | 請求者ID |
| mvpd | Mvpd ID |
| 產生 | 註冊代碼建立時間戳記（自1970年1月1日以來的毫秒） |
| 過期 | 註冊代碼過期的時間戳記（自1970年1月1日以來的毫秒） |
| deviceId | 唯一裝置ID（或XSTS代號） |
| deviceType | 裝置類型 |
| deviceUser | 使用者登入裝置 |
| appId | 應用程式ID |
| appVersion | 應用程式版本 |
| registrationURL | 要向最終用戶顯示的登錄Web應用的URL |

{style="table-layout:auto"}
 </br>

 

### 錯誤消息XSD  {#error-message}

```XML
    <?xml version="1.0" encoding="UTF-8"?>
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns="rest.pass.adobe.com"
               targetNamespace="rest.pass.adobe.com"
               attributeFormDefault="unqualified"
               elementFormDefault="unqualified">
        <xs:element name="error">
            <xs:complexType>
                <xs:all>
                    <xs:element name="status" type="xs:int" minOccurs="1" maxOccurs="1"/>
                    <xs:element name="message" type="xs:string" minOccurs="1" maxOccurs="1"/>
                    <xs:element name="details" type="xs:string" minOccurs="0" maxOccurs="1"/>
                </xs:all>
            </xs:complexType>
        </xs:element>
    </xs:schema>
```
 

### 範例回應 {#sample-response}

**XML:**

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
 
**JSON:**

```JSON
    {
        "id": "678f9fea-9d364b29-246c-488f-b97e-298566d1b9e0",
        "code": "D4BDU2W",
        "requestor": "sampleRequestorId",
        "mvpd": "sampleMvpdId",
        "generated": 1348039555877,
        "expires": 1348043155877,
        "info": {
            "deviceId": "dGhpc0l.kQUR1bW15RGV2.aWNlSWQ=",
            "deviceType": "xboxOne",
            "deviceUser": "JD",
            "appId": "2345",
            "appVersion": "2.0",
            "registrationURL": "http://loginwebapp.com"
        }
    }
```

