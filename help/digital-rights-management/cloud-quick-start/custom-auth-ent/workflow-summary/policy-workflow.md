---
title: 策略工作流詳細資訊
description: 策略工作流詳細資訊
copied-description: true
exl-id: e3daf7a9-def0-48a9-8190-adb25eec7b59
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# 蜂類工作流 {#bees-workflow}

**摘要：**

* **策略**  — 建立DRM BEES感知策略，該策略指示使用此策略打包的所有內容都需要BEES。
* **包裝**  — 使用支援蜂類的DRM策略打包內容。
* **驗證**  — 驗證您的客戶端設備，並使用黃金時段DRM API或黃金時段API將此令牌與黃金時段雲DRM關聯。 這樣做將導致客戶端設備將此身份驗證令牌連同所有許可證請求一起發送到Mighine Cloud DRM。 黃金時段雲DRM將不處理審核，而是將其作為不透明的blob傳遞給您的BEES終結點進行處理。
* **許可**  — 請求受保護內容的許可證。 客戶端設備將自動將先前設定的驗證令牌附加到呼叫。
* **權利**  — 黃金時段雲DRM將確定內容是與需要BEES的策略打包的。 黃金時段雲DRM將構建JSON請求以發送到BEES端點。 BEES響應將指示黃金時段雲DRM是否發放許可證，以及可選地，使用哪個DRM策略。

## 策略工作流詳細資訊 {#policy-workflow-details}

當黃金時段雲DRM處理許可請求時，它分析請求中的DRM策略，以確定是否需要在顯示內容之前調用後端權利服務。 如果蜜蜂呼叫 *是* 需要，Mighine Cloud DRM將建立BEES請求，然後分析DRM策略以獲取BEES請求的指定BEES URL端點。

應用指示BEES要求的DRM策略，在策略中指定以下兩個自定義屬性：

* `policy.customProp.1=bees.required=<true | false>`
* `policy.customProp.2=bees.url=<url to your BEES endpoint>`

<!--<a id="example_F617FC49A4824C0CB234C92E57D876D3"></a>-->

例如，使用Mogine DRM策略管理器( [!DNL AdobePolicyManager.jar])，您可以在 [!DNL flashaccesstools.properties] 配置檔案：

* `policy.customProp.1=bees.required=true`
* `policy.customProp.2=bees.url=https://mybeesserver.example.com/bees`

>[!NOTE]
>
>如果您已在使用 `policy.customProp.1` 或 `policy.customProp.2` 對於另一個屬性，只需為較新的屬性使用唯一數字。

## 包工作流詳細資訊 {#package-workflow-details}

在打包受Adobe訪問保護的內容期間，必須對內容應用一個支援蜂類的DRM策略。

## 驗證工作流詳細資訊 {#authentication-workflow-details}

為了讓您的BEES端點做出權利決定，客戶端設備必須提供身份驗證資訊。 通過使用您自己的客戶特定身份驗證令牌來完成此任務。

黃金時段雲DRM不必理解此令牌 — 它只需將此令牌傳遞給您的BEES端點。 客戶端設備負責建立或獲取此令牌並使用 `DRMManager.setAuthenticationToken()` API。

執行以下操作以將此令牌與Mogine Cloud DRM關聯，以便隨許可證請求一起發送：

實例化 `DRMManager` 對象，其中包含為Mighine Cloud DRM打包的內容的DRM元資料。

的 `setAuthenticationToken()` 方法通過將給定的位元組陣列與用於實例化的DRM元資料中提供的許可證伺服器URL關聯而工作 `DRMManager`。

```java
//client device acquires auth token needed by your BEES endpoint  
DRMManager mgr = new DRMManager(<DRM Metadata of CloudDRM content>);  
mgr.setAuthenticationToken(<auth token>);
```

令牌隨所有許可證請求一起發送，直到通過調用清除令牌 `.setAuthenticationToken` 參數為null。

## 許可證工作流詳細資訊{#license-workflow-details}

通過呼叫從Mogifle Cloud DRM請求許可證 `mgr.loadVoucher()`。

## 權利請求和響應詳細資訊{#entitlement-request-and-response-details}

當Mignishe Cloud DRM確定內容已與支援蜂類的DRM策略打包時，它構造以下JSON請求以發送到在DRM策略中指定的BEES端點：

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

應從BEES終結點得到以下響應：

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

黃金時段雲DRM使用響應來確定它是否應該向請求設備頒發許可證，以及它是否應該將新的DRM策略替換到許可證生成過程中。 如果 `isAllowed` 是 `true` 並且在響應中未提供策略，則在內容打包時間期間使用的原始DRM策略將用於生成許可證。
