---
description: Primetime DRM的主要元件包括Java SDK、Flash Player和Adobe AIR使用者端執行階段環境。
title: Java SDK、Flash Player和Adobe AIR使用者端
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# ADOBE PRIMETIME DRM SDK {#section_522E57DFEEFF4794978FF2D366B83690}

Primetime DRM是以Java SDK的形式提供，可提供建置區塊，讓您從中建立伺服器實作。 使用SDK，您可以建立適合您組織商業模式的Primetime DRM解決方案。

以下小節將說明SDK中提供的Java API。

## 用於管理裝置群組網域的Java API{#java-apis-for-managing-device-group-domains}

這些API可讓伺服器處理加入和離開裝置群組網域的使用者端請求。

裝置群組網域是能夠彼此共用授權的裝置的邏輯集合。 為了做到這一點，每個裝置必須首先聯結/註冊到相同的網域。 在伺服器上執行的Primetime DRM SDK必須處理裝置網域加入（註冊）請求以及裝置網域離開（取消註冊）請求。 未加入任何網域的裝置將獲得與該裝置繫結的授權，該授權無法與任何其他裝置共用。

## 用於保護內容的Java API{#java-apis-for-protecting-content}

這些API用於定義許可權及準備內容以進行分發。 內容保護API為：

* 原則管理

  原則管理API可用來建立和修改要套用至內容的原則。 您可以建立或更新原則，包括取得/設定所有使用規則，以及允許自訂名稱空間中的其他引數。

* 內容封裝

  內容封裝API用於加密內容，以及從封裝內容中擷取中繼資料。

## 用於發行授權的Java API{#java-apis-for-issuing-licenses}

當使用者端向伺服器要求授權時，就會使用這些API。 SDK支援使用者端的下列要求：

* 驗證

  驗證API可用於處理驗證請求並產生驗證權杖。

* 授權產生與贏取

  授權產生和贏取API用於為使用者產生授權。

* 支援Adobe AIR 1.5版本的使用者端和內容

  為了回溯相容性的目的，SDK有API可處理來自AIR應用程式的請求，這些應用程式是針對AIR 1.5版及舊版使用者端和受保護的內容而建立的。

## 參考實作 {#reference-implementation}

SDK包含參考實作、簡單的Adobe Primetime DRM部署，示範如何使用Java API。 參考實作提供許可證伺服器、Watched資料夾封裝程式、Primetime DRM管理員AIR應用程式，以及根據Java API進行內容封裝和原則管理的命令列工具。 若要深入瞭解Primetime DRM參考實作，請參閱保護內容。
