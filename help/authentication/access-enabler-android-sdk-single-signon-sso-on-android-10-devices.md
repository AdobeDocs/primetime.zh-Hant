---
title: 在Android 10應用程式上存取啟用碼Android SDK單一登入(SSO)
description: 在Android 10應用程式上存取啟用碼Android SDK單一登入(SSO)
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---



# 在Android 10應用程式上存取啟用碼Android SDK單一登入(SSO) {#access-enabler-android-sdk-single-sign-on-sso-on-android-10-apps}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 概述

Adobe Primetime驗證支援應用程式之間的單一登入(SSO)可在使用Android OS的裝置上透過Access Enabler Android SDK取得。 為了在Android裝置上提供單一登入(SSO),Access Enabler Android SDK 3.2.1版（最新）和舊版使用儲存在Android儲存實作中的共用資料庫檔案，所有Adobe Primetime驗證支援的應用程式皆可存取。

不過，Google在最新的Android 10版本中產生了一些變更，「讓使用者能更多控制其檔案，並限制檔案凌亂，鎖定Android 10（API層級29）及以上版本的應用程式，依預設會獲得外部儲存裝置或範圍儲存的範圍存取權。 此類應用只能查看其應用特定目錄 `\[...\]`」。 如需與這些Android 10儲存變更相關的詳細資訊，請參閱 [Android的資料和檔案儲存檔案](https://developer.android.com/training/data-storage/files/external-scoped).

由於這些更改，Access Enabler Android版本提供的單一登錄(SSO) **3.2.1 SDK（最新）** 和舊版可能會在Android 10裝置上受到影響，如下一節所述。

請參閱 [Roku SSO概述](/help/authentication/roku-sso-overview.md).

## 行為

視您應用程式的 **target SDK層級** 或 **android:requestLegacyExternalStorage** manifest屬性Access Enabler Android 3.2.1 SDK（最新）版和舊版提供的單一登入(SSO)目前的行為如下：

- 您的應用程式目標 **Android 9（API層級28）** 或更低 **-\>** 單一登入(SSO) **會運作**
- 您的應用程式目標 **Android 10** **（API第29層）** 和 **set** 值 **requestLegacyExternalStorage設為true** 在應用程式的資訊清單檔案中 **-\>** 單一登入(SSO) **會運作**
- 您的應用程式目標 **Android 10** **（API第29層）** 和 **未設定** 值 **requestLegacyExternalStorage設為true** 在應用程式的資訊清單檔案中 **-\>** 單一登入(SSO) **將無法運作**


>[!TIP]
>
> 在Adobe Primetime驗證Access Enabler Android SDK與範圍儲存完全相容之前，您可以暫時根據應用程式的目標SDK層級或requestLegacyExternalStorage資訊清單屬性選擇退出，如公開所述 [Android檔案](https://developer.android.com/training/data-storage/files/external-scoped#opt-out-of-scoped-storage).

