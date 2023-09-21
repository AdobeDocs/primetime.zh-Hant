---
description: Adobe Primetime DRM的任何使用都包含工作流程中不同點的兩個關鍵步驟。 每個資產必須完成一次內容準備，然後才能建立受保護的內容。 想要觀看該受保護資產的每個消費者都會多次進行內容擷取，一次完成。
title: 內容準備
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 內容準備{#content-preparation}

Adobe Primetime DRM的任何使用都包含工作流程中不同點的兩個關鍵步驟。 每個資產必須完成一次內容準備，然後才能建立受保護的內容。 想要觀看該受保護資產的每個消費者都會多次進行內容擷取，一次完成。

在讓內容可供發佈之前，您必須先以視訊格式編碼內容、建立一或多個指定內容使用規則的原則，並使用Adobe Primetime DRM SDK封裝內容。

編碼、封裝和發佈內容的步驟如下：

1. 使用Adobe或第三方提供的編碼工具，以您所需的視訊格式編碼內容。
1. 建立原則，指定消費者可檢視內容的使用規則。

   原則是規則和限制的容器，用來決定消費者檢視受保護內容的方式、時間和位置。

   封裝程式至少需要一個原則，其中至少要有一個使用規則。 當License Server產生授權時，您可以覆寫使用規則，並新增其他使用規則。

1. 封裝內容並指定要套用的原則。

   Primetime DRM SDK會使用內容加密金鑰(CEK)加密內容，並將一或多個原則繫結至內容。 結果會產生*protected內容檔案*只有從對應的License Server取得授權的消費者才能播放。

   在封裝期間，內容會使用CEK加密。 CEK會使用License Server公開金鑰加密，並隨原則包含在Primetime DRM中繼資料中。 Primetime DRM中繼資料是使用Packager私密金鑰簽署，且中繼資料包含在受保護的內容中。

1. 讓受保護的內容可分發給消費者。

   受保護的內容通常會使用內容發佈網路(CDN)發佈。 CDN可使用使用者端執行階段支援的任何機制，例如Flash Media Server、用於多位元速率串流的AdobeHTTP Dynamic Streaming，或用於漸進式下載的HTTP網頁伺服器。
