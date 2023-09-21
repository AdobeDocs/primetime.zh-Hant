---
title: 從FMRMS 1.0或1.5移轉至Adobe存取2.0和更高版本
description: 從FMRMS 1.0或1.5移轉至Adobe存取2.0和更高版本
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# 從FMRMS 1.0或1.5移轉至Adobe存取2.0和更高版本 {#migrating-from-fmrms-or-to-adobe-access-and-above}

為了繼續為使用Flash MediaRights Management伺服器(FMRMS) 1.0或1.5封裝的內容發行授權，授權和原則資料必須從LiveCycleES伺服器移轉到客戶基於AdobeAccess SDK的新伺服器。 重要步驟為：

1. 匯入授權資訊
1. 將FMRMS原則轉換為Adobe存取格式
1. 透過支援1.x相容性要求 `FMRMSv1RequestHandler` 和 `FMRMSv1MetadataHandler`

若要將LiveCycleES的授權資訊匯入AdobeAccess型伺服器，請參閱 [!DNL Reference Implementation\Server\migration\db] 資料夾。 提供範例指令碼，用於將相關資料從MySQL、Oracle或SQL Server資料庫匯出為CSV檔案格式。 匯出資料後，即可將其匯入您選擇的資料庫。 匯出的授權資訊包括授權ID、封裝時指派的內容ID、所使用原則的ID、內容封裝的時間以及內容加密金鑰。 如需Adobe存取的相關資訊，請務必提供此資訊，以便將1.x內容中繼資料轉換為Adobe存取中繼資料格式(請參閱 `FMRMSv1RequestHandler` 和 `FMRMSv1MetadataHandler`)。 在參考實作中，此資料儲存在「許可證」資料庫表格中，並由 `RefImplMetadataConvReqHandler`.

現有原則需要轉換成Adobe存取格式，才能在轉換1.0或1.5內容的中繼資料和核發授權時使用那些原則。 Reference Implementation\Server\migration資料夾包含根據舊有原則建立Adobe存取原則的範常式式碼。

如果您要從FMRMS 1.0移轉至Adobe存取，請參閱V1_0PolicyConverter.java範例。 執行&#39;&#39;以編譯範常式式碼 `ant-f build-migration.xml build-1.0-converter`「 (指令碼預期1.0和Adobe存取程式庫位於 [!DNL libs/1.0] 和libs/flashaccess)。 編輯converter.properties檔案以指向您的LiveCycleES伺服器。 然後執行「 `ant -f build-migration.xml migrate-all-1.0-policies`»以將所有FMRMS 1.0原則轉換為Adobe存取格式。

如果您要從FMRMS 1.5移轉至Adobe存取，請參閱V1_5PolicyConverter.java範例。 執行&#39;&#39;以編譯範常式式碼 `ant-f build-migration.xml build-1.5-converter`「 （指令碼預期1.5和3.0程式庫分別在libs/1.5和libs/flashaccess中）。 編輯converter.properties檔案以指向您的LiveCycleES伺服器。 然後執行「 `ant -f build-migration.xml migrate-all-1.5-policies`»以將所有FMRMS 1.5原則轉換為Adobe存取格式。

轉換的原則將寫入一組檔案中。 此外，PolicyConverter將會輸出包含舊原則ID與新原則ID對應的CSV檔案。 此檔案可匯入參考實作資料庫的「PolicyConversion」表格，並將由使用 `RefImplMetadataConvReqHandler`.

將相關資料移轉至Adobe存取型伺服器後，您就可以實作1.x相容性要求的支援。 另請參閱 `RefImplUpgradeV1ClientHandler` 和 `RefImplMetadataConvReqHandler` 在參考實作中，以取得如何處理這些型別請求的範例。
