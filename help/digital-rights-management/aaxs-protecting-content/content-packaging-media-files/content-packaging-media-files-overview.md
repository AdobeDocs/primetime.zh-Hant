---
title: 概述
description: 概述
copied-description: true
exl-id: 67c3d98f-8c17-4b5a-8abb-00f6f0f1e823
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# 概述 {#overview}

*包裝* 指對FLV或F4V檔案加密和應用策略的過程。 使用介質打包API來打包檔案。 Adobe訪問Java SDK只能包裝漸進式下載Flash和AIR內容，如FLV、F4V和MP4。 為了使用Adobe訪問DRM對其他內容格式(如AdobeHTTP Dynamic Streaming(HDS)或AppleHTTP即時流(HLS))打包內容，您必須使用其他工具，如Adobe Medium伺服器( [https://www.adobe.com/products/adobe-media-server-family.html](https://www.adobe.com/products/adobe-media-server-family.html))或實現Adobe廣播SDK的編碼器( [https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf](https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf))。 或者，客戶可以選擇使用Adobe的Java Mighide Packager工具集，該工具集可以將內容打包成多種目標格式，如HDS、HLS和DASH。

打包從許可證伺服器中解耦。 打包程式不需要連接到許可證伺服器來交換有關內容的任何資訊。 許可證伺服器為頒發許可證而需要知道的所有資訊都包含在內容元資料中。

當檔案被加密時，如果沒有相應的許可證，則無法分析其內容。 Adobe訪問允許您選擇要加密的檔案的哪些部分。 由於Adobe® Access™可以分析FLV和F4V內容的檔案格式，因此它可以智慧地加密檔案的選擇性部分，而不是整個檔案。 元資料和提示點等資料可以保持未加密狀態，以便搜索引擎仍然可以搜索檔案。

給定內容可能具有多個策略。 例如，如果您希望在不需要多次打包內容的情況下在不同業務模式下對內容進行許可，則此功能可能非常有用。 例如，您可以允許在短時間內匿名訪問，然後允許客戶購買內容並擁有無限的訪問權限。 如果內容使用多個策略打包，則許可證伺服器必須實現邏輯以選擇要用於頒發許可證的策略。

>[!NOTE]
>
>該體系結構允許指定使用策略並在打包內容時將其綁定到內容。 在客戶端可以回放內容之前，客戶端必須獲取該電腦的許可證。 許可證指定強制使用的規則並提供用於解密內容的密鑰。 該策略是用於生成許可證的模板，但許可證伺服器可以選擇在頒發許可證時覆蓋使用規則。 請注意，許可證可能會因到期時間或播放窗口等約束而變為無效。

打包內容時有許多選項。 在 `DRMParameters` 介面和實現該介面的類， `F4VDRMParameters` 和 `FLVDRMParameters`。 通過這些類，您可以設定簽名和密鑰參數，並指示是加密音頻內容、視頻內容還是指令碼資料。 要瞭解這些命令在參考實現中是如何實現的，請參閱中討論的「介質打包器」命令行選項的說明 *使用Adobe訪問參考實現*。 這些選項基於Java API，因此可用於寫程式使用。

打包選項包括：

* 加密選項（音頻、視頻、部分加密）。
* 許可證伺服器URL（客戶端將此URL用作發送到許可證伺服器的所有請求的基本URL）
* 許可證伺服器傳輸證書
* 用於加密CEK的許可證伺服器證書。
* 用於對元資料簽名的打包器憑據

Adobe訪問提供了用於在CEK中傳遞的API。 如果未指定CEK，則SDK會隨機生成它。 通常，您需要為每段內容提供不同的CEK。 但是，在動態流中，您可能會對該內容的所有檔案使用相同的CEK，因此用戶只需要一個許可證，就可以無縫地從一個比特率過渡到另一個比特率。 要對多個內容使用相同的密鑰和許可證，請傳遞相同的密鑰 `DRMParameters` 對象 `MediaEncrypter.encryptContent()`，或在CEK中通過 `V2KeyParameters.setContentEncryptionKey()`。 要對每段內容使用不同的密鑰和許可證，請建立一個新 `DRMParameters` 實例。

使用密鑰輪替對內容進行打包時，可以控制使用的輪替密鑰以及密鑰更改的頻率。 `F4VDRMParameters` 和 `FLVDRMParameters` 執行 `KeyRotationParameters` 。 通過此介面，可以啟用密鑰輪替。 您還需要指定 `RotatingContentEncryptionKeyProvider`。 對於加密的每個示例，此類確定要使用的旋轉密鑰。 您可以實施您自己的提供商，或使用 `TimeBasedKeyProvider` 包含在SDK中。 此實現在指定的秒數後隨機生成新密鑰。

在某些情況下，您可能需要將內容元資料儲存為單獨的檔案，並使其與內容分開提供給客戶端。 為此，請調用 `MediaEncrypter.encryptContent()`，返回 `MediaEncrypterResult` 的雙曲餘切值。 呼叫 `MediaEncrypterResult.getKeyInfo()` 將結果轉為 `V2KeyStatus`。 然後檢索內容元資料並將其儲存在檔案中。

所有這些任務都可使用Java API完成。 有關本章中討論的Java API的詳細資訊，請參見 *Adobe訪問API參考*。

有關介質打包器參考實現的資訊，請參見 *使用Adobe訪問參考實現*。
