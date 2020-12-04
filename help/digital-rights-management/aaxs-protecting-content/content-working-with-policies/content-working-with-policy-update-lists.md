---
seo-title: 使用策略更新清單
title: 使用策略更新清單
uuid: 583abb31-5c80-43f2-bc3d-a2300f61c4ea
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# 使用策略更新清單{#working-with-policy-update-lists}

對於沒有資料庫儲存策略資訊的許可證伺服器，您可能希望使用策略更新清單來通知許可證伺服器更新的策略。 策略更新清單可能包含策略的更新版本或已撤銷的策略ID清單。 如果`HandlerConfiguration`中提供原則更新清單，SDK會在簽發授權時強制執行此清單。

如果內容擁有者或發佈者想要根據特定政策停止發行授權，政策也可能遭到撤銷。 原則更新清單可用於強制SDK中的原則撤銷。 原則更新清單也可用來提供SDK之更新原則清單。 請注意，廢止政策並不會廢止已發行的授權。 它只會防止依據該政策發行額外授權。

使用策略更新清單涉及使用`PolicyUpdateListFactory`對象。 要建立策略更新清單，請載入現有策略更新清單，並使用Java API檢查策略是否已更新或已撤銷，請執行以下步驟：

1. 設定您的開發環境，並包括在項目中設定開發環境中提到的所有JAR檔案。
1. 建立`ServerCredentialFactory`例項以載入簽署所需的憑證。
1. 使用您建立的`ServerCredential`建立`PolicyUpdateListFactory`實例。
1. 指定要撤銷的原則ID。
1. 使用剛建立的策略ID `String`建立`PolicyRevocationEntry`對象，並將其傳遞到`PolicyUpdateListFactory.addRevocationEntry()`以將其添加到策略更新清單中。 呼叫`PolicyUpdateListFactory.generatePolicyUpdateList()`以產生新的原則更新清單。 同樣地，更新的策略也可以使用`PolicyUpdateEntry`添加到清單中。
1. 如果策略更新清單已存在，則可以通過調用`PolicyUpdateList.getBytes()`將其序列化以進行載入。 要載入清單，請調用`PolicyUpdateListFactory.loadPolicyUpdateList()`並傳入序列化清單。
1. 請呼叫`PolicyUpdateList.verifySignature()`，確認簽名有效且清單已由正確的授權伺服器憑證簽署。
1. 要檢查條目是否被撤銷，請將策略ID `String`傳遞到`PolicyUpdateList.isRevoked()`。 或者，清單可以傳入`HandlerConfiguration`，並在授權發行時強制執行。

要向現有`PolicyUpdateList`添加其他條目，請載入現有策略更新清單。 建立新的`PolicyUpdateListFactory`例項。 呼叫P `olicyUpdateListFactory.addEntries`，將舊清單中的所有條目添加到新清單中。 呼叫`PolicyUpdateListFactory.addRevocationEntry`或`addUpdatedEntry`，將任何新的撤銷或更新項目新增至PolicyUpdateList。

有關演示如何建立策略更新清單、載入現有策略更新清單以及檢查策略是否已撤銷的示例代碼，請參閱參考實施命令行工具「示例」目錄中的`com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList`。
