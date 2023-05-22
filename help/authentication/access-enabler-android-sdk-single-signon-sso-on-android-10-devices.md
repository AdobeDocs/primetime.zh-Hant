---
title: Access Enabler Android SDK Single Sign-On(SSO)，在Android 10應用上
description: Access Enabler Android SDK Single Sign-On(SSO)，在Android 10應用上
exl-id: dedade15-c451-4757-b684-d3728e11dd87
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# Access Enabler Android SDK Single Sign-On(SSO)，在Android 10應用上 {#access-enabler-android-sdk-single-sign-on-sso-on-android-10-apps}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 概述

在使用Android作業系統的設備上，可通過Access Enabler Android SDK在Adobe Primetime認證支援的應用之間使用單一登錄(SSO)。 為了在Android設備上提供單點登錄(SSO),Access Enabler Android SDK 3.2.1版（最新版）和早期版本使用共用資料庫檔案，該檔案保存在Android儲存實現中，所有Adobe Primetime認證支援的應用都可訪問。

但是，Google在最新版Android 10中做出了一些更改，「以讓用戶對檔案有更多控制，並限制檔案雜亂，預設情況下，針對Android 10（API級別29）及更高版本的應用允許範圍訪問外部儲存設備或範圍儲存。 此類應用只能查看其應用特定目錄 `\[...\]`。 有關這些Android 10儲存更改的更多詳細資訊，請參見 [用於Android的資料和檔案儲存文檔](https://developer.android.com/training/data-storage/files/external-scoped)。

由於這些更改，Access Enabler Android版本提供的單一登錄(SSO) **3.2.1 SDK（最新）** Android 10設備上的早期版本可能受到影響，如下一節所述。

請參閱 [Roku SSO概述](/help/authentication/roku-sso-overview.md)。

## 行為

取決於您的應用 **目標SDK級別** 或 **android:requestLegacyExternalStorage** manifest屬性Access Enabler Android 3.2.1版SDK（最新版）和早期版本提供的單一登錄(SSO)當前的行為如下：

- 你的應用目標 **Android 9（API級別28）** 或 **-\>** 單點登錄(SSO) **工作**
- 你的應用目標 **安卓10** **（API級別29）** 和 **集** 值 **requestLegacyExternalStorage為true** 在應用的清單檔案中 **-\>** 單點登錄(SSO) **工作**
- 你的應用目標 **安卓10** **（API級別29）** 和 **未設定** 值 **requestLegacyExternalStorage為true** 在應用的清單檔案中 **-\>** 單點登錄(SSO) **不能工作**


>[!TIP]
>
> 在Adobe Primetime驗證Access Enabler Android SDK與作用域儲存完全相容之前，您可以根據應用的目標SDK級別或requestLegacyExternalStorage清單屬性臨時選擇退出，如公共中所述 [Android文檔](https://developer.android.com/training/data-storage/files/external-scoped#opt-out-of-scoped-storage)。
