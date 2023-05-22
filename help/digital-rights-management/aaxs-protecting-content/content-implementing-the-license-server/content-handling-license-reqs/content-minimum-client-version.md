---
title: 最低客戶端版本
description: 最低客戶端版本
copied-description: true
exl-id: ba311d33-f3dd-42c5-ac66-7ad665d1bd20
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# 最低客戶端版本 {#minimum-client-version}

AdobeAccess 2.0.2和更高版本引入了一些AdobeAccess 2.0客戶端無法理解的新用法規則。 通過設定最低支援的客戶端版本( `HandlerConfiguration.setMinSupportedClientVersion()`)，許可證伺服器可以控制當舊客戶端遇到使用這些使用規則的許可證時其行為。 基於此設定，伺服器可以指示較舊客戶端是否可以忽略他們不瞭解的使用規則，或者較舊客戶端是否無法使用這些使用規則使用許可證。

比如說，

* 如果許可證指定了設備功能要求( [播放受保護內容所需的設備功能](../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-device-capabilities.md)),Adobe訪問客戶端2.0.2和更高版本可以強制執行這些要求。
* 如果許可證伺服器不希望內容在不瞭解設備功能要求的客戶端上播放，請將支援的最低客戶端版本設定為2(對於2.0.2)。 這將阻止伺服器在2.0.2之前向Adobe訪問客戶端頒發許可證。如果許可證從一個客戶端傳輸到另一個客戶端，則還將強制執行最低客戶端版本。
* 如果許可證伺服器希望允許較舊的客戶端忽略設備功能要求，請將支援的最低客戶端版本設定為1(對於Adobe訪問2.0)。 伺服器將向任何客戶端版本2.0及更高版本頒發許可證。 如果客戶端升級或將許可證傳輸到版本為2.0.2或更高版本的另一台客戶端，則將強制執行許可證中的設備功能要求，因為客戶端現在將支援該使用規則。
