---
title: 如何發出隱私請求
description: 如何發出隱私請求
exl-id: abb21306-98d6-4899-914a-bdfa85cbd204
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 0%

---

# 如何發出隱私請求 {#howto-make-privacy-request}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 標識符和命名空間 {#identifier-namespace}

在發送訪問或刪除隱私請求時，客戶應用程式需要包括以下標識符：

* **mvpdID** - MVPD的唯一標識符。
* **用戶ID**  — 唯一標識程式設計師應用的用戶，但是從MVPD組織。 請參閱程式設計師概述中的瞭解用戶ID。
* **IMSOrgID** -Adobe Experience CloudIdentity Management服務組織ID，它唯一地標識了Adobe Experience Cloud的客戶


請查看以下示例：

```JSON
"userIDs": [{
     "namespace":"http://www.adobe.com/primetimeAuthentication/Dish",  -----> "Dish" is the id of the MVPD
     "type":"unregistered",
     "value":"1234-5678-8765-4321" ----> "1234-5678-8765-4321" is the userId associated with the MVPD account
}]
```

>[!IMPORTANT]
>
>用戶必須經過身份驗證才能生成黃金時段身份驗證的隱私請求。 否則，程式設計師必須找到提取MVPD userID的其他方法。

## 請求類型 {#req-type}

Mogine Authentication支援訪問和刪除請求。

### 訪問 {#access-req}

對於訪問請求：

我們將返回一個JSON檔案，其中包含為該資料主題建立的身份驗證和授權請求總數的摘要。
所有這些事件都按客戶篩選。


**請求示例**

必須上載包含要為其提交資料存取請求的黃金時段身份驗證標識符的JSON。 要查看格式良好的JSON的外觀，請參見以下示例：

```JSON
{
    "companyContexts": [{
            "namespace": "imsOrgID",
            "value": "1234567890@AdobeOrg"
        }
    ],
    "users": [{
            "key": "John Dow",
            "action": ["access"],
            "userIDs": [{
                "namespace":"http://www.adobe.com/primetimeAuthentication/Dish",
                "type":"unregistered",
                "value":"1234-5678-8765-4321"
             }]
         
        }
    ],
    
    "include":["primetimeAuthentication"],
    "regulation" : "ccpa"
}
```

**響應樣本**

```JSON
{
    "jobId": "d9a6b417-f619-4420-82a3-09f61fa8eff3",
    "requestId": "15765127177927284RX-739",
    "userKey": "John Dow",
    "action": "access",
    "status": "complete",
    "submittedBy": "564f7c9a-e0c8-4e74-99b8-20317ae1e235@techacct.adobe.com",
    "createdDate": "12/16/2019 04:11 PM GMT",
    "lastModifiedDate": "12/16/2019 04:15 PM GMT",
    "userIds": [
        {
            "namespace": "http://www.adobe.com/primetimeAuthentication/Dish",
            "value": "1234-5678-8765-4321",
            "type": "unregistered",
            "isDeletedClientSide": false
        }
    ],
    "productResponses": [
        {
            "product": "Primetime Authentication",
            "retryCount": 0,
            "processedDate": "12/16/2019 04:15 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "results": {
                    "userContexts": [
                        {
                            "namespace": "http://www.adobe.com/primetimeAuthentication/Dish",
                            "namespaceId": 0,
                            "value": "1234-5678-8765-4321",
                            "type": "unregistered"
                        }
                    ],
                    "receiptData": {
                        "createdAt": "2019-12-16T16:15:23.4Z",
                        "message": "Data summary",
                        "numberOfAuthenticationSessions": "6",
                        "numberOfAuthorizationDecisions": "11"
                    }
                },
                "message": "Success"
            }
        }
    ],
    "downloadUrl": "https://va7gdprdevblob.blob.core.windows.net/va7gdprdevblobpublic/usa/4161962b9e8ef0027453d7cc02ecd93d/d9a6b417-f619-4420-82a3-09f61fa8eff3/d9a6b417-f619-4420-82a3-09f61fa8eff3.zip",
    "regulation": "ccpa"
}
```

### 刪除 {#delete-req}

必須上載包含要為其提交資料刪除請求的黃金時段身份驗證標識符的JSON。 要查看格式良好的JSON的外觀，請參見以下示例：

**請求示例**

```JSON
{
    "companyContexts": [{
            "namespace": "imsOrgID",
            "value": "1234567890@AdobeOrg"
        }
    ],
    "users": [{
            "key": "John Dow",
            "action": ["delete"],
            "userIDs": [{
                "namespace":"http://www.adobe.com/primetimeAuthentication/Dish",
                "type":"unregistered",
                "value":"1234-5678-8765-4321"
             }]
         
        }
    ],
    
    "include":["primetimeAuthentication"],
    "regulation" : "ccpa"
}
```

