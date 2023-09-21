---
title: 封裝媒體檔案概述
description: 封裝媒體檔案概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---

# 概觀 {#packaging-media-files-overview}

封裝是指將DRM政策加密並套用至視訊內容的程式。 您可以使用媒體封裝API來封裝檔案。 Primetime DRM Java SDK只能封裝漸進式下載內容，例如MP4。

>[!NOTE]
>
>請務必聯絡您的Primetime DRM代表，瞭解如何為您的媒體格式和使用案例選取最適合的封裝選項。

封裝會從授權伺服器上解除。 封裝程式不需要連線到授權伺服器來交換任何有關內容的資訊。 授權伺服器簽發授權所需瞭解的一切資訊都會包含在內容中繼資料中。

當檔案被加密時，如果沒有適當的授權，就無法剖析其內容。 您可以使用Primetime DRM來選取您要加密的檔案部分。 由於Primetime DRM可剖析視訊內容的檔案格式，因此可聰明地加密檔案的選擇性部分，而非整個檔案。 中繼資料和提示點等資料可以維持未加密狀態，讓搜尋引擎仍可搜尋檔案。

指定的內容可能有多個DRM原則。 例如，您可以授權不同商業模式下的內容，而無需多次封裝內容。 此外，您可以允許短期匿名存取，然後允許客戶購買內容以擁有無限制的存取權。 如果使用多個DRM原則封裝內容，則License Server必須實作邏輯，以選取必須使用哪個DRM原則來核發許可證。

>[!NOTE]
>
>該架構允許在封裝內容時指定使用DRM原則並將其繫結到內容。 使用者端必須先取得指定電腦的授權，才能播放內容。 授權會指定強制使用的使用規則，並提供解密內容時必須使用的金鑰。 DRM政策代表產生許可證的範本。 但是，當授權伺服器發出授權時，可能會覆寫使用規則。 此類限制（例如到期時間或播放視窗）可能會使授權無效。

Primetime DRM提供用於傳入CEK的API。 如果未指定CEK，SDK會隨機產生它。 通常每個內容區段都需要不同的CEK。 不過，在Dynamic Streaming中，您可能會對組成該內容的所有檔案使用相同的CEK。 因此，使用者只需要單一授權，就能順暢地從一個位元速率轉換到另一個位元速率。 如果您想要針對多個內容片段使用相同的金鑰和授權，您需要傳遞相同的 `DRMParameters` 物件至 `MediaEncrypter.encryptContent()`，或使用在CEK中傳遞 `V2KeyParameters.setContentEncryptionKey()`. 如果您想要針對內容的每個區段使用不同的金鑰和授權，則需要建立新的 `DRMParameters` 每個檔案的執行個體。

使用按鍵旋轉封裝內容時，您可以控制使用的旋轉按鍵以及按鍵變更的頻率。 `F4VDRMParameters` 和 `FLVDRMParameters` 實作 `KeyRotationParameters` 介面。 透過此介面，您可以啟用金鑰輪換。 您也必須指定 `RotatingContentEncryptionKeyProvider`. 針對每個加密的範例，此類別會決定要使用的輪換金鑰。 您可以實作自己的提供者，或使用 `TimeBasedKeyProvider` 包含在SDK中。 此實作會在指定的秒數後隨機產生新金鑰。

在某些情況下，您可能需要將內容中繼資料儲存為個別檔案，並讓使用者端可將其與內容分開使用。 在這種情況下，您需要叫用 `MediaEncrypter.encryptContent()`，會傳回 `MediaEncrypterResult` 物件。 呼叫 `MediaEncrypterResult.getKeyInfo()` 並將結果轉換為 `V2KeyStatus`. 然後擷取內容中繼資料並將其儲存在檔案中。

所有這些工作都可以使用Java API來完成。

另請參閱 *Adobe Primetime DRM API參考* 以取得有關Java API的詳細資料。

另請參閱 *使用Adobe Primetime DRM參考實作* 以瞭解Media Packager參考實作。
