---
title: 在黃金時段Experience Cloud中使用身份驗證ID
description: 在黃金時段Experience Cloud中使用身份驗證ID
exl-id: 03354c01-5aad-4d81-beee-1c3834599134
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# 在黃金時段Experience Cloud中使用身份驗證ID

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 什麼是Experience CloudID以及如何獲取它？ {#what-exp-cloud-id-obtain}

Experience CloudID（簡稱ECID）是Adobe Experience Cloud為應用程式/網站中的每個用戶生成的唯一ID。 ECID被大量用於所有Experience Cloud報告，這些報告用於將多個應用程式/網站中特定用戶的資訊連結在一起。

如果您已部署了提供訪問者ID的系統，則應將相同ID用於此文檔的範圍。

獲取ECID的一種方法是使用Experience CloudID服務。 您可以基於TDM、JS庫、伺服器端、直接整合或移動平台的本機庫，使用您的首選實現類型。 有關可用服務、庫、SDK和實施指南的全面視圖，請參閱：https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-implementation-guides.html





## 在黃金時段Experience Cloud中使用ID有何好處？ {#benefit-ex-cloud-id}

如果您將我們的SDK和無客戶端REST API配置為使用您的ECID，則您以後將能夠將Moginiqe Authentication收集的資料連結到您現有的Experience Cloud解決方案。 這將使您能夠更好地瞭解您的客戶的旅程和體驗，以及Adobe提供的所有解決方案。

## 如何在黃金時段Experience Cloud中使用ID? {#how-to-ex-cloud-id-authn}

獲取ECID（如上所述）後，您需要將此資訊傳遞給我們的SDK和我們的無客戶端REST API。 此資訊稍後將在SDK進行的每次網路呼叫中傳遞給我們的伺服器。 每個SDK的配置過程不同，如下所示：

### JS SDK {#js-sdk}

對於JavaScript，您需要將映射中的ECID作為第三個參數傳遞給setRequestor調用。

**用法示例：**

```JavaScript
accessEnabler.setRequestor("REQUESTOR_ID", ["ENDPOINT_URL"],
    {
        "visitorID": "THE_ECID_VALUE"
    }
);
```

### iOS/電視作業系統SDK {#ios-sdk}

對於iOS/tvOS SDK，有一種名為setOptions的專用方法。

**用法示例：**

```JavaScript
accessEnabler.setOptions(
    [
        "visitorID": "THE_ECID_VALUE"
    ]
);
```

### Android/fireTV SDK {#android-sdk}

對於Android/fireTV SDK，該機制與iOS類似。 只是參數名稱不同。 此處記錄了API。

**用法示例：**

```JavaScript
String visitor_id = "THE_ECID_VALUE";

HashMap<String, String> options = new HashMap();
options.put("ap_vi",visitor_id);

accessEnabler.setOptions(options);
```

### 無客戶端API {#clientless-api}

當通過REST API使用Adobe Primetime時， **ECID** 應發送值 **在所有API上** 作為名為 **「ap_vi」**。

**用法示例：**

`GET: https://api.auth.adobe.com/api/v1/authorize?...&ap_vi=THE_ECID_VALUE`