**響應樣本**

對於刪除請求：

* 我們只共用一個資料被刪除的回執，而不是一個包含所有已刪除資料的聚合檔案。
* 響應中包含的接收包含為該資料主題找到的驗證和授權令牌總數的摘要。

```JSON
{
    "jobId": "aab380d1-a0cd-4a0d-ba95-2649ee90c063",
    "requestId": "15759883098453100RX-074",
    "userKey": "John Dow",
    "action": "delete",
    "status": "complete",
    "submittedBy": "564f7c9a-e0c8-4e74-99b8-20317ae1e235@techacct.adobe.com",
    "createdDate": "12/10/2019 02:31 PM GMT",
    "lastModifiedDate": "12/10/2019 02:34 PM GMT",
    "userIds": [
        {
            "namespace": "http://www.adobe.com/primetimeAuthentication/Dish",
            "value": "1234-5678-8765-4321",
            "type": "unregistered",
            "isDeletedClientSide": false
        }
    ],
    "productResponses": [
        {
            "product": "Primetime Authentication",
            "retryCount": 0,
            "processedDate": "12/10/2019 02:34 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "results": {
                    "userContexts": [
                        {
                            "namespace": "http://www.adobe.com/primetimeAuthentication/Dish",
                            "namespaceId": 0,
                            "value": "1234-5678-8765-4321",
                            "type": "unregistered"
                        }
                    ],
                    "receiptData": {
                        "createdAt": "2019-12-10T14:34:55.274Z",
                        "message": "Data summary",
                        "numberOfAuthenticationSessions": "2",
                        "numberOfAuthorizationDecisions": "3"
                    }
                },
                "message": "Success"
            }
        }
    ],
    "downloadUrl": "https://va7gdprdevblob.blob.core.windows.net/va7gdprdevblobpublic/usa/4161962b9e8ef0027453d7cc02ecd93d/aab380d1-a0cd-4a0d-ba95-2649ee90c063/aab380d1-a0cd-4a0d-ba95-2649ee90c063.zip",
    "regulation": "ccpa"
}
```

## 如何觸發請求 {#trigger-req}

客戶有2個選項可將隱私請求發送到Adobe:

* **手動**  — 使用 [Privacy Service用戶介面](#privacy-service-ui)
* **自動**  — 使用 [Privacy ServiceAPI ](#privacy-service-api)

### 使用Privacy ServiceUI {#privacy-service-ui}

A [完整教程](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=en#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_ui_tutorial.md) 有關如何訪問和使用Privacy Service用戶介面的資訊，可通過Adobe I/O服務線上獲取。 此外，客戶可以使用此連結訪問有關隱私法規的視頻和文章庫。 按一下「Adobe Experience Cloud」和「GDPR」菜單。 這將開啟許多視頻 — 「GDPR UI How-to 」解釋如何使用它。

在UI中，客戶需要載入其自己的IMSOrgID和包含每個產品的GDPR請求詳細資訊的JSON。

### 使用Privacy ServiceAPI {#privacy-service-api}

Adobe Experience Platform Privacy Service為私人資料的訪問/刪除請求和選擇退出銷售請求提供共同的集中便利。

的 **Privacy ServiceAPI文檔** 深入介紹Adobe客戶如何與AdobeAPI整合。

**使用Postman（免費第三方軟體）可視化API調用：**

* [Privacy ServiceGitHub上的APIPostman集合](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Privacy%20Service%20API.postman_collection.json)
* [建立Postman環境的視頻指南](https://video.tv.adobe.com/v/28832)
* [在Postman導入環境和集合的步驟](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/)


**API路徑：**

* 平台網關URL: `https://platform.adobe.io/`
* 此API的基本路徑： `/data/core/privacy/jobs`
* 完整路徑示例： `https://platform.adobe.io/data/core/privacy/jobs/ping`


**必需的標題：**

* 所有呼叫都需要標頭 `Authorization`。 `x-gw-ims-org-id`, `x-api-key`。 有關如何獲取這些值的詳細資訊，請參見 **驗證教程**。
* 請求正文中具有負載的所有請求(如POST、PUT和PATCH調用)都必須包括標頭 `Content-Type` 值為 `application/json`。

<!--

>[!RELATEDINFORMATION]
>
>* [Privacy Services Overview](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=en#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_ui_tutorial.md)
>* Privacy Service API documentation

-->
