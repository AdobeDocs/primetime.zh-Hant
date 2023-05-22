---
description: Adobe PrimetimeDRM是用於高價值視聽內容的高級Digital Rights Management(DRM)和內容保護解決方案。 在支援建立Java API的應用程式中，您可以使用Mighine DRM SDK指定DRM策略，將這些策略應用於內容，並加密該內容。
title: Adobe PrimetimeDRM有什麼新聞嗎
exl-id: 998dae80-b3d3-419e-8fd3-d925a83d8b53
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Adobe PrimetimeDRM有什麼新聞嗎{#what-is-new-in-adobe-primetime-drm}

Adobe PrimetimeDRM是用於高價值視聽內容的高級Digital Rights Management(DRM)和內容保護解決方案。 在支援建立Java API的應用程式中，您可以使用Mighine DRM SDK指定DRM策略，將這些策略應用於內容，並加密該內容。

>[!NOTE]
>
>黃金時段DRM以前稱為Adobe訪問，在此之前稱為Flash Access。

下面是內容保護過程的高級介紹：

1. 使用DRM Java API設定DRM策略屬性和加密參數。
1. 建立描述任何內容的使用角色的DRM策略。

   可以建立任意數量的DRM策略。 大多數用戶會建立少量策略，然後將它們應用到許多檔案。
1. 打包媒體檔案。

   *`Packaging a file`* 表示您加密檔案，然後對檔案應用DRM策略。
1. 實施許可證伺服器以向用戶頒發許可證。

完成這些步驟後，您的加密內容就可以部署了。 在部署之後，客戶端可以從許可證伺服器請求許可證，並且在接收後可以播放內容。

黃金時段DRM SDK提供Java API來完成這些任務。 該SDK包括許可證伺服器和命令行工具的參考實現，兩者都基於DRM SDK Java API。

下面介紹的功能是此版本中的新增功能。

## 新功能 {#section_F6BA874CEAE24610920BC3A4C6D20EBA}

* **硬站 —** 可以指定回放是在回放窗口結束時停止還是繼續。
* **與解析度相關的輸出控制項 —** 可以根據像素解析度指定輸出約束。
* **許可證伺服器響應的匿名化 —** 為了利用黃金時段DRM許可證伺服器協定增強隱私，傳輸證書序列號將被零，以用於許可證伺服器對支援客戶端的響應。
