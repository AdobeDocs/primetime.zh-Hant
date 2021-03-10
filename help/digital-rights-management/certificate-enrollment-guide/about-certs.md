---
title: 關於證書
description: 關於證書
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# 關於證書{#about-certificates}

Adobe PrimetimeDRM SDK提供下列組態：

* Primetime DRM Production SDK
* Primetime DRM評估SDK
* Primetime DRM試用版SDK

若要使用Primetime DRM SDK建立授權伺服器，您必須從Adobe取得數位憑證。 數位憑證（也稱為憑證）會將實體（例如個人、組織或系統）系結至特定的公開和私密金鑰對。 數位憑證可視為驗證個人、系統或組織身分的電子憑證。

為了在部署選項中提供最大的彈性和增強的安全性，Primetime DRM SDK需要4個憑證：

* 授權伺服器憑證

   SDK會使用此憑證來簽署發給客戶的內容授權。
* Packager憑證

   SDK在封裝（加密）內容時，會使用此憑證來產生DRM中繼資料。
* 傳輸憑證

   SDK會使用此憑證來保護用戶端與授權伺服器之間的通訊安全。
* 域CA證書

   想要實作網域伺服器的客戶需要網域CA憑證。 與其他證書不同，域CA證書不由Adobe頒發。

>[!NOTE]
>
>對於試用版SDK和試用版SDK，授權伺服器、封裝工具和傳輸憑證會結合為單一憑證。

