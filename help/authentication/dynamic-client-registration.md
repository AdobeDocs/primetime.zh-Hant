---
title: 動態客戶端註冊
description: 動態客戶端註冊
exl-id: 9bc2597d-b634-4542-849b-8e91a76cb8da
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 動態客戶端註冊 {#dynamic-client-registration}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 上下文 {#context}

為了與現代安全實踐、改進的UX和平台所有者要求保持一致，Adobe PrimetimeAuthentication Android SDK和iOSSDK正在朝採用的方向發展 [Android Chrome自定義頁籤](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari view controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}。

當前的AdobePass實現使用平台特定的Web視圖，以便提供用於顯示MVPD登錄頁的Web環境。 這些Web視圖不與平台瀏覽器共用憑據管理，因此用戶在使用Adobe Primetime身份驗證應用程式時無法使用瀏覽器保存的密碼。 此外，出於安全原因，一些平台正在為驗證任務棄用WebView控制器。 Google和Apple都提供了「Chrome自定義頁籤」和「Safari View Controller」等備用選項。 這些基本上是其各自瀏覽器的單一使用頁籤。 Adobe Primetime認證將在2018年採用這些新元件。

## 詳細資訊 {#details}

目前，有兩種方法可通過Adobe Pass身份驗證來識別和註冊應用程式：

* 通過允許的域清單註冊基於瀏覽器的客戶端
* 本地應用程式客戶端(如iOS和Android應用程式)通過簽名請求者機制註冊

為瞭解決Chrome自定義頁籤和Safari視圖控制器的新流，Adobe Pass提出了新的客戶註冊機制來註冊新的應用程式。 此機制將允許對應用程式進行更安全、更細緻的控制，並可用於在所有平台上註冊應用程式。

<!--
## Related Information

- [Dynamic Client Registration API](/help/authentication/dynamic-client-registration-api.md)
- [Dynamic Client Registration Management](/help/authentication/dynamic-client-registration-management.md)
-->
