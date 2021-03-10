---
title: 概觀
description: 概觀
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---


# 概述{#overview}

*封* 裝是指對FLV或F4V檔案加密並套用原則的程式。使用媒體封裝API來封裝檔案。 Adobe存取Java SDK只能封裝漸進式下載Flash和AIR內容，例如FLV、F4V和MP4。 若要使用Adobe存取DRM來封裝其他內容格式的內容，例如AdobeHTTP Dynamic Streaming(HDS)或Apple HTTP Live Streaming(HLS)，您必須使用其他工具，例如Adobe Medium伺服器([https://www.adobe.com/products/adobe-media-server-family.html](https://www.adobe.com/products/adobe-media-server-family.html))或實作Adobe廣播SDK的編碼器([https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf](https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf))。 或者，客戶可以選擇使用Adobe的Java Primetime Packager工具集，此工具集可封裝多種目標格式的內容，例如HDS、HLS和DASH。

封裝會從授權伺服器解除耦合。 套件不需要連線至授權伺服器，就可以交換任何內容相關資訊。 授權伺服器在核發授權時需要知道的一切，都包含在內容中繼資料中。

當檔案加密時，若沒有適當的授權，就無法剖析其內容。 Adobe訪問允許您選擇要加密的檔案的哪些部分。 由於Adobe® Access™可以解析FLV和F4V內容的檔案格式，因此它可以智慧加密檔案的選擇性部分，而不是整個檔案。 中繼資料和提示點等資料可保持未加密，如此搜尋引擎仍可搜尋檔案。

特定內容可能有多個策略。 例如，如果您想要在不同商業模式下授權內容，而不需要多次封裝內容，這可能很有用。 例如，您可以允許短時間的匿名存取，之後允許客戶購買內容並擁有無限存取權。 如果內容使用多個原則封裝，授權伺服器必須實作邏輯，以選擇要用來發佈授權的原則。

>[!NOTE]
>
>該體系結構允許在內容打包時指定使用策略並綁定到內容。 用戶端必須先取得該電腦的授權，才能播放內容。 授權會指定所執行的使用規則，並提供用來解密內容的金鑰。 原則是產生授權的範本，但授權伺服器在發行授權時可選擇覆寫使用規則。 請注意，授權可能會因到期時間或播放視窗等限制而失效。

封裝內容時有許多選項。 這些在`DRMParameters`介面和實現該介面的類中指定，即`F4VDRMParameters`和`FLVDRMParameters`。 您可以透過這些類別來設定簽名和金鑰參數，並指出要加密音訊內容、視訊內容或指令碼資料。 要瞭解這些在參考實施中如何實施，請參閱&#x200B;*使用Adobe訪問參考實施*&#x200B;中討論的Media Packager命令行選項說明。 這些選項是以Java API為基礎，因此可供程式化使用。

封裝選項包括：

* 加密選項（音訊、視訊、部分加密）。
* 授權伺服器URL（用戶端將此URL用作傳送至授權伺服器的所有要求的基本URL）
* 授權伺服器傳輸憑證
* 用於加密CEK的許可證伺服器證書。
* 簽署中繼資料的Packager憑證

Adobe存取提供API以傳入CEK。 如果未指定CEK,SDK會隨機產生它。 通常，您需要針對每個內容使用不同的CEK。 不過，在動態串流中，您可能會針對該內容的所有檔案使用相同的CEK，因此使用者只需要單一授權，而且可以順暢地從一個位元速率轉換到另一個位元速率。 若要對多個內容使用相同的金鑰和授權，請將相同的`DRMParameters`物件傳遞至`MediaEncrypter.encryptContent()`，或使用`V2KeyParameters.setContentEncryptionKey()`傳入CEK。 若要針對每個內容使用不同的金鑰和授權，請為每個檔案建立新的`DRMParameters`例項。

使用索引鍵旋轉封裝內容時，您可以控制使用的「旋轉索引鍵」以及索引鍵變更的頻率。 `F4VDRMParameters` 並實 `FLVDRMParameters` 現該 `KeyRotationParameters` 介面。通過此介面，可以啟用密鑰旋轉。 您還需要指定`RotatingContentEncryptionKeyProvider`。 對於每個加密的示例，此類確定要使用的旋轉密鑰。 您可以實作您自己的提供者，或使用SDK隨附的`TimeBasedKeyProvider`。 此實作會在指定秒數後隨機產生新金鑰。

在某些情況下，您可能需要將內容中繼資料儲存為個別檔案，並將它與內容分開提供給用戶端。 若要這麼做，請叫用`MediaEncrypter.encryptContent()`，它會傳回`MediaEncrypterResult`物件。 呼叫`MediaEncrypterResult.getKeyInfo()`並將結果轉存至`V2KeyStatus`。 然後擷取內容中繼資料，並將它儲存在檔案中。

所有這些工作都可使用Java API完成。 有關本章中討論的Java API的詳細資訊，請參閱&#x200B;*Adobe訪問API參考*。

有關Media Packager參考實作的資訊，請參閱&#x200B;*使用Adobe存取參考實作*。
