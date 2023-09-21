---
title: 裝置群組網域註冊
description: 裝置群組網域註冊
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# 裝置群組網域註冊{#device-group-domain-registration}

除了將授權繫結至特定裝置之外，Adobe存取3.0和更新版本也支援將授權繫結至裝置網域。 多個裝置可以加入網域並接收網域權杖。 在網域中的裝置取得授權後，該授權可以傳輸到網域中的任何其他裝置，並且這些裝置可以播放內容而不需要直接從授權伺服器取得授權。

若要支援網域繫結的授權，原則必須指定使用者端必須登入的網域伺服器。 原則也會指定網域伺服器的驗證需求（是否允許匿名存取，或伺服器是否需要使用者名稱/密碼或自訂驗證）。

Adobe Access使用者端3.0和更新版本支援網域註冊和網域繫結授權。 如果Flash Player中的較舊使用者端或Adobe Access 3.0使用者端要求支援網域註冊之內容的授權，授權伺服器可能會使用支援繫結至特定裝置的替代原則來發行授權。
