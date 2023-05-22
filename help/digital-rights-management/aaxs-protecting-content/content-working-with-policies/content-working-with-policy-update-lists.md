---
title: 使用策略更新清單
description: 使用策略更新清單
copied-description: true
exl-id: 71715eec-e6a3-4640-b17f-ec0c38caf73e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# 使用策略更新清單{#working-with-policy-update-lists}

對於沒有訪問資料庫以儲存策略資訊的許可證伺服器，您可能希望使用策略更新清單將更新的策略通知給許可證伺服器。 策略更新清單可能包含已吊銷的策略版本或策略ID清單。 如果在中提供策略更新清單 `HandlerConfiguration`, SDK將在頒發許可證時強制執行此清單。

如果內容所有者或分銷商希望根據特定策略終止發放許可證，則也可撤銷該策略。 策略更新清單可用於在SDK中強制執行策略撤消。 策略更新清單也可用於向SDK提供更新策略的清單。 請注意，撤消策略不會撤消已頒發的許可證。 它只防止根據該政策簽發額外許可證。

使用策略更新清單涉及使用 `PolicyUpdateListFactory` 的雙曲餘切值。 要建立策略更新清單，請載入現有策略更新清單，並檢查是否已使用Java API更新或吊銷策略，請執行以下步驟：

1. 設定開發環境並包括「設定項目內的開發環境」中提到的所有JAR檔案。
1. 建立 `ServerCredentialFactory` 實例，以載入簽名所需的憑據。
1. 建立 `PolicyUpdateListFactory` 實例使用 `ServerCredential` 建立的。
1. 指定要撤消的策略ID。
1. 建立 `PolicyRevocationEntry` 使用策略ID的對象 `String` 您剛剛建立的，並通過將其傳入策略更新清單將其添加到 `PolicyUpdateListFactory.addRevocationEntry()`。 通過調用生成新策略更新清單 `PolicyUpdateListFactory.generatePolicyUpdateList()`。 同樣，可以使用 `PolicyUpdateEntry`。
1. 如果策略更新清單已存在，則可以通過調用對其進行序列化以載入 `PolicyUpdateList.getBytes()`。 要載入清單，請調用 `PolicyUpdateListFactory.loadPolicyUpdateList()` 並在序列化清單中傳遞。
1. 通過調用驗證簽名是否有效以及清單是否由正確的許可證伺服器證書籤名 `PolicyUpdateList.verifySignature()`。
1. 要檢查項是否被吊銷，請傳遞策略ID `String` 入 `PolicyUpdateList.isRevoked()`。 或者，該清單可以傳入 `HandlerConfiguration` 發證後執行。

將附加條目添加到現有條目 `PolicyUpdateList`，載入現有策略更新清單。 新建 `PolicyUpdateListFactory` 實例。 呼叫P `olicyUpdateListFactory.addEntries` 將舊清單中的所有條目添加到新清單。 呼叫 `PolicyUpdateListFactory.addRevocationEntry` 或 `addUpdatedEntry` 將任何新的吊銷或更新條目添加到PolicyUpdateList。

有關演示如何建立策略更新清單、載入現有策略更新清單以及檢查策略是否已被吊銷的示例代碼，請參見 `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` 在「參考實現」命令行工具「示例」目錄中。
