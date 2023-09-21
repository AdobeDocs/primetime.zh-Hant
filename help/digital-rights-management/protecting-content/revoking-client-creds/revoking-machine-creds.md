---
title: 正在撤銷電腦認證
description: 正在撤銷電腦認證
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# 正在撤銷電腦認證 {#revoking-machine-credentials}

Adobe會維護一個CRL，用於撤銷已知會遭到入侵的電腦認證。 SDK會自動強制執行此CRL。 如果有其他您不希望授權伺服器發行授權的電腦，您可以建立電腦撤銷清單，並新增要排除的電腦權杖的簽發者名稱和序號(使用 `MachineToken.getMachineTokenId()` 擷取電腦憑證的簽發者名稱和序號)。

撤銷電腦認證涉及使用 `RevocationListFactory` 物件。 若要建立撤銷清單，請載入現有的撤銷清單，然後使用Java API檢查電腦權杖是否已撤銷，請執行以下步驟：

1. 設定您的開發環境，並包含中提到的所有JAR檔案 [設定開發環境](../../protecting-content/setting-up-the-sdk/setup-dev-env.md) 在您的專案中。
1. 建立 `ServerCredentialFactory` 執行個體以載入簽署所需的認證。 授權伺服器認證可用來簽署撤銷清單。
1. 建立 `RevocationListFactory` 執行個體。
1. 指定要透過使用撤銷之電腦權杖的簽發者和序號 `IssuerAndSerialNumber` 物件。 所有Adobe Primetime DRM請求都包含機器權杖。
1. 建立 `RevocationList` 物件使用 `IssuerAndSerialNumber` 您剛建立的物件，並將其傳遞至以新增至撤銷清單 `RevocationListFactory.addRevocationEntry()`. 呼叫，產生新的撤銷清單 `RevocationListFactory.generateRevocationList()`.

1. 若要儲存撤銷清單，您可以呼叫 `RevocationList.getBytes()`. 若要載入清單，請呼叫 `RevocationListFactory.loadRevocationList()` 並在序列化清單中傳遞。

1. 透過呼叫，驗證簽章是否有效，以及清單是否由正確的授權伺服器簽署 `RevocationList.verifySignature()`.
1. 若要檢查專案是否已撤銷，請傳遞 `IssuerAndSerialNumber` 物件移入 `RevocationList.isRevoked()`. 撤銷清單也可傳遞至 `HandlerConfiguration` 讓SDK強制所有驗證和授權要求的撤銷清單。

若要將其他專案新增至現有專案，請執行下列步驟： `RevocationList`，載入現有的撤銷清單。 建立新的 `RevocationListFactory` 例項，並務必增加CRL編號。 呼叫 `RevocationListFactioryEntries.addRevocationEntries` 將舊清單中的所有專案新增至新清單。 呼叫 `RevocationListFactory.addRevocationEntry` 將任何新的撤銷專案新增至RevocationList。

如需示範如何建立撤銷清單的範常式式碼、載入現有的撤銷清單，以及檢查電腦代號是否已撤銷，請參閱 `com.adobe.flashaccess.samples.revocation.CreateRevocationList` 在參照實作命令列工具中 [!DNL samples] 目錄。
