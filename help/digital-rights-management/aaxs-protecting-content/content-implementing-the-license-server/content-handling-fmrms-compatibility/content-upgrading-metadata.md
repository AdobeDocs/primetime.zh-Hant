---
seo-title: 升級中繼資料
title: 升級中繼資料
uuid: cad0b23e-50ca-47ae-871f-be571cb00a26
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---


# 升級元資料{#upgrading-metadata}

如果Adobe Access用戶端遇到使用Flash Media Rights Management Server 1.x封裝的內容，它會從內容擷取加密中繼資料，並傳送至伺服器。 伺服器會將FMRMS 1.x中繼資料轉換為Adobe Access格式，並傳回給用戶端。 然後，用戶端會在標準Adobe Access授權要求中傳送更新的中繼資料。

* 請求處理常式類別為`com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`。
* 請求URL是&quot;*來自1.x content*&quot; +&quot;/flashaccess/headerconversion/v1&quot;的基本URL。

當伺服器從用戶端接收舊中繼資料時，可即時進行中繼資料轉換。 或者，伺服器可以對舊內容進行預處理，並儲存轉換後的元資料；在這種情況下，當用戶端要求新中繼資料時，伺服器只需要擷取符合舊中繼資料授權識別碼的新中繼資料。

若要轉換中繼資料，伺服器必須執行下列步驟：

* 獲取`LiveCycleKeyMetaData`。 若要預先轉換中繼資料，可使用`MediaEncrypter.examineEncryptedContent()`從1.x封裝檔案取得`LiveCycleKeyMetaData`。 中繼資料也包含在中繼資料轉換請求(`FMRMSv1MetadataHandler.getOriginalMetadata()`)中。
* 從舊的中繼資料取得授權識別碼，並尋找加密金鑰和原則（這項資訊原本位於Adobe LiveCycle ES資料庫中）。 LiveCycle ES政策必須轉換為Adobe Access 2.0政策。) 「參考實作」包含轉換原則和從LiveCycle ES匯出授權資訊的指令碼和范常式式碼。
* 填寫`V2KeyParameters`物件（您透過呼叫`MediaEncrypter.getKeyParameters()`來擷取）。
* 載入`SigningCredential`，此為Adobe用來簽署加密中繼資料的封裝憑證。 呼叫`MediaEncrypter.getSignatureParameters()`並填寫簽署憑證，以取得`SignatureParameters`物件。
* 呼叫`MetaDataConverter.convertMetadata()`以取得`V2ContentMetaData`。
* 呼叫`V2ContentMetaData.getBytes()`並儲存以供日後使用，或呼叫`FMRMSv1MetadataHandler.setUpdatedMetadata()`。

