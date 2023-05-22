---
title: 使用DRM策略更新清單
description: 使用DRM策略更新清單
copied-description: true
exl-id: 140f1fff-2078-427b-ade2-8ec18a14216f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# DRM策略更新清單 {#drm-policy-update-lists}

如果在打包任何內容後更新DRM策略中的使用規則，則許可證伺服器需要具有最新版本，然後才能頒發使用更新的DRM策略的許可證。 實現這一點的一種方法是通過DRM策略更新清單。

DRM策略更新清單由包括更新或撤消的DRM策略清單的檔案表示。 每次更新DRM策略時，都需要生成新的DRM策略更新清單，並定期將清單推送到所有許可證伺服器。

## 使用DRM策略更新清單 {#working-with-drm-policy-update-lists}

對於沒有訪問資料庫以儲存有關DRM策略的資訊的許可證伺服器，您可能希望使用DRM策略更新清單將任何更新的DRM策略通知給許可證伺服器。 DRM策略更新清單可以包括已撤消的DRM策略的更新版本或DRM策略ID的清單。 如果策略更新清單包含在 `HandlerConfiguration`,SDK在發出許可證時強制執行此清單。

如果內容所有者或分發者希望終止在特定DRM策略下發放許可證，則還可以撤消任何DRM策略。 DRM策略更新清單可用於在SDK中強制執行DRM策略撤消。 也可應用DRM策略更新清單，以向SDK提供更新的DRM策略清單。

>[!NOTE]
>
>無論何時撤消DRM策略，任何已頒發的許可證都不會自動撤消。 它僅防止根據該DRM策略發放附加許可證。

## 更新策略更新清單{#update-policy-update-lists}

使用DRM策略更新清單涉及使用 `PolicyUpdateListFactory` 的雙曲餘切值。 如果要建立DRM策略更新清單，則需要載入現有DRM策略更新清單，然後使用Java API檢查DRM策略是否已更新或撤消。

要使用DRM策略更新清單：

1. 設定開發環境並包括在項目中設定開發環境時包括的所有JAR檔案。
1. 建立 `ServerCredentialFactory` 實例，以載入簽名所需的憑據。
1. 建立 `PolicyUpdateListFactory` 實例 `ServerCredential` 你創造的。
1. 指定要撤消的DRM策略ID。
1. 建立 `PolicyRevocationEntry` 使用DRM策略ID `String` 建立的，然後將其傳遞到DRM策略更新清單 `PolicyUpdateListFactory.addRevocationEntry()`。
1. 通過調用生成新DRM策略更新清單 `PolicyUpdateListFactory.generatePolicyUpdateList()`。

   同樣，可以使用 `PolicyUpdateEntry`。
1. 如果DRM策略更新清單已存在，則可以通過調用將其序列化以載入 `PolicyUpdateList.getBytes()`。

   要載入清單，請調用 `PolicyUpdateListFactory.loadPolicyUpdateList()` 並在序列化清單中傳遞。
1. 通過調用驗證簽名是否有效以及清單是否已由正確的許可證伺服器證書籤名 `PolicyUpdateList.verifySignature()`。
1. 傳遞DRM策略ID `String` 入 `PolicyUpdateList.isRevoked()` 驗證條目是否已被吊銷。

   或者，可以將清單傳遞給 `HandlerConfiguration` 然後，只要頒發許可證，就強制執行。
如果要向現有條目添加更多條目 `PolicyUpdateList`，需要載入現有DRM策略更新清單。 因此，需要建立新的DRM `PolicyUpdateListFactory` 實例。 呼叫 `PolicyUpdateListFactory.addEntries` 將舊清單中的所有條目添加到新清單。 呼叫 `PolicyUpdateListFactory.addRevocationEntry` 或 `addUpdatedEntry` 將任何新的吊銷或更新條目添加到DRM PolicyUpdateList。

有關演示如何建立DRM策略更新清單的示例代碼，請參見 `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` 的 *參考實現命令行工具* [!DNL samples] 的子菜單。
