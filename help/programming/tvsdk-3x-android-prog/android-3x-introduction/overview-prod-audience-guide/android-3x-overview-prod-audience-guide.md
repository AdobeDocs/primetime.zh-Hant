---
description: 本指南提供如何在Java中實作的Android版TVSDK開發視訊播放器應用程式的相關資訊。
title: 產品概述、對象和本指南
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# 概觀 {#audience}

本指南提供如何在Java中實作的Android版TVSDK開發視訊播放器應用程式的相關資訊。

<!--<a id="section_FC24E86A2E6442B8A3769160769BBDFA"></a>-->

* 如需TVSDK支援的功能清單，請參閱 [Primetime TVSDK功能](../../../tvsdk-3x-android-prog/android-3x-introduction/overview-prod-audience-guide/android-3x-overview-of-the-player.md).
* 如需使用TVSDK的特定軟硬體需求，請參閱 [需求](../../../tvsdk-3x-android-prog/android-3x-introduction/android-3x-requirements.md).
* 如需可用API的清單，請參閱 [TVSDK Android API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.5/index.html).

## 產品概述 {#section_9664959F25C948878F2F7EF3D360CA95}

TVSDK包含API說明和程式碼範例，協助您將進階視訊功能、內容保護和廣告功能整合到播放器中。 您可以使用Java建立視訊播放器使用者介面。 TVSDK可協助您將使用者介面連線到其媒體播放器。 這可讓您根據媒體資訊清單播放影片和廣告。 您也可以使用TVSDK來擷取視訊的相關資訊、處理安全性以及控制和監視播放。

## 對象 {#section_527860B373734D3BA89FCF5EC1F6DC37}

本指南假設您瞭解如何使用Java開發應用計畫和視訊播放器。 您需在Java中實作視訊播放器UI，並整合所需的TVSDK功能。

## 關於本指南 {#section_9A5B2FC506B34B5DB71CA827B307A4D0}

本指南提供的資訊可讓您在Android裝置上使用Java的視訊播放器中納入TVSDK功能。

## 本指南中的名稱空間標籤法 {#section_8B866054E9ED4B5F99DCA7A681404632}

>[!TIP]
>
>TVSDK API名稱空間前置詞 [!DNL com.adobe.mediacore] 為了簡單起見，通常會省略。
>
>如果上下文是清楚的，許多API元素在參照時沒有它們的父類別指示器。
