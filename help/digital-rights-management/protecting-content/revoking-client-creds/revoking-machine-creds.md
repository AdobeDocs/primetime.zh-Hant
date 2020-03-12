---
seo-title: 廢止機器認證
title: 廢止機器認證
uuid: 3647c843-5f1a-457e-949d-10a6278b1c29
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 廢止機器認證 {#revoking-machine-credentials}

Adobe會維護CRL，以廢止已知受到危害的機器認證。 此CRL由SDK自動執行。 如果您不希望您的授權伺服器核發授權的其他電腦，您可以建立電腦撤銷清單並新增您要排除的電腦Token的發行者名稱和序號（用於擷取電腦憑證的發行者名稱和序號）。 `MachineToken.getMachineTokenId()`

撤消電腦憑據涉及對象的 `RevocationListFactory` 使用。 若要建立撤銷清單、載入現有的撤銷清單，並檢查使用Java API是否已撤銷機器Token，請執行下列步驟：

1. 設定您的開發環境，並將「設定開發環境」中提 [及的所有JAR檔案包括在項目](../../protecting-content/setting-up-the-sdk/setup-dev-env.md) 中。
1. 建立 `ServerCredentialFactory` 例項以載入簽署所需的認證。 許可證伺服器憑證用於簽署撤銷清單。
1. 建立例 `RevocationListFactory` 項。
1. 指定使用物件所要撤銷之機器Token的發行者和序 `IssuerAndSerialNumber` 號。 所有Adobe Primetime DRM請求都包含機器Token。
1. 使用您 `RevocationList` 剛建立的物 `IssuerAndSerialNumber` 件建立物件，並將它傳入到撤銷清單中 `RevocationListFactory.addRevocationEntry()`。 透過呼叫產生新的撤銷清單 `RevocationListFactory.generateRevocationList()`。

1. 若要儲存撤銷清單，您可以透過呼叫將其序列化 `RevocationList.getBytes()`。 若要載入清單，請呼 `RevocationListFactory.loadRevocationList()` 叫並傳入序號清單。

1. 透過呼叫，確認簽名有效且清單已由正確的授權伺服器簽署 `RevocationList.verifySignature()`。
1. 要檢查條目是否已撤銷，請將對象 `IssuerAndSerialNumber` 傳遞到 `RevocationList.isRevoked()`。 此外，也可將撤銷清單傳入， `HandlerConfiguration` 讓SDK對所有驗證和授權要求執行撤銷清單。

若要新增其他項目至現有的 `RevocationList`撤銷清單，請載入現有的撤銷清單。 建立新 `RevocationListFactory` 實例，並確保增加CRL編號。 呼 `RevocationListFactioryEntries.addRevocationEntries` 叫將舊清單中的所有條目添加到新清單中。 呼 `RevocationListFactory.addRevocationEntry` 叫將任何新的撤銷項目新增至RevocationList。

如需示範如何建立撤銷清單、載入現有的撤銷清單以及檢查機器Token是否已撤銷的范常式式碼，請參 `com.adobe.flashaccess.samples.revocation.CreateRevocationList` 閱參考實作命令列工具目 [!DNL samples] 錄。
