---
title: 授權取得程式概觀
description: 授權取得程式概觀
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---


# 授權取得程式概觀{#license-acquisition-process-overview}

以下各節使用ActionScript3(AS3)程式碼範例，說明如何讓您的應用程式在Primetime DRM的保護下播放內容。 針對行動平台上的原生應用程式，會在適當時候顯示與此工作流程的細微差異。 不過，Primetime DRM工作流程在所有平台上都非常類似，因此您對AS3程式碼的瞭解會讓您將外推至其他平台變得相當簡單。

**授權取得程式：**

1. 取得受保護內容的DRM中繼資料。
1. 檢查本機是否提供授權：

   * 如果授權可在本機使用，請載入授權並前往步驟6。
   * 如果本機未提供授權，請繼續步驟3。

1. 檢查是否需要驗證：

   * 如果需要驗證，請從使用者取得驗證憑證，並將其傳遞至授權伺服器。
   * 如果不需要驗證，請轉至步驟6。

1. 如果需要設備域註冊，請加入設備域。
1. 如果需要驗證且現在已完成，請從授權伺服器下載授權。
1. 播放內容。

如果未發生任何錯誤，且使用者已成功獲得檢視內容的授權，Primetime會調度`DRMStatusEvent`物件，而應用程式會開始播放。 `DRMStatusEvent`物件包含相關的授權資訊，可識別使用者的原則和權限。 例如，`DRMStatusEvent`可能會包含有關內容是否可離線使用、授權到期等資訊。

應用程式可使用授權資訊來通知使用者其原則的狀態。 例如，應用程式可顯示使用者在狀態列中檢視內容的剩餘天數。 如果允許使用者離線存取，則會快取授權，並將加密內容下載至使用者的機器。 內容可在授權快取期間定義期間存取。 事件中的detail屬性包含`DRM.voucherObtained`。 應用程式會決定將內容儲存在本機的位置，以便離線使用。 您也可以使用`DRMManager`類別預先載入授權。
