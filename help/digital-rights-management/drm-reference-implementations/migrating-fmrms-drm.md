---
description: 若要繼續針對已與Flash Media Rights Management Server(FMRMS)1.0或1.5一起封裝的內容發行授權，您必須將授權和DRM政策資料從LiveCycle ES伺服器移轉至客戶以Adobe Primetime DRM SDK為基礎的新伺服器。
seo-description: 若要繼續針對已與Flash Media Rights Management Server(FMRMS)1.0或1.5一起封裝的內容發行授權，您必須將授權和DRM政策資料從LiveCycle ES伺服器移轉至客戶以Adobe Primetime DRM SDK為基礎的新伺服器。
seo-title: 從FMRMS 1.0或1.5移轉至Adobe Primetime DRM 2.0或更新版本
title: 從FMRMS 1.0或1.5移轉至Adobe Primetime DRM 2.0或更新版本
uuid: 49ecbbd2-d83b-4bf2-841e-c3f9e5d5e141
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 從FMRMS 1.0或1.5移轉至Adobe Primetime DRM 2.0或更新版本{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

若要繼續針對已與Flash Media Rights Management Server(FMRMS)1.0或1.5一起封裝的內容發行授權，您必須將授權和DRM政策資料從LiveCycle ES伺服器移轉至客戶以Adobe Primetime DRM SDK為基礎的新伺服器。

若要移轉，請完成下列工作：

1. 匯入授權資訊：

   1. 若要從LiveCycle ES將授權資訊匯入您以Primetime DRM為基礎的伺服器，請參閱資料夾中的範例資料庫指 [!DNL Reference Implementation\Server\migration\db] 令碼。
   1. 運行示例指令碼，將相關資料從MySQL、Oracle或SQL Server資料庫導出為CSV檔案格式。
   1. 從LiveCycle ES匯出資料後，請將資料匯入您的資料庫。

      匯出的授權資訊包括：

      * 授權ID
      * 在封裝時指派的內容ID
      * 正在應用的DRM策略的ID
      * 內容封裝的時間
      * 內容加密金鑰
      在您將1.x內容中繼資料轉換為Primetime DRM中繼資料格式之前，需要這些資訊。 在參考實施中，此資料儲存在許可證資料庫表中，由使用 `RefImplMetadataConvReqHandler`。 有關詳細資訊，請參 `FMRMSv1RequestHandler` 見和 `FMRMSv1MetadataHandler`。


1. 將FMRMS政策轉換為Primetime DRM格式：

   1. 在您套用DRM原則以轉換中繼資料並核發1.0版或1.5版內容的授權之前，請先將現有的DRM原則轉換為Primetime DRM格式。

      該資 `Reference Implementation\Server\migration` 料夾包含建立以舊版DRM原則為基礎之Primetime DRM原則的范常式式碼。 若要從FMRMS 1.0移轉至Primetime DRM，請參閱范 `V1_0PolicyConverter.java` 例。
   1. 執行指令碼來編譯范 `ant-f build-migration.xml build-1.0-converter` 常式式碼，指令碼會在和目錄中搜尋1.0和Primetime DRM [!DNL libs/1.0] 程 [!DNL libs/flashaccess] 式庫。

   1. 編輯 [!DNL converter.properties] 檔案以指向您的LiveCycle ES伺服器。
   1. 執 `ant -f build-migration.xml migrate-all-1.0-policies` 行以將所有FMRMS 1.0 DRM策略轉換為Primetime DRM格式。

      若要從FMRMS 1.5移轉至Primetime DRM，請參閱范 `V1_5PolicyConverter.java` 例。

   1. 執行指令碼來編譯范 `ant-f build-migration.xml build-1.5-converter` 常式式碼，指定1.5和3.0程式庫位於和目 [!DNL libs/1.5] 錄 [!DNL libs/flashaccess] 中。

   1. 編輯 [!DNL converter.properties] 檔案以指向您的LiveCycle ES伺服器。
   1. 執 `ant -f build-migration.xml migrate-all-1.5-policies` 行以將所有FMRMS 1.5 DRM策略轉換為Primetime DRM格式。

      轉換的DRM策略被保存為一組檔案。 所 `DRM PolicyConverter` 述生成CSV格式的檔案，該檔案包括將舊DRM策略ID映射到新DRM策略ID。 您可以將此檔案導入 [!DNL PolicyConversion] 到引用實現資料庫中的表，該表由使用 `RefImplMetadataConvReqHandler`。

1. 支援1.x相容性要求與 `FMRMSv1RequestHandler` 和屬 `FMRMSv1MetadataHandler` 性：

   1. 在相關資料移轉至以Primetime DRM為基礎的伺服器後，實作1.x相容性要求的支援。

      如需如何處理這些請求類型的範例，請參 `RefImplUpgradeV1ClientHandler` 閱 `RefImplMetadataConvReqHandler` 參考實作。

