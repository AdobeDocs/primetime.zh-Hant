---
description: Primetime DRM的主要元件包括Java SDK，以及Flash Player和Adobe AIR用戶端執行時期環境。
title: Java SDK、Flash Player和Adobe AIR用戶端
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# Adobe PrimetimeDRM SDK {#section_522E57DFEEFF4794978FF2D366B83690}

Primetime DRM是以Java SDK的形式提供，提供您可從中建立伺服器實作的建立區塊。 使用SDK，您可以建立適合您組織商業模型的Primetime DRM解決方案。

SDK中提供的Java API將於下列子節中說明。

## 用於管理設備組域的Java API{#java-apis-for-managing-device-group-domains}

這些API可讓伺服器處理用戶端要求加入和離開裝置群組網域。

裝置群組網域是可彼此共用授權的裝置的邏輯集合。 為了達到此目的，每台設備必須先加入／註冊到同一個域。 在伺服器上執行的Primetime DRM SDK必須處理裝置網域加入（註冊）請求，以及裝置網域離開（取消註冊）請求。 未加入任何網域的裝置將會取得系結至該裝置的授權，無法共用給任何其他裝置。

## 用於保護內容的Java API{#java-apis-for-protecting-content}

這些API可用來定義權限並準備內容以供散發。 內容保護API包括：

* 策略管理

   策略管理API用於建立和修改要應用於內容的策略。 可以建立或更新策略，包括獲取／設定所有使用規則以及允許自定義命名空間中的其他參數。

* 內容封裝

   內容封裝API用於加密內容並從封裝內容擷取中繼資料。

## 用於發行許可證的Java API{#java-apis-for-issuing-licenses}

當用戶端向伺服器要求授權時，會使用這些API。 SDK支援來自用戶端的下列要求：

* 驗證

   驗證API可用來處理驗證請求並產生驗證Token。

* 授權製作與取得

   授權產生與贏取API可用來為使用者產生授權。

* 支援Adobe AIR1.5版用戶端和內容

   為了向後相容，SDK有API可處理針對AIR 1.5版及舊版用戶端所建立之AIR應用程式的要求，以及受保護的內容。

## 參考實施{#reference-implementation}

SDK包含參考實作、簡單的Adobe PrimetimeDRM部署，示範如何使用Java API。 參考實作提供授權伺服器、Watched Folder Packager、Primetime DRM Manager AIR應用程式，以及以Java API為基礎的內容封裝與原則管理命令列工具。 若要進一步瞭解Primetime DRM參考實作，請參閱保護內容。