---
title: 測試封裝的內容
description: 測試封裝的內容
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---


# 測試封裝內容{#test-the-packaged-content}

您應驗證封裝作業是否成功，方法是使用公開提供的Adobe Primetime案頭播放器(透過Flash Player)。 此播放器只能支援HDS內容。 為測試HLS內容，需要Primetime瀏覽器TVSDK播放器。

1. 將您的內容裝載在網頁伺服器上。
1. 在https://drmtest2.adobe.com:8080/AccessPlayer/player.html啟動Primetime DRM(先前稱為Adobe存取)播放器。
1. 將URL貼到您的HDS資訊清單([!DNL .f4m])至播放器的導覽欄位，然後按一下&#x200B;**[!UICONTROL Play]**&#x200B;按鈕。
