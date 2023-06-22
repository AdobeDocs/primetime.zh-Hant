---
title: Android 10應用程式上的Access Enabler Android SDK單一登入(SSO)
description: Android 10應用程式上的Access Enabler Android SDK單一登入(SSO)
exl-id: dedade15-c451-4757-b684-d3728e11dd87
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# Android 10應用程式上的Access Enabler Android SDK單一登入(SSO) {#access-enabler-android-sdk-single-sign-on-sso-on-android-10-apps}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 概觀

使用Android作業系統的裝置可透過Access Enabler Android SDK在Adobe Primetime驗證支援的應用程式之間使用單一登入(SSO)。 為了在Android裝置上提供單一登入(SSO)，Access Enabler Android SDK 3.2.1版（最新）和舊版使用共用資料庫檔案（儲存在Android儲存實施中），所有Adobe Primetime驗證支援的應用程式都可以存取。

不過，Google在最新的Android 10版本中做了一些變更，「讓使用者更能掌控其檔案，並限制檔案雜亂，針對Android 10 （API層級29）及更高版本的應用程式預設會獲得外部儲存裝置的設定範圍存取權，或設定範圍儲存裝置。 這類應用程式只能看見其應用程式專屬的目錄 `\[...\]`「。 有關這些Android 10儲存空間變更的更多詳細資訊，請參閱 [Android的資料和檔案儲存檔案](https://developer.android.com/training/data-storage/files/external-scoped).

由於這些變更，Access Enabler Android版本所提供的單一登入(SSO)功能 **3.2.1 SDK （最新）** 和舊版可能會在Android 10裝置上受到影響，如下節所述。

另請參閱 [Roku SSO概觀](/help/authentication/roku-sso-overview.md).

## 行為

根據您應用程式的 **目標SDK層級** 或使用方式 **android：requestLegacyExternalStorage** 資訊清單屬性Access Enabler Android 3.2.1 SDK （最新）版和舊版所提供的單一登入(SSO)目前行為如下：

- 您的應用程式目標 **Android 9 （API層級28）** 或以下 **-\>** 單一登入(SSO) **將有效**
- 您的應用程式目標 **Android 10** **（API層級29）** 和會 **set** 的值 **requestLegacyExternalStorage設為true** 在應用程式的資訊清單檔案中 **-\>** 單一登入(SSO) **將有效**
- 您的應用程式目標 **Android 10** **（API層級29）** 和會 **未設定** 的值 **requestLegacyExternalStorage設為true** 在應用程式的資訊清單檔案中 **-\>** 單一登入(SSO) **無法運作**


>[!TIP]
>
> 在Adobe Primetime Authentication Access Enabler Android SDK與適用範圍的儲存完全相容之前，您可以根據應用程式的目標SDK層級或requestLegacyExternalStorage資訊清單屬性（如公開內容所述），暫時選擇退出 [Android檔案](https://developer.android.com/training/data-storage/files/external-scoped#opt-out-of-scoped-storage).
