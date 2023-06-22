---
title: 正在撤銷電腦認證
description: 正在撤銷電腦認證
copied-description: true
exl-id: 4f49a94c-1bd9-4a7a-ac92-4da0b7fe4ae4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# 正在撤銷電腦認證 {#revoking-machine-credentials}

Adobe會維護一個CRL，用於撤銷已知已遭入侵的電腦認證。 SDK會自動強制執行此CRL。 如果有其他電腦不想讓授權伺服器發行授權，您可以建立電腦撤銷清單，並新增要排除之電腦權杖的發行者名稱和序號(使用 `MachineToken.getMachineTokenId()` 以擷取電腦憑證的簽發者名稱和序號)。

撤銷電腦認證涉及使用 `RevocationListFactory` 物件。 若要建立撤銷清單、載入現有的撤銷清單，以及檢查機器權杖是否已使用Java API撤銷，請執行以下步驟：

1. 設定您的開發環境，並包含中提到的所有JAR檔案 [設定開發環境](../../protecting-content/setting-up-the-sdk/setup-dev-env.md) 在您的專案中。
1. 建立 `ServerCredentialFactory` 執行個體以載入簽署所需的認證。 授權伺服器認證可用來簽署撤銷清單。
1. 建立 `RevocationListFactory` 執行個體。
1. 指定要撤銷的電腦權杖的簽發者和序號，請使用 `IssuerAndSerialNumber` 物件。 所有Adobe Primetime DRM請求都包含機器權杖。
1. 建立 `RevocationList` 物件 `IssuerAndSerialNumber` 您剛建立的物件，並將其傳遞至以新增至撤銷清單 `RevocationListFactory.addRevocationEntry()`. 呼叫，產生新的撤銷清單 `RevocationListFactory.generateRevocationList()`.

1. 若要儲存撤銷清單，您可以呼叫 `RevocationList.getBytes()`. 若要載入清單，請呼叫 `RevocationListFactory.loadRevocationList()` 並在序列化清單中傳遞。

1. 透過呼叫，確認簽章有效且清單已由正確的授權伺服器簽署 `RevocationList.verifySignature()`.
1. 若要檢查專案是否已撤銷，請傳遞 `IssuerAndSerialNumber` 物件進入 `RevocationList.isRevoked()`. 撤銷清單也可傳遞至 `HandlerConfiguration` ，讓SDK針對所有驗證和授權請求強制執行撤銷清單。

若要新增其他專案至現有專案，請執行下列步驟： `RevocationList`，載入現有的撤銷清單。 建立新的 `RevocationListFactory` 例項，並務必增加CRL編號。 呼叫 `RevocationListFactioryEntries.addRevocationEntries` 將舊清單中的所有專案新增至新清單。 呼叫 `RevocationListFactory.addRevocationEntry` 將任何新的撤銷專案新增至RevocationList。

如需示範如何建立撤銷清單的範常式式碼、載入現有的撤銷清單，以及檢查機器權杖是否已撤銷，請參閱 `com.adobe.flashaccess.samples.revocation.CreateRevocationList` 在參考實作命令列工具中 [!DNL samples] 目錄。
