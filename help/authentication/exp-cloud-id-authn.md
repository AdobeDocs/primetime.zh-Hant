---
title: 在Primetime驗證中使用Experience CloudID
description: 在Primetime驗證中使用Experience CloudID
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---


# 在Primetime驗證中使用Experience CloudID

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 什麼是Experience CloudID以及如何取得？ {#what-exp-cloud-id-obtain}

Experience CloudID（簡稱ECID）是Adobe Experience Cloud針對您應用程式/網站中每位個別使用者產生的唯一ID。 ECID在所有Experience Cloud報表中都大量使用，這些報表用來連結多個應用程式/網站中特定使用者的相關資訊。

如果您已有提供訪客ID的系統，則應在本檔案的範圍內使用相同的ID。

取得ECID的其中一種方式是使用Experience CloudID服務。 您可以根據TDM、JS程式庫、伺服器端、直接整合或適用於行動平台的原生程式庫，使用您偏好的實作類型。 如需可用服務、程式庫、SDK和實作指南的完整檢視，請參閱：https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-implementation-guides.html





## 在Primetime驗證中使用Experience CloudID有何好處？ {#benefit-ex-cloud-id}

如果您設定我們的SDK和無用戶端REST API以使用您的ECID，您稍後將能將Primetime驗證所收集的資料連結至您現有的Experience Cloud解決方案。 這可讓您更清楚了解客戶歷程，以及Adobe提供的所有解決方案。

## 如何在Primetime驗證中使用Experience CloudID? {#how-to-ex-cloud-id-authn}

取得ECID（如上所述）後，您就必須將此資訊傳遞至我們的SDK和無用戶端REST API。 這些資訊稍後會在SDK進行的每次網路呼叫上傳遞至我們的伺服器。 每個SDK的設定程式都不同，如下所示：

### JS SDK {#js-sdk}

若是JavaScript，您必須將ECID傳入對映中，作為第三個參數傳遞至setRequestor呼叫。

**用法範例：**

```JavaScript
accessEnabler.setRequestor("REQUESTOR_ID", ["ENDPOINT_URL"],
    {
        "visitorID": "THE_ECID_VALUE"
    }
);
```

### iOS/tvOS SDK {#ios-sdk}

若為iOS/tvOS SDK，則有一種名為setOptions的專用方法。

**用法範例：**

```JavaScript
accessEnabler.setOptions(
    [
        "visitorID": "THE_ECID_VALUE"
    ]
);
```

### Android/fireTV SDK {#android-sdk}

Android/fireTV SDK的機制類似於iOS。 只是參數名稱不同。 此處記錄API。

**用法範例：**

```JavaScript
String visitor_id = "THE_ECID_VALUE";

HashMap<String, String> options = new HashMap();
options.put("ap_vi",visitor_id);

accessEnabler.setOptions(options);
```

### 無用戶端API {#clientless-api}

透過REST API使用Adobe Primetime時， **ECID** 值應傳送 **在所有API上** 作為參數，名為 **&#39;ap_vi&#39;**.

**用法範例：**

`GET: https://api.auth.adobe.com/api/v1/authorize?...&ap_vi=THE_ECID_VALUE`