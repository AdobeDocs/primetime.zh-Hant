---
description: Adobe Primetime DRM是適用於高價值視聽內容的進階Digital Rights Management(DRM)和內容保護解決方案。 在支援建立Java API的應用程式中，您可以使用Primetime DRM SDK來指定DRM原則、將這些原則套用至內容，以及加密該內容。
title: Adobe Primetime DRM的新功能
exl-id: 998dae80-b3d3-419e-8fd3-d925a83d8b53
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Adobe Primetime DRM的新功能{#what-is-new-in-adobe-primetime-drm}

Adobe Primetime DRM是適用於高價值視聽內容的進階Digital Rights Management(DRM)和內容保護解決方案。 在支援建立Java API的應用程式中，您可以使用Primetime DRM SDK來指定DRM原則、將這些原則套用至內容，以及加密該內容。

>[!NOTE]
>
>Primetime DRM以前稱為Adobe存取，之前稱為Flash Access。

以下是內容保護程式的高層級逐步解說：

1. 使用DRM Java API來設定DRM原則屬性和加密引數。
1. 建立說明任何內容之使用角色的DRM原則。

   您可以建立任意數量的DRM原則。 大部分的使用者會建立少量原則，然後將其套用至許多檔案。
1. 封裝媒體檔案。

   *`Packaging a file`* 表示您先加密檔案，然後將DRM原則套用至檔案。
1. 實作授權伺服器以核發授權給使用者。

完成這些步驟後，您的加密內容就可供部署。 部署後，使用者端可向授權伺服器要求授權，並在收到授權後播放內容。

Primetime DRM SDK提供Java API來完成這些工作。 SDK包含許可證伺服器和命令列工具的參考實作，兩者都以DRM SDK Java API為基礎。

以下說明的功能是此版本中的新增功能。

## 新功能 {#section_F6BA874CEAE24610920BC3A4C6D20EBA}

* **硬式停止 —** 您可以指定在播放視窗結束時是否停止或繼續播放。
* **解析度相依的輸出控制項 —** 您可以根據畫素解析度來指定輸出限制。
* **授權伺服器回應的匿名化 —** 為了使用Primetime DRM授權伺服器通訊協定來增強隱私權，傳輸憑證序號將會歸零，以取得對支援使用者端的授權伺服器回應。
