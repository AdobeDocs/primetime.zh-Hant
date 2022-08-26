---
title: 註冊頁
description: 註冊頁
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 1%

---


# 註冊頁 {#registration-page}

## REST API終結點 {#clientless-endpoints}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

&lt;reggie_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暫存 —  [api.auth.staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暫存 —  [api.auth.staging.adobe.com](http://api.auth-staging.adobe.com/)

 </br>

## 說明 {#create-reg-code-svc}

返回隨機生成的註冊代碼和登錄頁URI。

| 端點 | 已調用  </br>按 | 輸入   </br>參數 | HTTP  </br>方法 | 響應 | HTTP  </br>響應 |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>/reggie/v1/{requestor/regcode</br>例如：</br>REGGIE_FQDN/reggie/v1/sampleRequestorId/regcode | 流式處理應用</br>或</br>程式設計師服務 | 1。請求  </br>    （路徑元件）</br>2.  設備ID（散列）   </br>    （強制）</br>3.  device_info/X-Device-Info（必需）</br>4.  mvpd（可選）</br>5.  ttl（可選）</br>6。  _設備類型_</br> 7。  _設備用戶_ （不建議使用）</br>8.  _應用ID_ （不建議使用） | POST | XML或JSON包含註冊代碼和資訊或錯誤詳細資訊（如果失敗）。 請參閱下面的架構和示例。 | 201 |

{style=&quot;table-layout:auto&quot;}

| 輸入參數 | 說明 |
| --- | --- |
| 請求 | 此操作對其有效的程式設計師請求者ID。 |
| 設備ID | 設備ID位元組。 |
| 設備資訊/</br>X設備資訊 | 流設備資訊。</br>**注釋**:此URL可以作為URL參數傳遞，但由於此參數的可能大小和對GETURL長度的限制，它應作為X-Device-Info在http標頭中傳遞。 </br>請參閱中的完整詳細資訊 [傳遞設備和連接資訊](http://tve.helpdocsonline.com/passing-device-information)。 |
| mvpd | 此操作對其有效的MVPD ID。 |
| TTL | 此重編碼應在幾秒鐘內生存多久。</br>**注釋**:ttl允許的最大值為36000秒（10小時）。 值越高，將導致400個HTTP響應（錯誤請求）。 如果 `ttl` 為空，Mogife Authentication將預設值設定為30分鐘。 |
| _設備類型_ | 設備類型（如Roku、PC）。</br>如果此參數設定正確，ESM將提供 [按設備類型分解](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) 使用Clientless時，可對Roku、AppleTV、Xbox等執行不同類型的分析。</br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br>**注釋**:device_info將替換此參數。 |
| _設備用戶_ | 設備用戶標識符。 |
| _應用ID_ | 應用程式ID/名稱。 </br>**注釋**:device_info將替換此參數。 |

{style=&quot;table-layout:auto&quot;&quot;


>[!CAUTION]
>
>**流設備IP地址**
></br>
>對於客戶端到伺服器實現，流設備IP地址隨此調用隱式發送。  對於伺服器到伺服器實施， **重碼** 呼叫是程式設計師服務，而不是流式設備，需要以下報頭才能傳遞流式設備IP地址：
>
>
>
```
>X-Forwarded-For : <streaming_device_ip> 
>```
>
>何處 `<streaming\_device\_ip>` 是流設備公共IP地址。
></br></br>
>示例：</br>
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
| ID | 註冊代碼服務生成的UUID |
| 代碼 | 註冊代碼服務生成的註冊代碼 |
| 請求 | 請求者ID |
| mvpd | Mvpd ID |
| 生成 | 註冊代碼建立時間戳（自1970年1月1日以來以毫秒為單位） |
| 過期 | 註冊代碼過期的時間戳（自1970年1月1日以來以毫秒為單位） |
| 設備ID | 唯一設備ID（或XSTS令牌） |
| 設備類型 | 設備類型 |
| 設備用戶 | 用戶登錄到設備 |
| 應用ID | 應用程式ID |
| appVersion | 應用程式版本 |
| 註冊URL | 要顯示給最終用戶的登錄Web應用的URL |

{style=&quot;table-layout:auto&quot;}
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
 

### 示例響應 {#sample-response}

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

[返回REST API參考](http://tve.helpdocsonline.com/rest-api-reference)
