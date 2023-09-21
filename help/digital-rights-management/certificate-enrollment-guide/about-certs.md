---
title: 關於憑證
description: 關於憑證
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 關於憑證 {#about-certificates}

Adobe Primetime DRM SDK提供下列設定：

* Primetime DRM Production SDK
* Primetime DRM評估SDK
* Primetime DRM試用版SDK

若要使用Primetime DRM SDK建立授權伺服器，您必須從Adobe取得數位憑證。 數位憑證（也簡稱為憑證）會將實體（例如個人、組織或系統）與特定的公開和私密金鑰組繫結。 數位憑證可以視為驗證個人、系統或組織身分的電子憑證。

為了在部署選項中實現最大彈性和增強安全性，Primetime DRM SDK需要四個憑證：

* 授權伺服器憑證

  SDK會使用此憑證來簽署核發給使用者端的內容授權。
* 封裝程式憑證

  封裝（加密）內容時，SDK會使用此憑證來產生DRM中繼資料。
* 傳輸憑證

  SDK會使用此憑證來保護使用者端與授權伺服器之間的通訊。
* 網域CA憑證

  想要實作網域伺服器的客戶需要網域CA憑證。 與其他憑證不同，網域CA憑證不是由Adobe所簽發。

>[!NOTE]
>
>對於Evaluation SDK和Trial SDK，授權伺服器、封裝程式和傳輸憑證會合併為單一憑證。
