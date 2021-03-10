---
title: 從FMRMS 1.0或1.5遷移到Adobe訪問2.0和更高版本
description: 從FMRMS 1.0或1.5遷移到Adobe訪問2.0和更高版本
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# 從FMRMS 1.0或1.5遷移到AdobeAccess 2.0和{#migrating-from-fmrms-or-to-adobe-access-and-above}以上版本

為了繼續針對使用Flash媒體Rights Management伺服器(FMRMS)1.0或1.5封裝的內容發行授權，授權和原則資料必須從LiveCycleES伺服器移轉至客戶的新伺服器(以Adobe存取SDK為基礎)。 重要步驟是：

1. 匯入授權資訊
1. 將FMRMS策略轉換為Adobe訪問格式
1. 透過`FMRMSv1RequestHandler`和`FMRMSv1MetadataHandler`支援1.x相容性要求

要從LiveCycleES將許可證資訊導入基於Adobe訪問的伺服器，請參閱[!DNL Reference Implementation\Server\migration\db]資料夾中提供的示例資料庫指令碼。 提供了用於將相關資料從MySQL、Oracle或SQL Server資料庫導出為CSV檔案格式的示例指令碼。 匯出資料後，即可將其匯入您選擇的資料庫。 匯出的授權資訊包括授權ID、封裝時指派的內容ID、使用之原則的ID、封裝內容的時間，以及內容加密金鑰。 對於Adobe訪問，需要此資訊才能將1.x內容元資料轉換為Adobe訪問元資料格式（請參見`FMRMSv1RequestHandler`和`FMRMSv1MetadataHandler`）。 在參考實施中，此資料儲存在許可證資料庫表中，並由`RefImplMetadataConvReqHandler`使用。

現有的原則必須轉換為「Adobe存取」格式，以便在轉換中繼資料並核發1.0或1.5內容的授權時，才能使用這些原則。 參考Implementation\Server\migration folder contains sample code for creating an Adobe Access policy based on older policies。

如果要從FMRMS 1.0遷移到Adobe訪問，請參見V1_0PolicyConverter.java示例。 執行&quot; `ant-f build-migration.xml build-1.0-converter`&quot;編譯范常式式碼(指令碼預期1.0和Adobe存取程式庫分別位於[!DNL libs/1.0]和libs/flashaccess中)。 編輯converter.properties檔案以指向LiveCycleES伺服器。 然後執行&quot; `ant -f build-migration.xml migrate-all-1.0-policies`&quot;，將所有FMRMS 1.0策略轉換為Adobe訪問格式。

如果要從FMRMS 1.5遷移到Adobe訪問，請參見V1_5PolicyConverter.java示例。 執行&quot; `ant-f build-migration.xml build-1.5-converter`&quot;編譯范常式式碼（指令碼預期1.5和3.0程式庫分別位於libs/1.5和libs/flashaccess中）。 編輯converter.properties檔案以指向LiveCycleES伺服器。 然後執行&quot; `ant -f build-migration.xml migrate-all-1.5-policies`&quot;，將所有FMRMS 1.5策略轉換為Adobe訪問格式。

轉換的策略將寫入一組檔案。 此外，PolicyConverter將輸出一個CSV檔案，其中包含將舊策略ID映射到新策略ID的映射。 此檔案可以導入到參考實施資料庫的&quot;PolicyConversion&quot;表中，並將由`RefImplMetadataConvReqHandler`使用。

相關資料移轉至您的Adobe存取式伺服器後，您就可以建置1.x相容性要求的支援。 請參閱參考實作中的`RefImplUpgradeV1ClientHandler`和`RefImplMetadataConvReqHandler`，以取得如何處理這些請求類型的範例。
