---
title: 如何提出隱私權要求
description: 如何提出隱私權要求
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 0%

---


# 如何提出隱私權要求 {#howto-make-privacy-request}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 識別碼和命名空間 {#identifier-namespace}

傳送存取或刪除隱私權要求時，客戶應用程式需要包含下列識別碼：

* **mvpdID** - MVPD的唯一識別碼。
* **userID**  — 唯一標識程式設計師應用程式的用戶，但從MVPD組織。 請參閱程式設計師概述中的了解用戶ID。
* **IMSOrgID** - Adobe Experience Cloud Identity Management服務組織ID，可在Adobe Experience Cloud中唯一識別客戶


請檢查以下範例：

```JSON
"userIDs": [{
     "namespace":"http://www.adobe.com/primetimeAuthentication/Dish",  -----> "Dish" is the id of the MVPD
     "type":"unregistered",
     "value":"1234-5678-8765-4321" ----> "1234-5678-8765-4321" is the userId associated with the MVPD account
}]
```

>[!IMPORTANT]
>
>使用者必須通過驗證，才能產生Primetime驗證的隱私權要求。 否則，程式設計師必須找到提取MVPD userID的其他方法。

## 請求類型 {#req-type}

Primetime驗證支援存取和刪除請求。

### 存取 {#access-req}

對於存取請求：

我們會提供回JSON檔案，其中包含為該資料主體建立的驗證和授權要求總數的摘要。
所有這些事件會依客戶篩選。


**要求範例**

您必須上傳JSON及您要提交資料存取請求的Primetime驗證識別碼。 若要查看格式正確的JSON看起來是什麼樣子，請參閱以下範例：

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

**回應範例**

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

您必須上傳JSON及您要提交資料刪除請求的Primetime驗證識別碼。 若要查看格式正確的JSON看起來是什麼樣子，請參閱以下範例：

**要求範例**

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

**回應範例**

對於刪除請求：

* 我們只共用已刪除資料的接收，而不是包含已刪除所有資料的聚合檔案。
* 回應中包含的接收包含為該資料主體找到的驗證和授權權杖總數的摘要。

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

## 如何觸發要求 {#trigger-req}

客戶有2個選項可傳送隱私權要求至Adobe:

* **手動**  — 使用 [Privacy Service使用者介面](#privacy-service-ui)
* **自動**  — 使用 [Privacy ServiceAPI ](#privacy-service-api)

### 使用Privacy ServiceUI {#privacy-service-ui}

A [完整教學課程](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=en#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_ui_tutorial.md) 有關如何訪問和使用Privacy Service用戶介面的資訊，可通過Adobe I/O服務線上獲得。 此外，客戶可以使用此連結存取有關隱私權法規的影片和文章資料庫。 按一下Adobe Experience Cloud和GDPR功能表。 這將會開啟許多影片 — 「GDPR UI使用方法」說明如何使用。

在UI中，客戶需要載入自己的IMSOrgID，以及包含每個產品之GDPR要求詳細資料的JSON。

### 使用Privacy ServiceAPI {#privacy-service-api}

Adobe Experience Platform Privacy Service可為私人資料的存取/刪除請求和選擇退出銷售請求提供共同的集中便利化。

此 **Privacy ServiceAPI檔案** 深入說明Adobe客戶如何與AdobeAPI整合。

**使用Postman（免費的協力廠商軟體）將API呼叫視覺化：**

* [Privacy ServiceGitHub上的API Postman集合](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Privacy%20Service%20API.postman_collection.json)
* [建立Postman環境的影片指南](https://video.tv.adobe.com/v/28832)
* [在Postman中匯入環境和集合的步驟](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/)


**API路徑：**

* 平台網關URL: `https://platform.adobe.io/`
* 此API的基本路徑： `/data/core/privacy/jobs`
* 完整路徑的範例： `https://platform.adobe.io/data/core/privacy/jobs/ping`


**必要標題：**

* 所有呼叫都需要標題 `Authorization`, `x-gw-ims-org-id`，和 `x-api-key`. 如需如何取得這些值的詳細資訊，請參閱 **驗證教學課程**.
* 請求內文中包含裝載的所有請求(例如POST、PUT和PATCH呼叫)都必須包含標題 `Content-Type` 值為 `application/json`.

<!--

>[!RELATEDINFORMATION]
>
>* [Privacy Services Overview](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=en#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_ui_tutorial.md)
>* Privacy Service API documentation

-->