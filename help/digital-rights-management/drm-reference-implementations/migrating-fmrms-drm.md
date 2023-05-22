---
description: 要繼續為已與Flash媒體Rights Management伺服器(FMRMS)1.0或1.5打包的內容頒發許可證，必須將許可證和DRM策略資料從LiveCycleES伺服器遷移到基於Adobe PrimetimeDRM SDK的客戶新伺服器。
title: 從FMRMS 1.0或1.5遷移到Adobe PrimetimeDRM 2.0或更高版本
exl-id: 6490f2ad-4863-4b41-9ebd-1de47da4250b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# 從FMRMS 1.0或1.5遷移到Adobe PrimetimeDRM 2.0或更高版本{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

要繼續為已與Flash媒體Rights Management伺服器(FMRMS)1.0或1.5打包的內容頒發許可證，必須將許可證和DRM策略資料從LiveCycleES伺服器遷移到基於Adobe PrimetimeDRM SDK的客戶新伺服器。

要遷移，請完成以下任務：

1. 導入許可證資訊：

   1. 要將許可證資訊從LiveCycleES導入到基於Mogine DRM的伺服器，請參閱 [!DNL Reference Implementation\Server\migration\db] 的子菜單。
   1. 運行示例指令碼，將相關資料從MySQL、Oracle或SQL Server資料庫導出為CSV檔案格式。
   1. 從LiveCycleES導出資料後，將資料導入到資料庫。

      導出的許可證資訊包括：

      * 許可證ID
      * 打包時分配的內容ID
      * 正在應用的DRM策略的ID
      * 內容打包的時間
      * 內容加密密鑰

      在將1.x內容元資料轉換為黃金時段DRM元資料格式之前，需要此資訊。 在引用實現中，此資料儲存在許可證資料庫表中，並由 `RefImplMetadataConvReqHandler`。 有關詳細資訊，請參見 `FMRMSv1RequestHandler` 和 `FMRMSv1MetadataHandler`。


1. 將FMRMS策略轉換為黃金時段DRM格式：

   1. 在應用DRM策略以轉換元資料並為1.0版或1.5版內容頒發許可證之前，請將現有DRM策略轉換為黃金時段DRM格式。

      的 `Reference Implementation\Server\migration` 資料夾包含建立基於舊DRM策略的Mogfire DRM策略的示例代碼。 要從FMRMS 1.0遷移到黃金時段DRM，請參閱 `V1_0PolicyConverter.java` 樣式。
   1. 通過運行編譯示例代碼 `ant-f build-migration.xml build-1.0-converter` 指令碼，用於在中搜索1.0和黃金時段DRM庫 [!DNL libs/1.0] 和 [!DNL libs/flashaccess] 的子菜單。

   1. 編輯 [!DNL converter.properties] 檔案以指向您的LiveCycleES伺服器。
   1. 運行 `ant -f build-migration.xml migrate-all-1.0-policies` 將所有FMRMS 1.0 DRM策略轉換為黃金時段DRM格式。

      要從FMRMS 1.5遷移到黃金時段DRM，請參閱 `V1_5PolicyConverter.java` 樣式。

   1. 通過運行編譯示例代碼 `ant-f build-migration.xml build-1.5-converter` 指令碼，它要求1.5和3.0庫在 [!DNL libs/1.5] 和 [!DNL libs/flashaccess] 的子菜單。

   1. 編輯 [!DNL converter.properties] 檔案以指向您的LiveCycleES伺服器。
   1. 運行 `ant -f build-migration.xml migrate-all-1.5-policies` 將所有FMRMS 1.5 DRM策略轉換為黃金時段DRM格式。

      轉換的DRM策略被保存為一組檔案。 的 `DRM PolicyConverter` 生成CSV格式的檔案，該檔案包括將舊DRM策略ID映射到新DRM策略ID。 可以將此檔案導入到 [!DNL PolicyConversion] 引用實現資料庫中的表，其使用 `RefImplMetadataConvReqHandler`。

1. 支援與 `FMRMSv1RequestHandler` 和 `FMRMSv1MetadataHandler` 屬性：

   1. 在相關資料已遷移到基於黃金時段DRM的伺服器後，實現對1.x相容性請求的支援。

      有關如何處理這些類型請求的示例，請參見 `RefImplUpgradeV1ClientHandler` 和 `RefImplMetadataConvReqHandler` 在參考實現中。
