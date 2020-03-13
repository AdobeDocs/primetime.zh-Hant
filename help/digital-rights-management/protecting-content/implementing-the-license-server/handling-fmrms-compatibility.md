---
description: 處理FMRMS相容性
seo-description: 處理FMRMS相容性
seo-title: 升級客戶端
title: 升級客戶端
uuid: c32ee087-2edf-4d11-be36-e2b31f3769de
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# 處理FMRMS相容性 {#handling-fmrms-compatibility}

Flash Media Rights Management Server 1.x相容性有兩種要求類型。 一種請求類型可提示1.x用戶端升級至支援Adobe Primetime DRM 2.0或更新版本的執行時期。 另一種是用來在請求授權之前，將1.x中繼資料更新為Primetime DRM格式。 只有當您先前已部署任何使用FMRMS 1.0或1.5的內容時，才需要支援這些請求。

## 升級客戶端 {#upgrading-clients}

如果FMRMS 1.x用戶端連絡Adobe Primetime DRM伺服器，伺服器需要提示用戶端升級。

* 請求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`。
* 請求URL是&quot;*1.x內容的基本URL*&quot; + &quot; [!DNL /edcws/services/urn:EDCLicenseService]&quot;

   與其他Adobe Primetime請求處理常式不同，此處理常式不提供任何請求資訊的存取權，也不要求設定任何回應資料。 建立例項 `FMRMSv1RequestHandler`，然後呼叫 `close()`

## 升級中繼資料 {#upgrading-metadata}

如果Adobe Access用戶端遇到使用Flash Media Rights Management Server 1.x封裝的內容，它會從內容擷取加密中繼資料，並傳送至伺服器。 伺服器會將FMRMS 1.x中繼資料轉換為Adobe Access格式，並傳回給用戶端。 然後，用戶端會在標準Adobe Access授權要求中傳送更新的中繼資料。

* 請求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`。
* 請求URL是「*1.x內容的基本URL*」 +&quot;/flashaccess/headerconversion/v1」。

當伺服器從用戶端接收舊中繼資料時，可即時進行中繼資料轉換。 或者，伺服器可以對舊內容進行預處理，並儲存轉換後的元資料；在這種情況下，當用戶端要求新中繼資料時，伺服器只需要擷取符合舊中繼資料授權識別碼的新中繼資料。

若要轉換中繼資料，伺服器必須執行下列步驟：

* Get `LiveCycleKeyMetaData`. 若要預先轉換中繼資料， `LiveCycleKeyMetaData` 可使用1.x封裝檔案取得 `MediaEncrypter.examineEncryptedContent()`。 中繼資料也包含在中繼資料轉換請求( `FMRMSv1MetadataHandler.getOriginalMetadata()`)中。
* 從舊的中繼資料取得授權識別碼，並尋找加密金鑰和原則（這項資訊原本位於Adobe LiveCycle ES資料庫中）。 LiveCycle ES政策必須轉換為Adobe Access 2.0政策。)「參考實作」包含轉換原則和從LiveCycle ES匯出授權資訊的指令碼和范常式式碼。
* 填寫物 `V2KeyParameters` 件(您透過呼叫擷取 `MediaEncrypter.getKeyParameters()`)。
* 載入 `SigningCredential`Adobe用來簽署加密中繼資料的封裝憑證。 呼叫並 `SignatureParameters` 填寫簽署憑 `MediaEncrypter.getSignatureParameters()` 證，以取得物件。
* 呼叫 `MetaDataConverter.convertMetadata()` 以取得 `V2ContentMetaData`。
* 請電 `V2ContentMetaData.getBytes()` 洽並儲存以供日後使用，或撥打 `FMRMSv1MetadataHandler.setUpdatedMetadata()`。