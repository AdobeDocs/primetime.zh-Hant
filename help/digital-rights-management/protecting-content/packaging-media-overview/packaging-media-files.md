---
title: 封裝媒體檔案概觀
description: 封裝媒體檔案概觀
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---


# 概述{#packaging-media-files-overview}

封裝是指對視訊內容加密和套用DRM原則的程式。 您可以使用媒體封裝API來封裝檔案。 Primetime DRM Java SDK只能封裝漸進式下載內容，例如MP4。

>[!NOTE]
>
>請務必連絡您的Primetime DRM代表，瞭解如何針對您的媒體格式和使用案例選擇最適合的封裝選項。

封裝會從授權伺服器解除耦合。 套件不需要連線至授權伺服器，就可以交換任何內容相關資訊。 授權伺服器在核發授權時需要知道的一切，都包含在內容中繼資料中。

當檔案加密時，若沒有適當的授權，就無法剖析其內容。 您可以使用Primetime DRM來選擇要加密的檔案部分。 由於Primetime DRM可以解析視頻內容的檔案格式，因此它可以智慧地加密檔案的選擇性部分而不是整個檔案。 資料（例如中繼資料和提示點）可保持未加密，如此搜尋引擎仍可搜尋檔案。

指定的內容片段可以具有多個DRM策略。 例如，您可以在不同商業模式下授權內容，而不需要多次封裝內容。 此外，您也可以在短時間內允許匿名存取，然後允許客戶購買內容以擁有無限存取權。 如果內容是使用多個DRM原則封裝的，授權伺服器必須實作邏輯，以選擇必須使用哪些DRM原則來發佈授權。

>[!NOTE]
>
>該體系結構允許在內容打包時指定使用DRM策略並將其綁定到內容。 用戶端必須先取得指定電腦的授權，才能播放內容。 授權會指定所執行的使用規則，並提供必須用來解密內容的金鑰。 DRM策略表示用於生成許可證的模板。 不過，授權伺服器在發行授權時可能會覆寫使用規則。 授權可能因此類限制而無效，例如過期時間或播放視窗。

Primetime DRM提供用於傳入CEK的API。 如果未指定CEK,SDK會隨機產生它。 通常，您需要針對每個內容區段使用不同的CEK。 不過，在動態串流中，您可能會針對構成該內容的所有檔案使用相同的CEK。 因此，使用者只需要單一授權，即可順暢地從一個位元速率轉換至另一個位元速率。 如果您想要針對多個內容使用相同的金鑰和授權，您需要將相同的`DRMParameters`物件傳遞至`MediaEncrypter.encryptContent()`，或使用`V2KeyParameters.setContentEncryptionKey()`傳入CEK。 如果您想要針對每個內容區段使用不同的金鑰和授權，則必須為每個檔案建立新的`DRMParameters`例項。

當您使用按鍵旋轉封裝內容時，可以控制使用的旋轉按鍵和按鍵變更的頻率。 `F4VDRMParameters` 並實 `FLVDRMParameters` 現該 `KeyRotationParameters` 介面。通過此介面，可以啟用密鑰旋轉。 您還需要指定`RotatingContentEncryptionKeyProvider`。 對於每個加密的示例，此類確定要使用的旋轉密鑰。 您可以實作您自己的提供者，或使用SDK隨附的`TimeBasedKeyProvider`。 此實作會在指定秒數後隨機產生新金鑰。

在某些情況下，您可能需要將內容中繼資料儲存為個別檔案，並將它與內容分開提供給用戶端。 在這種情況下，您需要調用`MediaEncrypter.encryptContent()` ，它返回`MediaEncrypterResult`對象。 呼叫`MediaEncrypterResult.getKeyInfo()`並將結果轉存至`V2KeyStatus`。 然後擷取內容中繼資料，並將它儲存在檔案中。

所有這些工作都可使用Java API完成。

如需Java API的詳細資訊，請參閱&#x200B;*Adobe PrimetimeDRM API參考*。

有關Media Packager參考實作的資訊，請參閱&#x200B;*使用Adobe PrimetimeDRM參考實作*。
