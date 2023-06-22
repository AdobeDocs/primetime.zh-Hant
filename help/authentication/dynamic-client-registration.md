---
title: 動態使用者端註冊
description: 動態使用者端註冊
exl-id: 9bc2597d-b634-4542-849b-8e91a76cb8da
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 動態使用者端註冊 {#dynamic-client-registration}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 內容 {#context}

為符合現代安全性實務、改良UX和平台擁有者的要求，Adobe Primetime Authentication Android SDK和iOS SDK正朝著採用方向前進 [Android Chrome自訂標籤](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari view controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}.

目前的AdobePass實作使用平台特定的Web檢視，以提供顯示MVPD登入頁面的Web環境。 這些網頁檢視不會與平台瀏覽器共用認證管理，因此使用者在使用Adobe Primetime驗證應用程式時無法使用瀏覽器儲存的密碼。 此外，基於安全考量，有些平台正逐步淘汰WebView控制器以進行驗證工作。 Google和Apple都提供替代選項，例如「Chrome自訂標籤」和「Safari檢視控制器」。 這些基本上是其各自瀏覽器的單一使用標籤。 Adobe Primetime驗證將在2018年採用這些新元件。

## 詳細資料 {#details}

目前，Adobe Pass驗證識別及註冊應用程式的方式有兩種：

* 瀏覽器型使用者端會透過允許的網域清單進行註冊
* 原生應用程式使用者端(例如iOS和Android應用程式)會透過已簽署的請求者機制進行註冊

為了處理Chrome自訂標籤和Safari檢視控制器新的流程，Adobe Pass建議新的使用者端註冊機制來註冊新的應用程式。 此機制可讓您對應用程式進行更安全和精細的控制，並可用於在所有平台上註冊應用程式。

<!--
## Related Information

- [Dynamic Client Registration API](/help/authentication/dynamic-client-registration-api.md)
- [Dynamic Client Registration Management](/help/authentication/dynamic-client-registration-management.md)
-->
