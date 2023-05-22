---
title: 撤消電腦憑據
description: 撤消電腦憑據
copied-description: true
exl-id: 4f49a94c-1bd9-4a7a-ac92-4da0b7fe4ae4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# 撤消電腦憑據 {#revoking-machine-credentials}

Adobe維護用於撤消已知被洩露的電腦憑據的CRL。 此CRL由SDK自動強制執行。 如果您不希望您的許可證伺服器向其頒發許可證的其他電腦，則可以建立電腦吊銷清單並添加要排除的電腦令牌的頒發者名稱和序列號(使用 `MachineToken.getMachineTokenId()` 檢索電腦證書的頒發者名稱和序列號)。

撤消電腦憑據涉及 `RevocationListFactory` 的雙曲餘切值。 要建立吊銷清單，請載入現有吊銷清單，並檢查是否使用Java API吊銷了電腦令牌，請執行以下步驟：

1. 設定開發環境並包括中提及的所有JAR檔案 [建立開發環境](../../protecting-content/setting-up-the-sdk/setup-dev-env.md) 你的項目。
1. 建立 `ServerCredentialFactory` 實例，以載入簽名所需的憑據。 許可證伺服器憑據用於對吊銷清單進行簽名。
1. 建立 `RevocationListFactory` 實例。
1. 指定要通過使用 `IssuerAndSerialNumber` 的雙曲餘切值。 所有Adobe PrimetimeDRM請求都包含電腦令牌。
1. 建立 `RevocationList` 對象使用 `IssuerAndSerialNumber` 您剛建立的對象，並通過將其傳遞到 `RevocationListFactory.addRevocationEntry()`。 通過調用生成新吊銷清單 `RevocationListFactory.generateRevocationList()`。

1. 要保存吊銷清單，可通過調用 `RevocationList.getBytes()`。 要載入清單，請調用 `RevocationListFactory.loadRevocationList()` 並在序列化清單中傳遞。

1. 通過調用驗證簽名是否有效以及清單是否由正確的許可證伺服器簽名 `RevocationList.verifySignature()`。
1. 要檢查項是否被吊銷，請通過 `IssuerAndSerialNumber` 對象 `RevocationList.isRevoked()`。 該撤銷清單也可被傳遞到 `HandlerConfiguration` 使SDK強制所有身份驗證和許可請求的吊銷清單。

將附加條目添加到現有條目 `RevocationList`，載入現有吊銷清單。 新建 `RevocationListFactory` 實例，並確保增加CRL號。 呼叫 `RevocationListFactioryEntries.addRevocationEntries` 將舊清單中的所有條目添加到新清單。 呼叫 `RevocationListFactory.addRevocationEntry` 將任何新的吊銷條目添加到RevocationList。

有關演示如何建立吊銷清單、載入現有吊銷清單以及檢查電腦令牌是否已被吊銷的示例代碼，請參見 `com.adobe.flashaccess.samples.revocation.CreateRevocationList` 在「參考實現」命令行工具中 [!DNL samples] 的子菜單。
