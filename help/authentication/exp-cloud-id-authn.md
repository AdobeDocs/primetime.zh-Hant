---
title: 在Primetime驗證中使用Experience CloudID
description: 在Primetime驗證中使用Experience CloudID
exl-id: 03354c01-5aad-4d81-beee-1c3834599134
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# 在Primetime驗證中使用Experience CloudID

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 什麼是Experience CloudID以及如何取得它？ {#what-exp-cloud-id-obtain}

Experience CloudID （簡稱ECID）是Adobe Experience Cloud為您的應用程式/網站中的每位使用者產生的唯一ID。 ECID在用於連結多個應用程式/網站中特定使用者資訊的所有Experience Cloud報表中大量使用。

如果您已有提供訪客ID的系統，則應針對本檔案的範圍使用相同的ID。

取得ECID的一種方式是使用Experience CloudID服務。 您可以根據TDM、JS程式庫、伺服器端、直接整合或行動平台的原生程式庫，使用您偏好的實作型別。 如需可用服務、程式庫、SDK和實作指南的完整檢視，請參閱： https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-implementation-guides.html





## 在Primetime驗證中使用Experience CloudID有何優點？ {#benefit-ex-cloud-id}

如果您設定我們的SDK和無使用者端REST API來使用您的ECID，您之後可以將Primetime驗證收集的資料連結至現有的Experience Cloud解決方案。 這可讓您更瞭解Adobe提供之所有解決方案的客戶歷程和體驗。

## 如何在Primetime驗證中使用Experience CloudID？ {#how-to-ex-cloud-id-authn}

取得ECID （以上說明）後，您需要將此資訊傳遞至我們的SDK和無使用者端REST API。 此資訊稍後會在SDK發出的每個網路呼叫中傳遞至我們的伺服器。 每個SDK的設定程式不同，如下所示：

### JS SDK {#js-sdk}

若是JavaScript，您必須在對應中將ECID傳遞為setRequestor呼叫的第三個引數。

**使用範例：**

```JavaScript
accessEnabler.setRequestor("REQUESTOR_ID", ["ENDPOINT_URL"],
    {
        "visitorID": "THE_ECID_VALUE"
    }
);
```

### iOS/tvOS SDK {#ios-sdk}

iOS/tvOS SDK有一個專用方法，稱為setOptions。

**使用範例：**

```JavaScript
accessEnabler.setOptions(
    [
        "visitorID": "THE_ECID_VALUE"
    ]
);
```

### Android/fireTV SDK {#android-sdk}

Android/fireTV SDK的機制類似於iOS。 只有引數名稱不同。 此API已記錄在此處。

**使用範例：**

```JavaScript
String visitor_id = "THE_ECID_VALUE";

HashMap<String, String> options = new HashMap();
options.put("ap_vi",visitor_id);

accessEnabler.setOptions(options);
```

### 無使用者端API {#clientless-api}

透過REST API使用Adobe Primetime時， **ECID** 值應傳送 **在所有API上** 作為引數，名為 **&#39;ap_vi&#39;**.

**使用範例：**

`GET: https://api.auth.adobe.com/api/v1/authorize?...&ap_vi=THE_ECID_VALUE`
