---
description: 處理FMRMS相容性
title: 升級使用者端
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# 處理FMRMS相容性 {#handling-fmrms-compatibility}

與Flash Media Rights Management Server 1.x相容性相關的請求有兩種型別。 有一種型別的請求可用來提示1.x使用者端升級至支援Adobe Primetime DRM 2.0或更新版本的執行階段。 另一個用於將1.x中繼資料更新為Primetime DRM格式，然後才能請求授權。 只有先前已部署使用FMRMS 1.0或1.5的任何內容時，才需要支援這些要求。

## 升級使用者端 {#upgrading-clients}

如果FMRMS 1.x使用者端連絡Adobe Primetime DRM伺服器，伺服器必須提示使用者端進行升級。

* 要求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* 請求URL是&quot;*來自1.x內容的基底URL*「 + 」 [!DNL /edcws/services/urn:EDCLicenseService]&quot;

  不像其他Adobe Primetime要求處理常式，此處理常式不提供任何要求資訊的存取權，或需要設定任何回應資料。 建立例項 `FMRMSv1RequestHandler`，然後呼叫 `close()`

## 升級中繼資料 {#upgrading-metadata}

如果Adobe Access使用者端遇到與Flash MediaRights Management伺服器1.x封裝的內容，它會從內容中擷取加密中繼資料，並將其傳送至伺服器。 伺服器會將FMRMS 1.x中繼資料轉換為Adobe存取格式，並傳回給使用者端。 使用者端接著會以標準Adobe存取授權請求傳送更新的中繼資料。

* 要求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* 請求URL是&quot;*來自1.x內容的基底URL*「 +」/flashaccess/headerconversion/v1」。

當伺服器從使用者端接收舊中繼資料時，可以即時完成中繼資料轉換。 或者，伺服器可以預先處理舊內容並儲存轉換後的中繼資料；在這種情況下，當使用者端請求新的中繼資料時，伺服器只需要擷取和舊中繼資料的授權識別碼相符的新中繼資料。

若要轉換中繼資料，伺服器必須執行下列步驟：

* Get `LiveCycleKeyMetaData`. 若要預先轉換中繼資料， `LiveCycleKeyMetaData` 可使用以下專案從1.x封裝檔案取得： `MediaEncrypter.examineEncryptedContent()`. 中繼資料也包含在中繼資料轉換請求( `FMRMSv1MetadataHandler.getOriginalMetadata()`)。
* 從舊中繼資料取得授權識別碼，並尋找加密金鑰和原則(此資訊最初在AdobeLiveCycleES資料庫中)。 LiveCycleES原則必須轉換為AdobeAccess 2.0原則。) 「參考實作」包含用於轉換原則及從LiveCycleES匯出授權資訊的指令碼和範常式式碼。
* 填入 `V2KeyParameters` 物件（您透過呼叫來擷取） `MediaEncrypter.getKeyParameters()`)。
* 載入 `SigningCredential`，這是由用來簽署加密中繼資料的Adobe所核發的封裝者認證。 取得 `SignatureParameters` 物件，透過呼叫 `MediaEncrypter.getSignatureParameters()` 並填寫簽署認證。
* 呼叫 `MetaDataConverter.convertMetadata()` 若要取得 `V2ContentMetaData`.
* 呼叫 `V2ContentMetaData.getBytes()` 並儲存以供日後使用，或呼叫 `FMRMSv1MetadataHandler.setUpdatedMetadata()`.
