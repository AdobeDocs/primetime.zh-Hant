---
description: 與Flash介質Rights Management伺服器1.x相容性相關的請求有兩種類型。 一種請求類型用於提示1.x用戶端升級至支援Adobe PrimetimeDRM 2.0或更新版本的執行時期。 另一種是用來在請求授權之前，將1.x中繼資料更新為Primetime DRM格式。 只有當您先前已部署任何使用FMRMS 1.0或1.5的內容時，才需要支援這些請求。
title: 處理FMRMS相容性
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---


# 處理FMRMS相容性{#handling-fmrms-compatibility}

與Flash介質Rights Management伺服器1.x相容性相關的請求有兩種類型。 一種請求類型用於提示1.x用戶端升級至支援Adobe PrimetimeDRM 2.0或更新版本的執行時期。 另一種是用來在請求授權之前，將1.x中繼資料更新為Primetime DRM格式。 只有當您先前已部署任何使用FMRMS 1.0或1.5的內容時，才需要支援這些請求。

## 升級客戶端{#upgrading-clients}

如果FMRMS 1.x客戶端與Adobe PrimetimeDRM伺服器聯繫，則伺服器需要提示客戶端升級。

* 請求處理常式類別為`com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`。
* 請求URL是&quot;*1.x content*&quot; + &quot; [!DNL /edcws/services/urn:EDCLicenseService]&quot;的基本URL

   與其他Adobe Primetime請求處理常式不同，此處理常式不提供任何請求資訊的存取權，也不要求設定任何回應資料。 建立`FMRMSv1RequestHandler`的例項，然後呼叫`close()`

## 升級元資料{#upgrading-metadata}

如果Adobe PrimetimeDRM客戶端遇到與Flash媒體Rights Management伺服器1.x打包的內容，則它從內容中提取加密元資料並將其發送到伺服器。 然後，伺服器將FMRMS 1.x元資料轉換為Primetime DRM格式，並將其發送到客戶端。 然後，客戶端在標準Primetime DRM許可請求中發送更新的元資料。

* 請求處理常式類別為`com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`。
* 請求URL是&quot;*1.x content*&quot; +&quot; [!DNL /flashaccess/headerconversion/v1]&quot;的基本URL。

當伺服器從用戶端接收舊中繼資料時，可即時進行中繼資料轉換。 或者，伺服器可以對舊內容進行預處理，並儲存轉換後的元資料；在這種情況下，當用戶端要求新中繼資料時，伺服器只需要擷取符合舊中繼資料授權識別碼的新中繼資料。

若要轉換中繼資料，伺服器必須執行下列步驟：

* 獲取`LiveCycleKeyMetaData`。 若要預先轉換中繼資料，可使用`MediaEncrypter.examineEncryptedContent()`從1.x封裝檔案取得`LiveCycleKeyMetaData`。 中繼資料也包含在中繼資料轉換請求(`FMRMSv1MetadataHandler.getOriginalMetadata()`)中。

* 從舊的中繼資料取得授權識別碼，並尋找加密金鑰和DRM原則(此資訊原本位於AdobeLiveCycleES資料庫中)。 LiveCycleES DRM策略必須轉換為Primetime DRM 2.0 DRM策略。) 「參考實施」包括用於轉換DRM策略和從LiveCycleES導出許可資訊的指令碼和示例代碼。
* 填寫`V2KeyParameters`物件（您透過呼叫`MediaEncrypter.getKeyParameters()`來擷取）。

* 載入`SigningCredential`，該是用於簽署加密元資料的Adobe頒發的打包憑據。 呼叫`MediaEncrypter.getSignatureParameters()`並填寫簽署憑證，以取得`SignatureParameters`物件。

* 呼叫`MetaDataConverter.convertMetadata()`以取得`V2ContentMetaData`。

* 呼叫`V2ContentMetaData.getBytes()`並儲存以供日後使用，或呼叫`FMRMSv1MetadataHandler.setUpdatedMetadata()`。