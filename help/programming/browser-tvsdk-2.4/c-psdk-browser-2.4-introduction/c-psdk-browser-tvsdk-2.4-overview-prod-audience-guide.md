---
description: 本指南提供如何使用瀏覽器TVSDK開發視訊播放器應用程式的相關資訊。
title: 產品概觀與受眾
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# 產品概觀與觀眾{#product-overview-and-audience}

本指南提供如何使用瀏覽器TVSDK開發視訊播放器應用程式的相關資訊。

## 產品概觀{#section_1C66E736CEFD4246B7C7C99AADD48118}

Adobe Primetime軟體開發套件(Browser TVSDK)是一套工具套件，可讓您在瀏覽器型視訊播放應用程式中加入進階的視訊播放功能、內容保護和廣告。 瀏覽器TVSDK提供JavaScript API來建立以瀏覽器為基礎的視訊應用程式，並包含下列模式的播放支援：

* 僅限HTML5
* HTML5含自動flash備援
* Flash永遠

此版本包含瀏覽器TVSDK API和範例參考實作。

### UI架構

為協助加速瀏覽器適用之JavaScript視訊播放器應用程式的UI開發，瀏覽器TVSDK包含UI架構，其中包含API以：

* 包含預設UI控制項，例如播放／暫停、音量等
* 輕鬆新增（或移除）進階的播放UI控制項，而不需直接控制DOM結構
* 輕鬆設定相關UI控制項的行為
* 建立自訂UI控制項
* 根據需求設定播放器UI的外觀

如需UI架構API的詳細資訊，請參閱[瀏覽器TVSDK 2.4的UI架構](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/index.html)。

## 對象{#section_DFC9DECC2E30426DBBDDEA4E288E666C}

本指南假設您瞭解如何使用JavaScript開發應用程式和視訊播放器。 您可以實作視訊播放器並整合瀏覽器TVSDK功能。