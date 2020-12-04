---
description: 本指南提供如何使用TVSDK for Android（以Java實作）開發視訊播放器應用程式的相關資訊。
seo-description: 本指南提供如何使用TVSDK for Android（以Java實作）開發視訊播放器應用程式的相關資訊。
seo-title: 產品概觀、觀眾和本指南
title: 產品概觀、觀眾和本指南
uuid: dd281a3e-a85f-4470-a730-2c5e87d0e490
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# 概述{#audience}

本指南提供如何使用TVSDK for Android（以Java實作）開發視訊播放器應用程式的相關資訊。

<!--<a id="section_FC24E86A2E6442B8A3769160769BBDFA"></a>-->

* 如需TVSDK支援的功能清單，請參閱[Primetime TVSDK功能](../../../tvsdk-3x-android-prog/android-3x-introduction/overview-prod-audience-guide/android-3x-overview-of-the-player.md)。
* 有關使用TVSDK的特定硬體和軟體需求，請參閱[需求](../../../tvsdk-3x-android-prog/android-3x-introduction/android-3x-requirements.md)。
* 如需可用API的清單，請參閱[TVSDK Android API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.5/index.html)。

## 產品概觀{#section_9664959F25C948878F2F7EF3D360CA95}

TVSDK包含API說明和程式碼範例，可協助您將進階視訊功能、內容保護和廣告功能整合至您的播放器。 您可使用Java來建立視訊播放器使用者介面。 TVSDK可協助您將該使用者介面連接至其媒體播放器。 這可讓您根據媒體資訊清單播放視訊和廣告。 您也可以使用TVSDK來擷取視訊的相關資訊、處理安全性，以及控制和監視播放。

## 對象{#section_527860B373734D3BA89FCF5EC1F6DC37}

本指南假設您瞭解如何使用Java開發應用程式和視訊播放器。 您可在Java中實作視訊播放器UI，並整合所需的TVSDK功能。

## 關於本指南{#section_9A5B2FC506B34B5DB71CA827B307A4D0}

本指南提供可讓您在Android裝置上使用Java將TVSDK功能整合在視訊播放器中的資訊。

## 本指南{#section_8B866054E9ED4B5F99DCA7A681404632}中的命名空間符號

>[!TIP]
>
>TVSDK API命名空間首碼[!DNL com.adobe.mediacore]通常會略過，以便簡潔。
>
>如果內容清楚，則會參照許多API元素，而不使用其父類別指示符。