---
title: 最低使用者端版本
description: 最低使用者端版本
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# 最低使用者端版本 {#minimum-client-version}

Adobe Primetime DRM 2.0.2和更新版本引進了一些新的使用規則，Primetime DRM 2.0使用者端不瞭解這些規則。 透過設定最低支援的使用者端版本( `HandlerConfiguration.setMinSupportedClientVersion()`)，則舊版使用者端遇到具有這些使用規則的授權時，授權伺服器可控制舊版使用者端的行為。 根據此設定，伺服器可指出較舊的使用者端是否可以忽略他們不瞭解的使用規則，或較舊的使用者端是否無法使用這些使用規則的授權。

例如，

* 如果授權指定裝置功能需求( [播放受保護內容所需的裝置功能](../../../protecting-content/introduction/usage-rules/runtime-application-restrictions/device-capabilities.md))、Primetime DRM使用者端2.0.2和更新版本可強制執行這些要求。
* 如果授權伺服器不想讓內容在不瞭解裝置功能需求的使用者端上播放，請將最低支援的使用者端版本設定為2 （適用於2.0.2）。 這會防止伺服器在2.0.2之前核發授權給Primetime DRM使用者端。如果許可證從一個使用者端傳輸到另一個使用者端，也會強制執行最低使用者端版本。
* 如果授權伺服器想要允許較舊的使用者端忽略裝置功能需求，請將支援的使用者端版本下限設定為1 （適用於Primetime DRM 2.0）。 然後，伺服器會向任何使用者端2.0版及更高版本發行授權。 如果使用者端將授權升級或傳輸到另一個具有2.0.2版或更新版本的使用者端，則強制實施授權中的裝置功能要求，因為使用者端之後可以支援該使用規則。
