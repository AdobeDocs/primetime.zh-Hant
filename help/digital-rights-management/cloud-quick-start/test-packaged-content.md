---
title: Test打包的內容
description: Test打包的內容
copied-description: true
exl-id: 98456bf8-5d4d-47a7-905a-e6dac1e826ba
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Test打包的內容 {#test-the-packaged-content}

您應通過使用公開可用的Adobe Primetime案頭播放器(通過Flash Player)驗證打包操作是否成功。 此播放器只能支援HDS內容。 為了testHLS內容，需要啟用Mogki時瀏覽器TVSDK的播放器。

1. 在Web伺服器上承載您的內容。
1. 在https://drmtest2.adobe.com:8080/AccessPlayer/player.html上啟動Mighine DRM(以前稱為Adobe訪問)播放器。
1. 將URL貼上到HDS清單( [!DNL .f4m])並按一下 **[!UICONTROL Play]** 按鈕
