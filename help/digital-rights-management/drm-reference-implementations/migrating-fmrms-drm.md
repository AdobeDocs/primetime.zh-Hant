---
description: 若要繼續針對已與Flash媒體Rights Management伺服器(FMRMS)1.0或1.5一起封裝的內容發行授權，您必須將授權和DRM政策資料從LiveCycleES伺服器移轉至客戶以Adobe PrimetimeDRM SDK為基礎的新伺服器。
title: 從FMRMS 1.0或1.5移轉至Adobe PrimetimeDRM 2.0或更新版本
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---


# 從FMRMS 1.0或1.5移轉至Adobe PrimetimeDRM 2.0或更新版本{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

若要繼續針對已與Flash媒體Rights Management伺服器(FMRMS)1.0或1.5一起封裝的內容發行授權，您必須將授權和DRM政策資料從LiveCycleES伺服器移轉至客戶以Adobe PrimetimeDRM SDK為基礎的新伺服器。

若要移轉，請完成下列工作：

1. 匯入授權資訊：

   1. 要從LiveCycleES將許可證資訊導入基於Primetime DRM的伺服器，請參閱[!DNL Reference Implementation\Server\migration\db]資料夾中的示例資料庫指令碼。
   1. 運行示例指令碼，將相關資料從MySQL、Oracle或SQL Server資料庫導出為CSV檔案格式。
   1. 從LiveCycleES導出資料後，將資料導入資料庫。

      匯出的授權資訊包括：

      * 授權ID
      * 在封裝時指派的內容ID
      * 正在應用的DRM策略的ID
      * 內容封裝的時間
      * 內容加密金鑰

      在您將1.x內容中繼資料轉換為Primetime DRM中繼資料格式之前，需要這些資訊。 在參考實施中，此資料儲存在許可證資料庫表中，並由`RefImplMetadataConvReqHandler`使用。 如需詳細資訊，請參閱`FMRMSv1RequestHandler`和`FMRMSv1MetadataHandler`。


1. 將FMRMS政策轉換為Primetime DRM格式：

   1. 在您套用DRM原則以轉換中繼資料並核發1.0版或1.5版內容的授權之前，請先將現有的DRM原則轉換為Primetime DRM格式。

      `Reference Implementation\Server\migration`資料夾包含范常式式碼，以建立以舊版DRM政策為基礎的Primetime DRM政策。 若要從FMRMS 1.0移轉至Primetime DRM，請參閱`V1_0PolicyConverter.java`範例。
   1. 運行`ant-f build-migration.xml build-1.0-converter`指令碼編譯示例代碼，該指令碼在[!DNL libs/1.0]和[!DNL libs/flashaccess]目錄中搜索1.0和Primetime DRM庫。

   1. 編輯[!DNL converter.properties]檔案以指向LiveCycleES伺服器。
   1. 運行`ant -f build-migration.xml migrate-all-1.0-policies`將所有FMRMS 1.0 DRM策略轉換為Primetime DRM格式。

      若要從FMRMS 1.5移轉至Primetime DRM，請參閱`V1_5PolicyConverter.java`範例。

   1. 運行`ant-f build-migration.xml build-1.5-converter`指令碼編譯示例代碼，該指令碼預期1.5和3.0庫位於[!DNL libs/1.5]和[!DNL libs/flashaccess]目錄中。

   1. 編輯[!DNL converter.properties]檔案以指向LiveCycleES伺服器。
   1. 運行`ant -f build-migration.xml migrate-all-1.5-policies`將所有FMRMS 1.5 DRM策略轉換為Primetime DRM格式。

      轉換的DRM策略被保存為一組檔案。 `DRM PolicyConverter`生成CSV格式的檔案，該檔案包括將舊DRM策略ID映射到新DRM策略ID。 您可以將此檔案導入到參考實施資料庫中的[!DNL PolicyConversion]表，其中`RefImplMetadataConvReqHandler`使用該檔案。

1. 支援`FMRMSv1RequestHandler`和`FMRMSv1MetadataHandler`屬性的1.x相容性要求：

   1. 在相關資料移轉至以Primetime DRM為基礎的伺服器後，實作1.x相容性要求的支援。

      如需如何處理這些請求類型的範例，請參閱參考實作中的`RefImplUpgradeV1ClientHandler`和`RefImplMetadataConvReqHandler`。

