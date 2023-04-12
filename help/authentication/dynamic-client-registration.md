---
title: 動態客戶端註冊
description: 動態客戶端註冊
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# 動態客戶端註冊 {#dynamic-client-registration}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 內容 {#context}

為符合現代安全性實務、改善的UX和平台擁有者需求，Adobe Primetime Authentication Android SDK和iOS SDK正朝著採用的方向邁進 [Android Chrome自訂分頁](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari view controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}.

目前的AdobePass實作使用平台特定的Web檢視，以提供顯示MVPD登入頁面的Web環境。 這些Web檢視不會與平台瀏覽器共用憑證管理，因此使用Adobe Primetime驗證應用程式時，使用者無法使用瀏覽器儲存的密碼。 此外，出於安全原因，一些平台正在為驗證任務淘汰WebView控制器。 Google和Apple都提供替代選項，例如「Chrome自訂分頁」和「Safari檢視控制器」。 這些基本上是各自瀏覽器的單一使用標籤。 Adobe Primetime驗證將於2018年採用這些新元件。

## 詳細資料 {#details}

目前，Adobe Pass Authentication有兩種方式來識別和註冊應用程式：

* 瀏覽器型用戶端可透過允許的網域清單註冊
* 原生應用程式用戶端(例如iOS和Android應用程式)是透過簽署的請求者機制來註冊

為了處理Chrome自訂分頁與Safari檢視控制器的新流程，Adobe Pass提出新的用戶端註冊機制，用於註冊新的應用程式。 此機制將允許對您的應用程式進行更安全、更精細的控制，並可用於在所有平台上註冊應用程式。

<!--
## Related Information

- [Dynamic Client Registration API](/help/authentication/dynamic-client-registration-api.md)
- [Dynamic Client Registration Management](/help/authentication/dynamic-client-registration-management.md)
-->