---
title: 裝置群組網域註冊
description: 裝置群組網域註冊
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# 裝置群組網域註冊{#device-group-domain-registration}

作為將授權繫結到特定裝置的替代方式，Primetime DRM 3.0或更新版本支援將授權繫結到裝置網域。

多個裝置可以加入網域並接收網域權杖。 在網域中的裝置取得授權後，該授權可以傳輸到網域中的任何其他裝置，並且這些裝置可以播放內容而不需要直接從授權伺服器取得授權。

如果您要支援任何網域繫結的授權，則Primetime DRM政策必須指定使用者端必須登入的網域伺服器。 不論是否啟用匿名存取，或伺服器是否需要使用者名稱/密碼或自訂驗證，Primetime DRM原則也必須指定網域伺服器的驗證需求。

Primetime DRM使用者端3.0或更新版本支援網域註冊和網域繫結授權。 如果Flash Player中的較舊使用者端或Adobe Primetime 3.0使用者端要求支援網域註冊之內容的授權，授權伺服器可能會核發使用替代Primetime DRM原則的授權，以支援與特定裝置的繫結。
