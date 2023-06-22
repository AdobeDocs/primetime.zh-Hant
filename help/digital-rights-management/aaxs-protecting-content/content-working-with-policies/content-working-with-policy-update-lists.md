---
title: 使用原則更新清單
description: 使用原則更新清單
copied-description: true
exl-id: 71715eec-e6a3-4640-b17f-ec0c38caf73e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# 使用原則更新清單{#working-with-policy-update-lists}

對於無法存取資料庫以儲存原則相關資訊的授權伺服器，您可能希望使用原則更新清單來通知授權伺服器已更新的原則。 原則更新清單可能包含更新版本的原則，或已撤銷的原則ID清單。 如果中提供了原則更新清單 `HandlerConfiguration`，SDK會在核發授權時強制執行此清單。

如果內容擁有者或經銷商想要根據特定原則停止簽發授權，原則也可能遭到撤銷。 原則更新清單可用來強制執行SDK中的原則撤銷。 原則更新清單也可用來為SDK提供已更新原則的清單。 請注意，撤銷原則不會撤銷已核發的授權。 它只會防止根據該原則簽發額外的授權。

使用原則更新清單涉及使用 `PolicyUpdateListFactory` 物件。 若要建立原則更新清單、載入現有原則更新清單，並使用Java API檢查原則是否已更新或撤銷，請執行以下步驟：

1. 設定您的開發環境，並在您的專案中包含設定開發環境中所提及的所有JAR檔案。
1. 建立 `ServerCredentialFactory` 執行個體以載入簽署所需的認證。
1. 建立 `PolicyUpdateListFactory` 使用下列專案的例項： `ServerCredential` 您已建立。
1. 指定要撤銷的原則ID。
1. 建立 `PolicyRevocationEntry` 使用原則ID的物件 `String` 您剛才已建立，並將其傳遞至以新增至原則更新清單 `PolicyUpdateListFactory.addRevocationEntry()`. 呼叫，產生新的原則更新清單 `PolicyUpdateListFactory.generatePolicyUpdateList()`. 同樣地，可使用將更新的原則新增至清單 `PolicyUpdateEntry`.
1. 如果原則更新清單已經存在，您可以呼叫，將其序列化以供載入 `PolicyUpdateList.getBytes()`. 若要載入清單，請呼叫 `PolicyUpdateListFactory.loadPolicyUpdateList()` 並在序列化清單中傳遞。
1. 透過呼叫，驗證簽章是否有效，以及清單是否由正確的授權伺服器憑證簽署 `PolicyUpdateList.verifySignature()`.
1. 若要檢查專案是否已撤銷，請傳遞原則ID `String` 到 `PolicyUpdateList.isRevoked()`. 或者，清單可傳遞至 `HandlerConfiguration` 並且會在簽發授權時強制執行。

若要新增其他專案至現有專案，請執行下列步驟： `PolicyUpdateList`，載入現有的原則更新清單。 建立新的 `PolicyUpdateListFactory` 執行個體。 呼叫P `olicyUpdateListFactory.addEntries` 將舊清單中的所有專案新增至新清單。 呼叫 `PolicyUpdateListFactory.addRevocationEntry` 或 `addUpdatedEntry` 將任何新的撤銷或更新專案新增至PolicyUpdateList。

如需示範如何建立原則更新清單、載入現有原則更新清單，以及檢查原則是否已撤銷的範常式式碼，請參閱 `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` 在「參考實作命令列工具」的「範例」目錄中。
