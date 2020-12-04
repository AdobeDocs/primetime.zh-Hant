---
seo-title: 從FMRMS 1.0或1.5移轉至Adobe Access 2.0及更新版本
title: 從FMRMS 1.0或1.5移轉至Adobe Access 2.0及更新版本
uuid: 05caeb39-0c62-4053-87a9-8e89030a188d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# 從FMRMS 1.0或1.5移轉至Adobe Access 2.0及以上版本{#migrating-from-fmrms-or-to-adobe-access-and-above}

為了繼續針對使用Flash Media Rights Management Server(FMRMS)1.0或1.5封裝的內容發行授權，授權和政策資料必須從LiveCycle ES伺服器移轉至客戶以Adobe Access SDK為基礎的新伺服器。 重要步驟是：

1. 匯入授權資訊
1. 將FMRMS政策轉換為Adobe Access格式
1. 透過`FMRMSv1RequestHandler`和`FMRMSv1MetadataHandler`支援1.x相容性要求

若要從LiveCycle ES將授權資訊匯入您以Adobe Access為基礎的伺服器，請參閱[!DNL Reference Implementation\Server\migration\db]資料夾中提供的範例資料庫指令碼。 提供了用於將相關資料從MySQL、Oracle或SQL Server資料庫導出為CSV檔案格式的示例指令碼。 匯出資料後，即可將其匯入您選擇的資料庫。 匯出的授權資訊包括授權ID、封裝時指派的內容ID、使用之原則的ID、封裝內容的時間，以及內容加密金鑰。 若是Adobe Access，必須將此資訊轉換為Adobe Access中繼資料格式（請參閱`FMRMSv1RequestHandler`和`FMRMSv1MetadataHandler`）。 在參考實施中，此資料儲存在許可證資料庫表中，並由`RefImplMetadataConvReqHandler`使用。

現有政策必須轉換為Adobe Access格式，才能在轉換中繼資料及核發1.0或1.5內容授權時使用這些政策。 參考Implementation\Server\migration folder contains sample code for creating an Adobe Access policy based on older policies。

如果您要從FMRMS 1.0移轉至Adobe Access，請參閱V1_0PolicyConverter.java範例。 執行&quot; `ant-f build-migration.xml build-1.0-converter`&quot;編譯范常式式碼（指令碼預期1.0和Adobe Access程式庫分別位於[!DNL libs/1.0]和libs/flashaccess中）。 編輯converter.properties檔案以指向您的LiveCycle ES伺服器。 然後執行&quot; `ant -f build-migration.xml migrate-all-1.0-policies`&quot;，將所有FMRMS 1.0原則轉換為Adobe Access格式。

如果您要從FMRMS 1.5移轉至Adobe Access，請參閱V1_5PolicyConverter.java範例。 執行&quot; `ant-f build-migration.xml build-1.5-converter`&quot;編譯范常式式碼（指令碼預期1.5和3.0程式庫分別位於libs/1.5和libs/flashaccess中）。 編輯converter.properties檔案以指向您的LiveCycle ES伺服器。 然後執行&quot; `ant -f build-migration.xml migrate-all-1.5-policies`&quot;，將所有FMRMS 1.5原則轉換為Adobe Access格式。

轉換的策略將寫入一組檔案。 此外，PolicyConverter將輸出一個CSV檔案，其中包含將舊策略ID映射到新策略ID的映射。 此檔案可以導入到參考實施資料庫的&quot;PolicyConversion&quot;表中，並將由`RefImplMetadataConvReqHandler`使用。

相關資料移轉至Adobe Access型伺服器後，您就可以建置1.x相容性要求的支援。 請參閱參考實作中的`RefImplUpgradeV1ClientHandler`和`RefImplMetadataConvReqHandler`，以取得如何處理這些請求類型的範例。
