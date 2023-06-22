---
title: 裝置群組網域註冊
description: 裝置群組網域註冊
copied-description: true
exl-id: 81d6023b-76e0-4786-805b-bfe77e9f8513
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# 裝置群組網域註冊{#device-group-domain-registration}

除了將授權繫結到特定裝置之外，Primetime DRM 3.0或更新版本也支援將授權繫結到裝置網域。

多個裝置可以加入網域並接收網域Token。 在網域中的裝置取得授權後，該授權可以傳輸到網域中的任何其他裝置，並且這些裝置可以在不直接從授權伺服器取得授權的情況下播放內容。

如果您想要支援任何網域繫結的授權，則Primetime DRM原則必須指定使用者端必須登入的網域伺服器。 不論是否啟用匿名存取，或伺服器是否需要使用者名稱/密碼或自訂驗證，Primetime DRM原則也必須指定網域伺服器的驗證需求。

Primetime DRM使用者端3.0版或更新版本支援網域註冊和網域繫結授權。 如果舊版使用者端或Flash Player中的Adobe Primetime 3.0使用者端請求支援網域註冊之內容的授權，授權伺服器可能會核發使用替代Primetime DRM原則的授權，以支援與特定裝置的繫結。
