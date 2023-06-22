---
title: 原則工作流程詳細資料
description: 原則工作流程詳細資料
copied-description: true
exl-id: e3daf7a9-def0-48a9-8190-adb25eec7b59
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# BEES工作流程 {#bees-workflow}

**摘要：**

* **原則**  — 建立DRM BEES感知原則，指示使用此原則封裝的所有內容都需要BEES。
* **封裝**  — 使用BEES感知DRM原則封裝內容。
* **驗證**  — 驗證您的使用者端裝置，並使用Primetime DRM API或Primetime API，將此代號與Primetime Cloud DRM建立關聯。 這麼做會讓使用者端裝置將此驗證權杖連同所有授權請求一起傳送至Primetime Cloud DRM。 Primetime Cloud DRM不會處理此變數，而是會將其以不透明blob的形式傳遞至您的BEES端點以進行處理。
* **授權**  — 請求受保護內容的授權。 使用者端裝置會自動將您先前設定的驗證Token附加至呼叫。
* **權利** - Primetime Cloud DRM會判斷內容是否封裝了需要BEES的原則。 Primetime Cloud DRM會建構JSON要求以傳送至BEES端點。 BEES回應將會指示Primetime Cloud DRM是否核發授權，以及選擇使用哪個DRM政策。

## 原則工作流程詳細資料 {#policy-workflow-details}

當Primetime Cloud DRM處理授權請求時，它會剖析請求中的DRM原則，以判斷是否需要在顯示內容之前呼叫後端權益服務。 如果蜜蜂呼叫 *是* 必要時，Primetime Cloud DRM會建立BEES要求，然後剖析DRM原則，以取得BEES要求的指定BEES URL端點。

套用指示BEES需求的DRM原則，在原則中指定以下兩個自訂屬性：

* `policy.customProp.1=bees.required=<true | false>`
* `policy.customProp.2=bees.url=<url to your BEES endpoint>`

<!--<a id="example_F617FC49A4824C0CB234C92E57D876D3"></a>-->

例如，使用Primetime DRM原則管理員( [!DNL AdobePolicyManager.jar])，則可在「 」中指定以下兩個自訂屬性 [!DNL flashaccesstools.properties] 設定檔：

* `policy.customProp.1=bees.required=true`
* `policy.customProp.2=bees.url=https://mybeesserver.example.com/bees`

>[!NOTE]
>
>如果您已使用 `policy.customProp.1` 或 `policy.customProp.2` 若是另一個屬性，則只需對較新的屬性使用唯一數字即可。

## 封裝工作流程詳細資料 {#package-workflow-details}

在封裝受Adobe存取保護的內容時，您必須將其中一個BEES感知的DRM政策套用至內容。

## 驗證工作流程詳細資料 {#authentication-workflow-details}

為了讓您的BEES端點做出許可權決策，使用者端裝置必須提供驗證資訊。 您可以使用自己的客戶特定驗證Token來達到此目的。

Primetime Cloud DRM不必瞭解此Token，只需將此Token傳遞至您的BEES端點即可。 使用者端裝置負責建立或取得此Token，並使用進行設定 `DRMManager.setAuthenticationToken()` API。

請執行以下動作來將此權杖與Primetime Cloud DRM建立關聯，以便隨授權請求傳送：

例項化 `DRMManager` 物件，其中包含針對Primetime Cloud DRM封裝之內容的DRM中繼資料。

此 `setAuthenticationToken()` 方法的運作方式是將指定的位元組陣列與用來具現化的DRM中繼資料中提供的License Server URL建立關聯 `DRMManager`.

```java
//client device acquires auth token needed by your BEES endpoint  
DRMManager mgr = new DRMManager(<DRM Metadata of CloudDRM content>);  
mgr.setAuthenticationToken(<auth token>);
```

Token會隨所有授權請求一起傳送，直到透過呼叫清除Token為止 `.setAuthenticationToken` 以null作為引數。

## 授權工作流程詳細資料{#license-workflow-details}

透過呼叫，向Primetime Cloud DRM請求授權 `mgr.loadVoucher()`.

## 權益請求和回應詳細資料{#entitlement-request-and-response-details}

當Primetime Cloud DRM判斷內容是以BEES感知DRM原則封裝時，它會建構以下JSON請求以傳送至DRM原則中指定的BEES端點：

```
{
    "title":"Entitlement Request",
    "type":"object",
    "properties": {
        "messageID": {
            "type":"string",
            "description":"Unique ID for this message. Used to confirm that the
                           returned response is for this particular message."
        },
        "version": {
            "type":"string",
            "description":"BEES Request Version. Currently 1."
        },
        "contentID": {
            "type":"string",
            "description":"Content ID (GUID)"
        },
        "customerSpecificAuthToken": {
            "type":"string",
            "description":"Base64-encoded authentication token. Must be set
                           explicitly by client before making the license request."
        }
    },
    "required": [
        "messageID",
        "version",
        "contentID"
    ]
}
```

BEES端點應會產生下列回應：

```
{
    "title":"Entitlement Response",
    "type":"object",
    "properties": {
        "messageID": {
            "type":"string",
            "description":"ID of the Entitlement Request that this Response is
                           handling. Must exactly match the ID of the request
                           or this response will be rejected."
        },
        "version": {
            "type":"string",
            "description":"BEES Response Version. Currently 1."
        },
        "isAllowed": {
            "type":"boolean",
            "description":"Grant the license or not."
        },
        "policy": {
            "type":"string",
            "description":"Base64-encoded policy to enforce  If no policy is
                           provided, the policy that was packaged with the content
                           during packaging time will be used to generate the license."
        },
        "error": {
            "type":"integer",
            "description":"An error number produced by the entitlement server.
                           Will be passed to the client as the 'code' field of
                           the server error response."
        },
        "errorText": {
            "type":"string",
            "description":"Additional error information produced by the
                           entitlement server. Will be passed to the client as
                           the 'text' field of the server error response."
        }
    },
    "required": [
        "messageID",
        "version",
        "isAllowed"
    ]
}
```

Primetime Cloud DRM會使用回應來判斷是否應該向請求裝置發放授權，以及是否應該將新的DRM政策取代至授權產生程式。 若 `isAllowed` 是 `true` 而且回應中不會提供任何原則，那麼內容封裝期間使用的原始DRM原則將用於產生授權。
