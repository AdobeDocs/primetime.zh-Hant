---
title: 升級中繼資料
description: 升級中繼資料
copied-description: true
exl-id: 04b3fb22-489e-41bb-95d0-99375f92fbae
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# 升級中繼資料{#upgrading-metadata}

如果Adobe Access使用者端遇到與Flash MediaRights Management伺服器1.x封裝的內容，它會從內容擷取加密中繼資料，並將其傳送至伺服器。 伺服器會將FMRMS 1.x中繼資料轉換為Adobe存取格式，並傳回給使用者端。 然後，使用者端會在標準Adobe存取授權請求中傳送更新的中繼資料。

* 要求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* 請求URL是&quot;*來自1.x內容的基礎URL*「 +」/flashaccess/headerconversion/v1」。

當伺服器從使用者端接收舊中繼資料時，可以立即完成中繼資料轉換。 或者，伺服器可以預先處理舊內容並儲存轉換過的中繼資料；在這種情況下，當使用者端請求新的中繼資料時，伺服器只需要擷取和舊中繼資料的授權識別碼相符的新中繼資料。

若要轉換中繼資料，伺服器必須執行下列步驟：

* 取得 `LiveCycleKeyMetaData`. 若要預先轉換中繼資料， `LiveCycleKeyMetaData` 可從1.x封裝檔案取得，使用 `MediaEncrypter.examineEncryptedContent()`. 中繼資料也包含在中繼資料轉換請求( `FMRMSv1MetadataHandler.getOriginalMetadata()`)。
* 從舊中繼資料取得授權識別碼，並尋找加密金鑰和原則(此資訊最初在AdobeLiveCycleES資料庫中)。 LiveCycleES原則必須轉換為Adobe存取2.0原則。) 參考實作包括指令碼和範常式式碼，用於轉換原則並從LiveCycleES匯出授權資訊。
* 填入 `V2KeyParameters` 物件（您透過呼叫來擷取） `MediaEncrypter.getKeyParameters()`)。
* 載入 `SigningCredential`，這是由用來簽署加密中繼資料的Adobe所發出的封裝程式認證。 取得 `SignatureParameters` 物件，透過呼叫 `MediaEncrypter.getSignatureParameters()` 並填寫簽署認證。
* 呼叫 `MetaDataConverter.convertMetadata()` 以取得 `V2ContentMetaData`.
* 呼叫 `V2ContentMetaData.getBytes()` 和存放區以供日後使用，或呼叫 `FMRMSv1MetadataHandler.setUpdatedMetadata()`.
