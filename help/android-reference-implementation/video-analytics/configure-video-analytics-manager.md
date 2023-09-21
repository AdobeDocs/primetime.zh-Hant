---
description: 您可以將視訊設定為搭配您的Adobe Analytics帳戶使用，以追蹤Primetime Android參考實作中的視訊使用情況。
title: 設定Video Analytics
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 設定Video Analytics {#configure-video-analytics}

您可以將視訊設定為搭配您的Adobe Analytics帳戶使用，以追蹤Primetime Android參考實作中的視訊使用情況。 Android參考實作旨在將視訊使用情況和心率資料傳送至Adobe Analytics。 若要啟用此功能，您必須先聯絡Adobe Primetime代表並建立Adobe Analytics帳戶。

在「參考實作」中，您必須設定兩個位置才能啟用Adobe Analytics整合。 選取新視訊進行播放後（亦即建立新的PlayerActivity後），執行階段Video Analytics設定就會生效。

1. 在中設定載入時間選項 `ADBMobileConfig.json` 資產檔案。

   此檔案由您的Adobe代表提供。 根據預設，Primetime SDK套件組合不會包含此變數。 如需此設定檔案中設定的詳細資訊，請參閱這裡的Android程式設計師指南：初始化並設定視訊分析。
1. 在「參考實作」設定功能表中設定執行階段選項

   ![](assets/img_psdk_ref_impl_va-settings-menu.png)

   | 執行階段選項 | 說明 |
   |---|---|
   | Video Analytics追蹤伺服器 | 視訊分析後端集合端點的URL。 這是傳送所有視訊心率追蹤呼叫的位置。 |
   | 工作ID | 處理工作識別碼。 這會向後端端點指出要套用至視訊追蹤呼叫的處理型別。 |
   | 頻道 | 使用者觀看內容的頻道名稱。 若為行動應用程式，這通常是應用程式的名稱。 |
   | 發佈者 | 內容發佈者的名稱 |
   | 除錯記錄 | 啟用廣泛記錄。 預設為停用，這會在啟用時影響效能，因此您會在生產環境中停用此功能。 |
   | 安靜模式 | 啟用後，不會進行網路呼叫，因此這有助於本機偵錯，但必須停用生產環境。 |
