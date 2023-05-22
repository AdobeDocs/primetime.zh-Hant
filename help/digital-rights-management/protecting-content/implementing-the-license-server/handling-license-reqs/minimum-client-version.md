---
title: 最低客戶端版本
description: 最低客戶端版本
copied-description: true
exl-id: c4aebafe-33b4-4da3-9e79-53d6a7e9f22d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# 最低客戶端版本 {#minimum-client-version}

Adobe PrimetimeDRM 2.0.2及更高版本引入了一些Mighide DRM 2.0客戶端所不瞭解的新使用規則。 通過設定最低支援的客戶端版本( `HandlerConfiguration.setMinSupportedClientVersion()`)，許可證伺服器可以控制當舊客戶端遇到使用這些使用規則的許可證時其行為。 基於此設定，伺服器可以指示較舊客戶端是否可以忽略他們不瞭解的使用規則，或者較舊客戶端是否無法使用這些使用規則使用許可證。

比如說，

* 如果許可證指定了設備功能要求( [播放受保護內容所需的設備功能](../../../protecting-content/introduction/usage-rules/runtime-application-restrictions/device-capabilities.md))，黃金時段DRM客戶端2.0.2及更高版本可以執行這些要求。
* 如果許可證伺服器不希望內容在不瞭解設備功能要求的客戶端上播放，請將支援的最低客戶端版本設定為2(對於2.0.2)。 這將阻止伺服器在2.0.2之前向Mogine DRM客戶端發放許可證。如果許可證從一個客戶端傳輸到另一個客戶端，則還強制實施最低客戶端版本。
* 如果許可證伺服器希望允許較舊的客戶端忽略設備功能要求，請將支援的最低客戶端版本設定為1（對於Mighine DRM 2.0）。 然後，伺服器向任何客戶端版本2.0及更高版本發放許可證。 如果客戶端升級或將許可證傳輸到版本為2.0.2或更高版本的另一台客戶端，則會強制執行許可證中的設備功能要求，因為客戶端隨後可以支援該使用規則。
