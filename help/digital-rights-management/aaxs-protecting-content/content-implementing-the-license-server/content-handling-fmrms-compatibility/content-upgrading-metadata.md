---
title: 升級元資料
description: 升級元資料
copied-description: true
exl-id: 04b3fb22-489e-41bb-95d0-99375f92fbae
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# 升級元資料{#upgrading-metadata}

如果Adobe訪問客戶端遇到與Flash媒體Rights Management伺服器1.x打包的內容，它將從內容中提取加密元資料並將其發送到伺服器。 伺服器將將FMRMS 1.x元資料轉換為Adobe訪問格式，並將其發回到客戶端。 然後，客戶機在標準Adobe訪問許可請求中發送更新的元資料。

* 請求處理程式類為 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`。
* 請求URL為「」*1.x內容的基URL*&quot; +&quot;/flashaccess/headerconversion/v1&quot;。

當伺服器從客戶端接收舊元資料時，可以即時執行元資料轉換。 或者，伺服器可以對舊內容進行預處理並儲存轉換後的元資料；在這種情況下，當客戶端請求新元資料時，伺服器只需要獲取與舊元資料的許可證標識符匹配的新元資料。

要轉換元資料，伺服器必須執行以下步驟：

* 獲取 `LiveCycleKeyMetaData`。 要預轉換元資料， `LiveCycleKeyMetaData` 可從1.x封裝檔案中使用 `MediaEncrypter.examineEncryptedContent()`。 元資料也包含在元資料轉換請求中( `FMRMSv1MetadataHandler.getOriginalMetadata()`)。
* 從舊元資料中獲取許可證標識符，並查找加密密鑰和策略(此資訊最初位於AdobeLiveCycleES資料庫中。 必須將LiveCycleES策略轉換為Adobe訪問2.0策略。) 參考實施包括用於轉換策略和從LiveCycleES導出許可證資訊的指令碼和示例代碼。
* 填寫 `V2KeyParameters` 對象(通過調用 `MediaEncrypter.getKeyParameters()`)。
* 載入 `SigningCredential`，是Adobe頒發的用於簽名加密元資料的打包器憑據。 獲取 `SignatureParameters` 調用對象 `MediaEncrypter.getSignatureParameters()` 並填寫簽名憑據。
* 呼叫 `MetaDataConverter.convertMetadata()` 獲取 `V2ContentMetaData`。
* 呼叫 `V2ContentMetaData.getBytes()` 並儲存供將來使用或呼叫 `FMRMSv1MetadataHandler.setUpdatedMetadata()`。
