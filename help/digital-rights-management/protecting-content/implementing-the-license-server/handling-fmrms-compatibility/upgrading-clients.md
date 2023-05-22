---
description: 與Flash媒體Rights Management伺服器1.x相容性相關的請求有兩種類型。 一種請求類型用於提示1.x客戶端升級到支援Adobe PrimetimeDRM 2.0或更高版本的運行時。 另一個用於在可請求許可之前將1.x元資料更新為黃金時段DRM格式。 只有在您以前部署了使用FMRMS 1.0或1.5的任何內容時，才需要支援這些請求。
title: 處理FMRMS相容性
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---


# 處理FMRMS相容性 {#handling-fmrms-compatibility}

與Flash媒體Rights Management伺服器1.x相容性相關的請求有兩種類型。 一種請求類型用於提示1.x客戶端升級到支援Adobe PrimetimeDRM 2.0或更高版本的運行時。 另一個用於在可請求許可之前將1.x元資料更新為黃金時段DRM格式。 只有在您以前部署了使用FMRMS 1.0或1.5的任何內容時，才需要支援這些請求。

## 升級客戶端 {#upgrading-clients}

如果FMRMS 1.x客戶端與Adobe PrimetimeDRM伺服器聯繫，則伺服器需要提示客戶端升級。

* 請求處理程式類為 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`。
* 請求URL為「」*1.x內容的基URL*&quot; + &quot; [!DNL /edcws/services/urn:EDCLicenseService]&quot;

   與其他Adobe Primetime請求處理程式不同，此處理程式不提供對任何請求資訊的訪問，也不要求設定任何響應資料。 建立實例 `FMRMSv1RequestHandler`，然後調用 `close()`

## 升級元資料 {#upgrading-metadata}

如果Adobe PrimetimeDRM客戶端遇到與Flash媒體Rights Management伺服器1.x打包的內容，則它從內容中提取加密元資料並將其發送到伺服器。 然後，伺服器將FMRMS 1.x元資料轉換為黃金時段DRM格式，並將其發送到客戶端。 然後，客戶端在標準黃金時段DRM許可請求中發送更新的元資料。

* 請求處理程式類為 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`。
* 請求URL為「」*1.x內容的基URL*&quot; +&quot; [!DNL /flashaccess/headerconversion/v1]。

當伺服器從客戶端接收舊元資料時，可以即時執行元資料轉換。 或者，伺服器可以對舊內容進行預處理並儲存轉換後的元資料；在這種情況下，當客戶端請求新元資料時，伺服器只需要獲取與舊元資料的許可證標識符匹配的新元資料。

要轉換元資料，伺服器必須執行以下步驟：

* 獲取 `LiveCycleKeyMetaData`。 要預轉換元資料， `LiveCycleKeyMetaData` 可從1.x封裝檔案中使用 `MediaEncrypter.examineEncryptedContent()`。 元資料也包含在元資料轉換請求中( `FMRMSv1MetadataHandler.getOriginalMetadata()`)。

* 從舊元資料中獲取許可證標識符，並查找加密密鑰和DRM策略(此資訊最初位於AdobeLiveCycleES資料庫中。 LiveCycleES DRM策略必須轉換為Mighine DRM 2.0 DRM策略。) 參考實現包括用於轉換DRM策略和從LiveCycleES導出許可證資訊的指令碼和示例代碼。
* 填寫 `V2KeyParameters` 對象(通過調用 `MediaEncrypter.getKeyParameters()`)。

* 載入 `SigningCredential`，是Adobe頒發的用於簽名加密元資料的打包器憑據。 獲取 `SignatureParameters` 調用對象 `MediaEncrypter.getSignatureParameters()` 並填寫簽名憑據。

* 呼叫 `MetaDataConverter.convertMetadata()` 獲取 `V2ContentMetaData`。

* 呼叫 `V2ContentMetaData.getBytes()` 並儲存供將來使用或呼叫 `FMRMSv1MetadataHandler.setUpdatedMetadata()`。