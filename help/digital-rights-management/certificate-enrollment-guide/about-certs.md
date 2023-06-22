---
title: 關於憑證
description: 關於憑證
copied-description: true
exl-id: 24ca19bb-a71e-461a-9c3c-558d650e2d99
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 關於憑證 {#about-certificates}

Adobe Primetime DRM SDK提供下列設定：

* Primetime DRM Production SDK
* Primetime DRM評估SDK
* Primetime DRM試用版SDK

若要使用Primetime DRM SDK建立授權伺服器，您必須從Adobe取得數位憑證。 數位憑證（也簡稱為憑證）會將實體（例如個人、組織或系統）與特定的公開和私密金鑰組繫結。 數位憑證可視為驗證個人、系統或組織身分的電子憑證。

為了讓您在部署選項中擁有最大的彈性和增強的安全性，Primetime DRM SDK需要四個憑證：

* 授權伺服器憑證

   SDK會使用此憑證來簽署核發給使用者端的內容授權。
* Packager憑證

   封裝（加密）內容時，SDK會使用此憑證來產生DRM中繼資料。
* 傳輸憑證

   SDK會使用此憑證來保護使用者端與授權伺服器之間的通訊。
* 網域CA憑證

   想要實作網域伺服器的客戶需要網域CA憑證。 與其他憑證不同，網域CA憑證不是由Adobe發行。

>[!NOTE]
>
>對於Evaluation SDK和試用版SDK，授權伺服器、封裝程式和傳輸憑證會合併為單一憑證。
