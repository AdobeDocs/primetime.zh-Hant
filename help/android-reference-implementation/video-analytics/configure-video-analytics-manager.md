---
description: 您可以在Primetime Android參考實作中追蹤視訊的使用情形，方法是將它設定為搭配您的Adobe Analytics帳戶運作。
title: 設定視訊分析
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# 設定視訊分析{#configure-video-analytics}

您可以在Primetime Android參考實作中追蹤視訊的使用情形，方法是將它設定為搭配您的Adobe Analytics帳戶運作。 Android參考實作旨在傳送視訊使用和心率資料至Adobe Analytics。 若要啟用此功能，您必須先連絡您的Adobe Primetime代表並建立Adobe Analytics帳戶。

「參考實作」中有兩個位置您必須進行設定，才能啟用Adobe Analytics整合。 執行時期的視訊分析設定會在選取新視訊以播放時生效（亦即，建立新的播放器活動後）。

1. 在`ADBMobileConfig.json`資產檔案中設定載入時間選項。

   此檔案由您的Adobe代表提供。 預設情況下，Primetime SDK套件中不包含它。 如需此設定檔案中設定的詳細資訊，請參閱Android程式設計人員指南，這裡：初始化並設定視訊分析。
1. 在「參考實作設定」選單中設定執行時期選項

   ![](assets/img_psdk_ref_impl_va-settings-menu.png)

   | 執行時期選項 | 說明 |
   |---|---|
   | 視訊分析追蹤伺服器 | 視訊分析後端系列端點的URL。 這是傳送所有視訊心率追蹤呼叫的地方。 |
   | 工作ID | 處理作業識別碼。 這會向後端端點指出要套用何種處理方式來進行視訊追蹤呼叫。 |
   | 頻道 | 使用者觀看內容的頻道名稱。 對於行動應用程式，這通常是應用程式的名稱。 |
   | 發行者 | 內容發佈者的名稱 |
   | 除錯記錄 | 啟動廣泛的記錄功能。 在預設下停用時，這會在啟用時影響效能，因此您會針對生產環境停用此功能。 |
   | 安靜模式 | 啟用此功能時，不會進行網路呼叫，因此這對於本機除錯非常有用，但必須針對生產環境停用。 |