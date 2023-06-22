---
title: 升級中繼資料
description: 升級中繼資料
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# 升級中繼資料{#upgrading-metadata}

如果Adobe Primetime DRM使用者端遇到與Flash MediaRights Management伺服器1.x封裝的內容，便會從內容中擷取加密中繼資料，並將其傳送至伺服器。 然後，伺服器會將FMRMS 1.x中繼資料轉換為Primetime DRM格式並傳送給使用者端。 然後，使用者端會以標準Primetime DRM授權請求傳送更新的中繼資料。

* 要求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* 請求URL是&quot;*來自1.x內容的基礎URL*「 +」 [!DNL /flashaccess/headerconversion/v1]「。

當伺服器從使用者端接收舊中繼資料時，可以立即完成中繼資料轉換。 或者，伺服器可以預先處理舊內容並儲存轉換過的中繼資料；在這種情況下，當使用者端請求新的中繼資料時，伺服器只需要擷取和舊中繼資料的授權識別碼相符的新中繼資料。

若要轉換中繼資料，伺服器必須執行下列步驟：

* 取得 `LiveCycleKeyMetaData`. 若要預先轉換中繼資料， `LiveCycleKeyMetaData` 可從1.x封裝檔案取得，使用 `MediaEncrypter.examineEncryptedContent()`. 中繼資料也包含在中繼資料轉換請求( `FMRMSv1MetadataHandler.getOriginalMetadata()`)。

* 從舊的中繼資料取得授權識別碼，並尋找加密金鑰和DRM原則(此資訊最初是在AdobeLiveCycleES資料庫中)。 LiveCycleES DRM政策必須轉換為Primetime DRM 2.0 DRM政策)。 「參考實作」包含用於轉換DRM原則和從LiveCycleES匯出許可證資訊的指令碼和範常式式碼。
* 填入 `V2KeyParameters` 物件（您透過呼叫來擷取） `MediaEncrypter.getKeyParameters()`)。

* 載入 `SigningCredential`，這是由用來簽署加密中繼資料的Adobe所發出的封裝程式認證。 取得 `SignatureParameters` 物件，透過呼叫 `MediaEncrypter.getSignatureParameters()` 並填寫簽署認證。

* 呼叫 `MetaDataConverter.convertMetadata()` 以取得 `V2ContentMetaData`.

* 呼叫 `V2ContentMetaData.getBytes()` 和存放區以供日後使用，或呼叫 `FMRMSv1MetadataHandler.setUpdatedMetadata()`.

