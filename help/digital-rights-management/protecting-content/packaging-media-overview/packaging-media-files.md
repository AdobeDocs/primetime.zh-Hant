---
title: 打包媒體檔案概述
description: 打包媒體檔案概述
copied-description: true
exl-id: 88c593a7-33b5-4773-b283-2ab16f9e8c3a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---

# 概述 {#packaging-media-files-overview}

打包是指對視頻內容加密和應用DRM策略的過程。 可以使用介質打包API來打包檔案。 Mighide DRM Java SDK只能包裝漸進式下載內容，如MP4。

>[!NOTE]
>
>請務必聯繫您的Mighine DRM代表，瞭解如何為您的媒體格式和使用案例選擇最合適的打包選項。

打包從許可證伺服器中解耦。 打包程式不需要連接到許可證伺服器來交換有關內容的任何資訊。 許可證伺服器在頒發許可證時需要知道的所有內容都包含在內容元資料中。

當檔案被加密時，如果沒有相應的許可證，則無法分析其內容。 可以使用Mogfi時DRM來選取要加密的檔案的部分。 由於Mighide DRM能夠分析視頻內容的檔案格式，因此它可以智慧地加密檔案的選擇性部分而不是整個檔案。 資料（如元資料和提示點）可保持未加密狀態，以便搜索引擎仍可搜索檔案。

指定的內容段可以具有多個DRM策略。 例如，您可以在不同業務模式下許可內容，而無需多次打包內容。 此外，您還可以允許短時間的匿名訪問，然後允許客戶購買內容以具有無限的訪問權限。 如果使用多個DRM策略打包內容，則許可證伺服器必須實現邏輯以選擇必須使用哪個DRM策略來頒發許可證。

>[!NOTE]
>
>該體系結構允許當內容打包時指定使用DRM策略並綁定到內容。 在客戶端可以回放內容之前，客戶端必須獲取指定電腦的許可證。 許可證指定強制使用的規則，並提供必須用於解密內容的密鑰。 DRM策略表示用於生成許可證的模板。 但是，當許可證伺服器發出許可證時，它可以覆蓋使用規則。 許可證可由諸如到期時間或回放窗口等約束而變為無效。

黃金時段DRM提供用於在CEK中傳遞的API。 如果未指定CEK，則SDK會隨機生成它。 通常，您需要為每個內容部分提供不同的CEK。 但是，在動態流中，您可能會對構成該內容的所有檔案使用相同的CEK。 因此，用戶只需一個許可證即可從一個比特率無縫過渡到另一個比特率。 如果希望對多個內容使用相同的密鑰和許可證，則需要傳遞相同的密鑰和許可證 `DRMParameters` 對象 `MediaEncrypter.encryptContent()`，或在CEK中通過 `V2KeyParameters.setContentEncryptionKey()`。 如果要為內容的每個部分使用不同的密鑰和許可證，則需要建立新的 `DRMParameters` 實例。

使用密鑰旋轉對內容進行打包時，可以控制使用的旋轉密鑰以及密鑰更改的頻率。 `F4VDRMParameters` 和 `FLVDRMParameters` 執行 `KeyRotationParameters` 。 通過此介面，可以啟用密鑰輪替。 您還需要指定 `RotatingContentEncryptionKeyProvider`。 對於加密的每個示例，此類確定要使用的旋轉密鑰。 您可以實施您自己的提供商，或使用 `TimeBasedKeyProvider` 包含在SDK中。 此實現在指定的秒數後隨機生成新密鑰。

在某些情況下，您可能需要將內容元資料儲存為單獨的檔案，並使其與內容分開提供給客戶端。 在這種情況下，你需要 `MediaEncrypter.encryptContent()`，返回 `MediaEncrypterResult` 的雙曲餘切值。 呼叫 `MediaEncrypterResult.getKeyInfo()` 將結果轉為 `V2KeyStatus`。 然後檢索內容元資料並將其儲存在檔案中。

所有這些任務都可通過Java API完成。

請參閱 *Adobe PrimetimeDRM API參考* 的子菜單。

請參閱 *使用Adobe PrimetimeDRM參考實現* 有關介質打包器參考實現的資訊。
