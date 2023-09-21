---
title: 概觀
description: 概觀
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# 概觀 {#overview}

*封裝* 是指加密原則並將其套用至FLV或F4V檔案的過程。 使用媒體封裝API來封裝檔案。 Adobe存取Java SDK只能封裝漸進式下載Flash和AIR內容，例如FLV、F4V和MP4。 若要針對其他內容格式(例如AdobeHTTP Dynamic Streaming(HDS)或Apple HTTP Live Streaming (HLS))使用Adobe存取DRM來封裝內容，您必須使用其他工具，例如Adobe Media Server( [https://www.adobe.com/products/adobe-media-server-family.html](https://www.adobe.com/products/adobe-media-server-family.html))或實作Adobe廣播SDK的編碼器( [https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf](https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf))。 或者，客戶可以選擇使用Adobe的Java Primetime Packager工具集，該工具集可以封裝各種目標格式（例如HDS、HLS和DASH）的內容。

封裝會從授權伺服器上解除。 封裝程式不需要連線到授權伺服器來交換任何有關內容的資訊。 授權伺服器發行授權所需瞭解的一切資訊都會包含在內容中繼資料中。

當檔案被加密時，如果沒有適當的授權，就無法剖析其內容。 Adobe存取可讓您選取要加密的檔案部分。 由於Adobe® Access™可剖析FLV和F4V內容的檔案格式，因此可聰明地加密檔案的選擇性部分，而非整個檔案。 中繼資料和提示點等資料可以維持未加密，讓搜尋引擎仍可搜尋檔案。

特定內容可能擁有多個原則。 例如，如果您想要在不同商業模式下授權內容，而不需要多次封裝內容，這將很有用。 例如，您可以允許匿名存取一段短時間，之後客戶可以購買內容並擁有無限的存取權。 如果使用多個原則封裝內容，則License Server必須實作邏輯，以選取要用來發行授權的原則。

>[!NOTE]
>
>此架構允許在封裝內容時指定使用原則並將其繫結至內容。 使用者端必須取得該電腦的授權，才能播放內容。 授權會指定強制使用的使用規則，並提供用來解密內容的金鑰。 原則是用於產生授權的範本，但授權伺服器可能會選擇在發行授權時覆寫使用規則。 請注意，許可證可能會因為到期時間或播放視窗等限制而變成無效。

封裝內容時，有多種選項可供選擇。 這些在 `DRMParameters` 介面和實作該介面的類別，也就是 `F4VDRMParameters` 和 `FLVDRMParameters`. 使用這些類別，您可以設定簽名和金鑰引數，以及指示是否要加密音訊內容、視訊內容或指令碼資料。 若要檢視如何在參考實作中實作這些專案，請參閱中討論的「媒體封裝器」命令列選項說明 *使用Adobe存取參考實作*. 這些選項是以Java API為基礎，因此可用於程式設計使用。

封裝選項包括：

* 加密選項（音訊、視訊、部分加密）。
* 授權伺服器URL （使用者端會使用此URL作為傳送給授權伺服器之所有要求的基底URL）
* 授權伺服器傳輸憑證
* 授權伺服器憑證，用於加密CEK。
* 用於簽署中繼資料的封裝程式認證

Adobe存取提供用於在CEK中傳遞的API。 如果未指定CEK，SDK會隨機產生它。 通常每個內容片段都需要不同的CEK。 不過，在Dynamic Streaming中，您可能會針對該內容的所有檔案使用相同的CEK，因此使用者只需要單一授權，且可以從一個位元速率順暢轉換到另一個位元速率。 若要針對多個內容片段使用相同的金鑰和授權，請傳遞相同的 `DRMParameters` 物件至 `MediaEncrypter.encryptContent()`，或使用在CEK中傳遞 `V2KeyParameters.setContentEncryptionKey()`. 若要對每個內容使用不同的金鑰和授權，請建立新的 `DRMParameters` 每個檔案的執行個體。

使用金鑰輪換來封裝內容時，您可以控制使用的輪換金鑰以及金鑰變更的頻率。 `F4VDRMParameters` 和 `FLVDRMParameters` 實作 `KeyRotationParameters` 介面。 透過此介面，您可以啟用金鑰輪換。 您也必須指定 `RotatingContentEncryptionKeyProvider`. 針對每個加密的範例，此類別會決定要使用的輪換金鑰。 您可以實作自己的提供者，或使用 `TimeBasedKeyProvider` 包含在SDK中。 此實作會在指定的秒數後隨機產生新金鑰。

在某些情況下，您可能需要將內容中繼資料儲存為個別檔案，並讓使用者端可將其與內容分開使用。 若要這麼做，請叫用 `MediaEncrypter.encryptContent()`，會傳回 `MediaEncrypterResult` 物件。 呼叫 `MediaEncrypterResult.getKeyInfo()` 並將結果轉換為 `V2KeyStatus`. 然後擷取內容中繼資料並將其儲存在檔案中。

所有這些工作都可以使用Java API來完成。 如需本章所述Java API的詳細資訊，請參閱 *Adobe存取API參考*.

如需Media Packager參考實作的相關資訊，請參閱 *使用Adobe存取參考實作*.
