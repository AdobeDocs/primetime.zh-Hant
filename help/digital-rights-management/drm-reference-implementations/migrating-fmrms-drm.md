---
description: 若要繼續核發已與Flash MediaRights Management伺服器(FMRMS) 1.0或1.5封裝之內容的授權，您必須將授權和DRM原則資料從LiveCycleES伺服器移轉至客戶以Adobe Primetime DRM SDK為基礎的新伺服器。
title: 從FMRMS 1.0或1.5移轉至Adobe Primetime DRM 2.0或更新版本
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# 從FMRMS 1.0或1.5移轉至Adobe Primetime DRM 2.0或更新版本{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

若要繼續核發已與Flash MediaRights Management伺服器(FMRMS) 1.0或1.5封裝之內容的授權，您必須將授權和DRM原則資料從LiveCycleES伺服器移轉至客戶以Adobe Primetime DRM SDK為基礎的新伺服器。

若要移轉，請完成下列作業：

1. 匯入授權資訊：

   1. 若要將許可證資訊從LiveCycleES匯入至以Primetime DRM為基礎的伺服器，請參閱 [!DNL Reference Implementation\Server\migration\db] 資料夾。
   1. 執行範例指令碼，將相關資料從MySQL、Oracle或SQL Server資料庫匯出為CSV檔案格式。
   1. 從LiveCycleES匯出資料後，將資料匯入資料庫。

      匯出的授權資訊包括下列內容：

      * 授權ID
      * 封裝時指派的內容ID
      * 正在套用的DRM原則ID
      * 封裝內容的時間
      * 內容加密金鑰

      在將1.x內容中繼資料轉換為Primetime DRM中繼資料格式之前，需要此資訊。 在參考實作中，此資料儲存在「許可證」資料庫表格中，並由 `RefImplMetadataConvReqHandler`. 如需詳細資訊，請參閱 `FMRMSv1RequestHandler` 和 `FMRMSv1MetadataHandler`.

1. 將FMRMS原則轉換為Primetime DRM格式：

   1. 在您套用DRM政策來轉換1.0或1.5版本內容的中繼資料並簽發許可證之前，請先將現有DRM政策轉換為Primetime DRM格式。

      此 `Reference Implementation\Server\migration` 資料夾包含以舊版DRM原則為基礎來建立Primetime DRM原則的範常式式碼。 若要從FMRMS 1.0移轉至Primetime DRM ，請參閱 `V1_0PolicyConverter.java` 範例。
   1. 執行以編譯範常式式碼 `ant-f build-migration.xml build-1.0-converter` 指令碼，會在中搜尋1.0和Primetime DRM程式庫 [!DNL libs/1.0] 和 [!DNL libs/flashaccess] 目錄。

   1. 編輯 [!DNL converter.properties] 檔案以指向您的LiveCycleES伺服器。
   1. 執行 `ant -f build-migration.xml migrate-all-1.0-policies` 將所有FMRMS 1.0 DRM原則轉換為Primetime DRM格式。

      若要從FMRMS 1.5移轉至Primetime DRM ，請參閱 `V1_5PolicyConverter.java` 範例。

   1. 執行以編譯範常式式碼 `ant-f build-migration.xml build-1.5-converter` 指令碼，預期1.5和3.0程式庫位於 [!DNL libs/1.5] 和 [!DNL libs/flashaccess] 目錄。

   1. 編輯 [!DNL converter.properties] 檔案以指向您的LiveCycleES伺服器。
   1. 執行 `ant -f build-migration.xml migrate-all-1.5-policies` 將所有FMRMS 1.5 DRM原則轉換為Primetime DRM格式。

      轉換的DRM政策會儲存為一組檔案。 此 `DRM PolicyConverter` 會產生CSV格式的檔案，其中包括將舊的DRM原則ID對應到新的DRM原則ID。 您可以將此檔案匯入 [!DNL PolicyConversion] 參考實作資料庫中的表格，用於 `RefImplMetadataConvReqHandler`.

1. 透過支援1.x相容性要求 `FMRMSv1RequestHandler` 和 `FMRMSv1MetadataHandler` 屬性：

   1. 將相關資料移轉至Primetime DRM伺服器後，實作1.x相容性要求的支援。

      如需有關如何處理這些型別請求的範例，請參閱 `RefImplUpgradeV1ClientHandler` 和 `RefImplMetadataConvReqHandler` 在參考實作中。
