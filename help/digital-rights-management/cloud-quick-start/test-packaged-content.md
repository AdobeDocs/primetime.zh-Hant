---
seo-title: 測試封裝的內容
title: 測試封裝的內容
uuid: 99df417a-85ce-45da-bfcf-33df2197bf5b
translation-type: tm+mt
source-git-commit: b7f52b71bde1d7bf59ef51d4f6f90dfaa07e347b
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---


# 測試封裝內容{#test-the-packaged-content}

您應驗證封裝作業是否成功，方法是使用公開提供的Adobe Primetime Desktop Player（透過Flash Player）。 此播放器只能支援HDS內容。 為測試HLS內容，需要Primetime瀏覽器TVSDK播放器。

1. 將您的內容裝載在網頁伺服器上。
1. 在https://drmtest2.adobe.com:8080/AccessPlayer/player.html啟動Primetime DRM（先前稱為Adobe Access）播放器。
1. 將URL貼到您的HDS資訊清單([!DNL .f4m])至播放器的導覽欄位，然後按一下&#x200B;**[!UICONTROL Play]**&#x200B;按鈕。
