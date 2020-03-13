---
seo-title: 升級中繼資料
title: 升級中繼資料
uuid: 769483e6-a2d1-46cb-afcf-557aa807037c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 升級中繼資料{#upgrading-metadata}

如果Adobe Primetime DRM用戶端遇到與Flash Media Rights Management Server 1.x封裝的內容，它會從內容擷取加密中繼資料並傳送至伺服器。 然後，伺服器將FMRMS 1.x元資料轉換為Primetime DRM格式，並將其發送到客戶端。 然後，客戶端在標準Primetime DRM許可請求中發送更新的元資料。

* 請求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`。
* 請求URL是「*1.x內容的基本URL*」 + [!DNL /flashaccess/headerconversion/v1]」。

當伺服器從用戶端接收舊中繼資料時，可即時進行中繼資料轉換。 或者，伺服器可以對舊內容進行預處理，並儲存轉換後的元資料；在這種情況下，當用戶端要求新中繼資料時，伺服器只需要擷取符合舊中繼資料授權識別碼的新中繼資料。

若要轉換中繼資料，伺服器必須執行下列步驟：

* Get `LiveCycleKeyMetaData`. 若要預先轉換中繼資料， `LiveCycleKeyMetaData` 可使用1.x封裝檔案取得 `MediaEncrypter.examineEncryptedContent()`。 中繼資料也包含在中繼資料轉換請求( `FMRMSv1MetadataHandler.getOriginalMetadata()`)中。

* 從舊的中繼資料取得授權識別碼，並尋找加密金鑰和DRM原則（這項資訊原本位於Adobe LiveCycle ES資料庫中）。 LiveCycle ES DRM政策必須轉換為Primetime DRM 2.0 DRM政策。)「參考實作」包含轉換DRM原則和從LiveCycle ES匯出授權資訊的指令碼和范常式式碼。
* 填寫物 `V2KeyParameters` 件(您透過呼叫擷取 `MediaEncrypter.getKeyParameters()`)。

* 載入 `SigningCredential`Adobe用來簽署加密中繼資料的封裝憑證。 呼叫並 `SignatureParameters` 填寫簽署憑 `MediaEncrypter.getSignatureParameters()` 證，以取得物件。

* 呼叫 `MetaDataConverter.convertMetadata()` 以取得 `V2ContentMetaData`。

* 請電 `V2ContentMetaData.getBytes()` 洽並儲存以供日後使用，或撥打 `FMRMSv1MetadataHandler.setUpdatedMetadata()`。

