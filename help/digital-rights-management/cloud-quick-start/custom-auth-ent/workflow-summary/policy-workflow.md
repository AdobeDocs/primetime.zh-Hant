---
seo-title: 原則工作流程詳細資訊
title: 原則工作流程詳細資訊
uuid: b355fcf6-3416-440f-9b30-a155e20f9f74
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# 蜜蜂工作流程 {#bees-workflow}

**摘要：**

* **策略** -建立DRM BEES感知策略，該策略指示使用此策略打包的所有內容都需要BEES。
* **封裝** -使用BEES-aware DRM政策封裝內容。
* **驗證** -驗證您的用戶端裝置，並使用Primetime DRM API或Primetime API，將此Token與Primetime Cloud DRM建立關聯。 這麼做會導致用戶端裝置將此驗證Token傳送至Primetime Cloud DRM，以及所有授權要求。 Primetime Cloud DRM不會處理Thistoken，但會將它傳遞（作為不透明的Blob）至您的BEES端點進行處理。
* **授權** -請求您受保護內容的授權。 用戶端裝置會自動將您先前設定的驗證Token附加至呼叫。
* **權益** - Primetime Cloud DRM將判斷內容已與需要BEES的原則一起封裝。 Primetime Cloud DRM將建構JSON要求，以傳送至BEES端點。 BEES回應會指示Primetime Cloud DRM是否核發授權，以及（可選）要使用的DRM政策。

## 原則工作流程詳細資訊 {#policy-workflow-details}

當Primetime Cloud DRM處理授權請求時，會分析請求中的DRM原則，以決定在內容可顯示之前是否需要呼叫後端權益服務。 如果需要BEES *呼叫* ,Primetime Cloud DRM將建立BEES請求，然後剖析DRM原則，以取得BEES請求的指定BEES URL端點。

應用指示BEES要求的DRM策略，在策略中指定以下兩個自定義屬性：

    * &#39;policy.customProp.1=bees.required=&lt;true| false>`
    * &#39;policy.customProp.2=bees.url=&lt;url to your BEES endpoint>`

<!--<a id="example_F617FC49A4824C0CB234C92E57D876D3"></a>-->

例如，使用Primetime DRM策略管理器( [!DNL AdobePolicyManager.jar])，您可以在配置檔案中指定以下兩個自 [!DNL flashaccesstools.properties] 定義屬性：

* `policy.customProp.1=bees.required=true`
* `policy.customProp.2=bees.url=https://mybeesserver.example.com/bees`

>[!NOTE]
>
>如果您已在使用或 `policy.customProp.1` 用於其 `policy.customProp.2` 他屬性，只需對較新屬性使用唯一數字即可。

## 封裝工作流程詳細資訊 {#package-workflow-details}

在封裝Adobe Access保護內容時，您必須將其中一個BEES感知的DRM政策套用至內容。

## 驗證工作流程詳細資訊 {#authentication-workflow-details}

為了讓您的BEES端點能夠做出權益決策，用戶端裝置必須提供驗證資訊。 您可以使用您自己的客戶專屬驗證Token來完成此作業。

Primetime Cloud DRM不需要瞭解此代號——它只是將此代號傳遞至您的BEES端點。 用戶端裝置負責建立或取得此Token，並使用 `DRMManager.setAuthenticationToken()` API加以設定。

請執行下列動作，將此Token與Primetime Cloud DRM建立關聯，以便隨授權要求傳送：

使用 `DRMManager` 為Primetime Cloud DRM封裝的內容的DRM中繼資料實例化物件。

該方 `setAuthenticationToken()` 法通過將給定位元組陣列與用於實例化的DRM元資料中提供的許可證伺服器URL相關聯而起作用 `DRMManager`。

```java
//client device acquires auth token needed by your BEES endpoint  
DRMManager mgr = new DRMManager(<DRM Metadata of CloudDRM content>);  
mgr.setAuthenticationToken(<auth token>);
```

Token會隨所有授權要求傳送，直到以空值為參數呼叫 `.setAuthenticationToken` 來清除Token為止。

## 授權工作流程詳細資訊{#license-workflow-details}

透過呼叫向Primetime Cloud DRM要求授權 `mgr.loadVoucher()`。

## 權益要求和回應詳細資訊{#entitlement-request-and-response-details}

當Primetime Cloud DRM判斷內容已封裝為具有BEES感應的DRM原則時，它會建構下列JSON要求，以傳送至DRM原則中指定的BEES端點：

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

BEES端點應提供以下響應：

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

Primetime Cloud DRM會使用回應來判斷是否應向請求裝置發放授權，以及是否應將新的DRM原則取代至授權產生程式。 如果 `isAllowed` 是 `true` 且回應中未提供原則，則內容封裝期間使用的原始DRM原則將用來產生授權。