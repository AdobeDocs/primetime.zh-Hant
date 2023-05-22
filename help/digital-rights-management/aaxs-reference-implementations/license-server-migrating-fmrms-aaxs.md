---
title: 從FMRMS 1.0或1.5遷移到AdobeAccess 2.0及更高版本
description: 從FMRMS 1.0或1.5遷移到AdobeAccess 2.0及更高版本
copied-description: true
exl-id: 9aadf9a0-a7c5-466b-9dd1-c1bab2b8bfc6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# 從FMRMS 1.0或1.5遷移到AdobeAccess 2.0及更高版本 {#migrating-from-fmrms-or-to-adobe-access-and-above}

為了繼續為使用Flash媒體Rights Management伺服器(FMRMS)1.0或1.5打包的內容頒發許可證，必鬚根據Adobe訪問SDK將許可證和策略資料從LiveCycleES伺服器遷移到客戶的新伺服器。 重要步驟是：

1. 導入許可證資訊
1. 將FMRMS策略轉換為Adobe訪問格式
1. 通過 `FMRMSv1RequestHandler` 和 `FMRMSv1MetadataHandler`

要將許可證資訊從LiveCycleES導入到基於Adobe訪問的伺服器，請參閱中提供的示例資料庫指令碼 [!DNL Reference Implementation\Server\migration\db] 的子菜單。 提供了示例指令碼，用於將相關資料從MySQL、Oracle或SQL Server資料庫導出為CSV檔案格式。 導出資料後，可將其導入到您選擇的資料庫中。 導出的許可證資訊包括許可證ID、打包時分配的內容ID、使用的策略ID、打包內容的時間以及內容加密密鑰。 對於Adobe訪問，將1.x內容元資料轉換為Adobe訪問元資料格式時需要此資訊(請參見 `FMRMSv1RequestHandler` 和 `FMRMSv1MetadataHandler`)。 在引用實現中，此資料儲存在許可證資料庫表中，並由 `RefImplMetadataConvReqHandler`。

現有策略需要轉換為Adobe訪問格式，以便在轉換元資料和為1.0或1.5內容頒發許可證時使用這些策略。 Reference Implementation\Server\migration資料夾包含用於基於舊策略建立Adobe訪問策略的示例代碼。

如果要從FMRMS 1.0遷移到「Adobe訪問」，請參見V1_0PolicyConverter.java示例。 通過運行「」編譯示例代碼 `ant-f build-migration.xml build-1.0-converter`&quot;(指令碼要求1.0和Adobe訪問庫位於 [!DNL libs/1.0] 和libs/flashaccess)。 編輯converter.properties檔案以指向LiveCycleES伺服器。 然後運行「 `ant -f build-migration.xml migrate-all-1.0-policies`&quot;將所有FMRMS 1.0策略轉換為Adobe訪問格式。

如果要從FMRMS 1.5遷移到Adobe訪問，請參見V1_5PolicyConverter.java示例。 通過運行「」編譯示例代碼 `ant-f build-migration.xml build-1.5-converter`&quot;（指令碼希望1.5和3.0庫分別位於libs/1.5和libs/flashaccess中）。 編輯converter.properties檔案以指向LiveCycleES伺服器。 然後運行「 `ant -f build-migration.xml migrate-all-1.5-policies`&quot;將所有FMRMS 1.5策略轉換為Adobe訪問格式。

轉換後的策略將寫入一組檔案。 此外，PolicyConverter將輸出一個CSV檔案，其中包含舊策略ID到新策略ID的映射。 此檔案可導入到引用實現資料庫的「PolicyConversion」表中，並將由 `RefImplMetadataConvReqHandler`。

在相關資料遷移到基於Adobe訪問的伺服器後，您就可以實施對1.x相容性請求的支援。 請參閱 `RefImplUpgradeV1ClientHandler` 和 `RefImplMetadataConvReqHandler` 在參考實現中，瞭解如何處理這些類型的請求的示例。
