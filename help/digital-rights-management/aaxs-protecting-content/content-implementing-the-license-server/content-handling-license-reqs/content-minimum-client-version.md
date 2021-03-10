---
title: 最低客戶端版本
description: 最低客戶端版本
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# 最低客戶端版本{#minimum-client-version}

AdobeAccess 2.0.2和更高版本引入了一些新的使用規則，AdobeAccess 2.0客戶端對這些規則不瞭解。 借由設定最低支援的用戶端版本(`HandlerConfiguration.setMinSupportedClientVersion()`)，授權伺服器可控制舊版用戶端在遇到具有這些使用規則的授權時的行為。 根據此設定，伺服器可以指出較舊的用戶端是否可忽略他們不瞭解的使用規則，或較舊的用戶端是否無法使用這些使用規則使用授權。

例如，

* 如果授權指定裝置功能需求（播放受保護內容所需的裝置功能[）,Adobe存取用戶端2.0.2及更高版本可強制執行這些需求。](../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-device-capabilities.md)
* 如果授權伺服器不希望內容在不瞭解裝置功能需求的用戶端上播放，請將支援的用戶端最低版本設定為2（針對2.0.2）。 這將阻止伺服器在2.0.2之前向Adobe訪問客戶端發放許可證。如果授權是從一個用戶端傳輸至另一個用戶端，則也會執行最低用戶端版本。
* 如果授權伺服器想要允許舊版用戶端忽略裝置功能需求，請將支援的最低用戶端版本設為1(對於Adobe存取2.0)。 伺服器會向任何2.0版及更新版本的用戶端發放授權。 如果用戶端升級或將授權轉讓給2.0.2版或更新版本的其他用戶端，授權中的裝置功能需求將會執行，因為用戶端現在會支援該使用規則。

