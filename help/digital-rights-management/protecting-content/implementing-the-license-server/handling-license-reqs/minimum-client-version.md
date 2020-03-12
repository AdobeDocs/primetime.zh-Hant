---
seo-title: 最低用戶端版本
title: 最低用戶端版本
uuid: f2b56cff-96fa-4954-a08a-9b3e78f496d6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 最低用戶端版本 {#minimum-client-version}

Adobe Primetime DRM 2.0.2及更新版本推出一些Primetime DRM 2.0用戶端不瞭解的新使用規則。 借由設定最低支援的用戶端版本( `HandlerConfiguration.setMinSupportedClientVersion()`)，授權伺服器可控制舊版用戶端在遇到具有這些使用規則的授權時的行為。 根據此設定，伺服器可以指出較舊的用戶端是否可忽略他們不瞭解的使用規則，或較舊的用戶端是否無法使用這些使用規則使用授權。

例如，

* 如果授權指定裝置功能需求(播放受保護內容所需的 [裝置功能](../../../protecting-content/introduction/usage-rules/runtime-application-restrictions/device-capabilities.md)),Primetime DRM用戶端2.0.2及更高版本可強制執行這些需求。
* 如果授權伺服器不希望內容在不瞭解裝置功能需求的用戶端上播放，請將支援的用戶端最低版本設定為2（針對2.0.2）。 這將阻止伺服器在2.0.2之前向Primetime DRM客戶端發放許可證。如果授權是從一個用戶端傳輸至另一個用戶端，則也會強制執行最低用戶端版本。
* 如果授權伺服器想要允許舊版用戶端忽略裝置功能需求，請將最低支援的用戶端版本設為1（適用於Primetime DRM 2.0）。 然後，伺服器會向任何2.0版及更新版本的用戶端發出授權。 如果用戶端升級或將授權轉讓給版本為2.0.2或更新版本的其他用戶端，則會強制執行授權中的裝置功能要求，因為用戶端可以支援該使用規則。

