---
title: 如何提出隱私權請求
description: 如何提出隱私權請求
exl-id: abb21306-98d6-4899-914a-bdfa85cbd204
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 0%

---

# 如何提出隱私權請求 {#howto-make-privacy-request}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 識別碼和名稱空間 {#identifier-namespace}

傳送存取或刪除隱私權請求時，客戶應用程式必須包含下列識別碼：

* **mvpdID** - MVPD的唯一識別碼。
* **userID**  — 唯一識別程式設計師應用程式的使用者，但源自MVPD。 請參閱瞭解程式設計師概觀中的使用者ID 。
* **IMSOrgID** - Adobe Experience Cloud Identity Management服務組織ID，可在Adobe Experience Cloud中唯一識別客戶


請檢查下列範例：

```JSON
"userIDs": [{
     "namespace":"http://www.adobe.com/primetimeAuthentication/Dish",  -----> "Dish" is the id of the MVPD
     "type":"unregistered",
     "value":"1234-5678-8765-4321" ----> "1234-5678-8765-4321" is the userId associated with the MVPD account
}]
```

>[!IMPORTANT]
>
>使用者必須經過驗證，才能產生Primetime驗證的隱私權請求。 否則，程式設計師必須找到其他方法來擷取MVPD userID。

## 請求型別 {#req-type}

Primetime驗證支援存取和刪除請求。

### 存取 {#access-req}

針對存取要求：

我們將提供包含為該資料主體建立的驗證和授權請求總數摘要的JSON檔案。
所有這些事件都是根據客戶篩選的。


**要求範例**

您必須上傳具有您要提交資料存取請求的Primetime驗證識別碼的JSON。 若要檢視格式正確的JSON是什麼樣子，請參閱此範例：

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

您必須上傳具有您要提交資料刪除請求之Primetime驗證識別碼的JSON。 若要檢視格式正確的JSON是什麼樣子，請參閱此範例：

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

對於Delete請求：

* 我們只分享已移除資料的回條，而非包含所有已移除資料的彙總檔案。
* 回應中包含的回條包含該資料主體找到之驗證和授權Token總數的摘要。

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

客戶若要傳送隱私權請求給Adobe，有2個選項可選：

* **手動**  — 使用 [Privacy Service使用者介面](#privacy-service-ui)
* **自動**  — 使用 [PRIVACY SERVICEAPI ](#privacy-service-api)

### 使用Privacy ServiceUI {#privacy-service-ui}

A [完成教學課程](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=en#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_ui_tutorial.md) 您可透過Privacy Service服務線上取得如何存取及使用Adobe I/O使用者介面的資訊。 此外，客戶可以使用此連結來存取隱私權法規的影片和文章庫。 按一下Adobe Experience Cloud和GDPR功能表。 本影片將開啟許多影片 — 「GDPR UI使用說明」說明如何使用。

在UI中，客戶需要載入他們自己的IMSOrgID和包含每個產品的GDPR請求詳細資料的JSON。

### 使用Privacy Service API {#privacy-service-api}

Adobe Experience Platform Privacy Service以集中方式提供存取/刪除私人資料請求的常見便利，以及選擇退出銷售的請求。

此 **Privacy Service API檔案** 深入涵蓋Adobe客戶如何與AdobeAPI整合。

**使用Postman （免費的第三方軟體）將API呼叫視覺化：**

* [在GitHub上Privacy ServiceAPI Postman集合](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Privacy%20Service%20API.postman_collection.json)
* [建立Postman環境的影片指南](https://video.tv.adobe.com/v/28832)
* [在Postman中匯入環境和集合的步驟](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/)


**API路徑：**

* 平台閘道URL： `https://platform.adobe.io/`
* 此API的基本路徑： `/data/core/privacy/jobs`
* 完整路徑的範例： `https://platform.adobe.io/data/core/privacy/jobs/ping`


**必要的標頭：**

* 所有呼叫都需要標題 `Authorization`， `x-gw-ims-org-id`、和 `x-api-key`. 如需如何取得這些值的詳細資訊，請參閱 **驗證教學課程**.
* 要求內文中具有裝載的所有要求(例如POST、PUT和PATCH呼叫)都必須包含標頭 `Content-Type` 具有值 `application/json`.

<!--

>[!RELATEDINFORMATION]
>
>* [Privacy Services Overview](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=en#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_ui_tutorial.md)
>* Privacy Service API documentation

-->
