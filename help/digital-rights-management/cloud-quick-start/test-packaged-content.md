---
title: 測試封裝內容
description: 測試封裝內容
copied-description: true
exl-id: 98456bf8-5d4d-47a7-905a-e6dac1e826ba
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# 測試封裝內容 {#test-the-packaged-content}

您應使用公開可用的Adobe Primetime Desktop Player (透過Flash Player)驗證封裝作業是否成功。 此播放器僅支援HDS內容。 為了測試HLS內容，需要啟用Primetime瀏覽器TVSDK的播放器。

1. 將您的內容託管在網頁伺服器上。
1. 在https://drmtest2.adobe.com:8080/AccessPlayer/player.html啟動Primetime DRM (先前稱為Adobe存取)播放器。
1. 將URL貼入您的HDS資訊清單( [!DNL .f4m])至播放器的導覽欄位，然後按一下 **[!UICONTROL Play]** 按鈕。
