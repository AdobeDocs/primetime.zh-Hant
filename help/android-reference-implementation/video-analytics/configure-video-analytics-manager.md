---
description: 通過將其配置為與您的Adobe Analytics帳戶配合使用，您可以跟蹤黃金時段Android參考實施中的視頻使用情況。
title: 配置視頻分析
exl-id: 42498e2a-9ff2-442c-8cf9-bd7901f618f4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 配置視頻分析 {#configure-video-analytics}

通過將其配置為與您的Adobe Analytics帳戶配合使用，您可以跟蹤黃金時段Android參考實施中的視頻使用情況。 Android參考實現旨在將視頻使用和心跳資料發送到Adobe Analytics。 要啟用此功能，您必須首先與Adobe Primetime代表聯繫並建立Adobe Analytics帳戶。

「參考實施」中有兩個位置必須配置以啟用Adobe Analytics整合。 一旦選擇了新視頻進行回放（即，一旦建立了新的PlayerActiviy），運行時視頻分析配置將生效。

1. 在 `ADBMobileConfig.json` assets檔案。

   此檔案由您的Adobe代表提供。 預設情況下，它不包括在黃金時段SDK包中。 有關此配置檔案中設定的詳細資訊，請參閱以下Android程式設計師指南：初始化和配置視頻分析。
1. 在「參考實施設定」菜單中配置運行時選項

   ![](assets/img_psdk_ref_impl_va-settings-menu.png)

   | 運行時選項 | 說明 |
   |---|---|
   | 視頻分析跟蹤伺服器 | 視頻分析後端集合終點的URL。 這是發送所有視頻心跳跟蹤呼叫的地方。 |
   | 作業ID | 處理作業標識符。 這向後端端點指示應用於視頻跟蹤呼叫的處理類型。 |
   | 頻道 | 用戶正在監視內容的頻道的名稱。 對於移動應用程式，這通常是應用程式的名稱。 |
   | 發佈者 | 內容發佈者的名稱 |
   | 調試日誌記錄 | 激活大量日誌記錄。 預設情況下禁用，啟用時可能會影響效能，因此您可以對生產環境禁用此功能。 |
   | 安靜模式 | 啟用此功能後，將不會進行網路調用，因此這對本地調試非常有用，但必須對生產環境禁用。 |
