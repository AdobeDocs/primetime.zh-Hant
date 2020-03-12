---
seo-title: 使用DRM策略更新清單
title: 使用DRM策略更新清單
uuid: 41f89671-81c6-4d3d-ac31-9c2a1980517a
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# DRM策略更新清單 {#drm-policy-update-lists}

如果您在封裝任何內容後更新DRM原則中的使用規則，授權伺服器必須擁有最新版本，才能核發使用更新DRM原則的授權。 要做到這一點，一個方法是通過DRM策略更新清單。

DRM策略更新清單由包括更新或撤銷的DRM策略清單的檔案表示。 每當您更新DRM策略時，都需要生成新的DRM策略更新清單，並定期將清單推送到所有許可證伺服器。

## 使用DRM策略更新清單 {#working-with-drm-policy-update-lists}

對於沒有存取資料庫以儲存有關DRM策略的資訊的許可證伺服器，您可能希望使用DRM策略更新清單來通知許可證伺服器任何更新的DRM策略。 DRM策略更新清單可包括已撤銷的DRM策略的更新版本或DRM策略ID的清單。 如果原則更新清單包含在 `HandlerConfiguration`中，SDK會在發出授權時強制執行此清單。

如果內容擁有者或發佈者想要根據特定DRM政策停止發行授權，您也可以撤銷任何DRM政策。 DRM策略更新清單可用於在SDK中強制DRM策略撤銷。 您也可以套用DRM原則更新清單，以提供更新後的DRM原則清單至SDK。

>[!NOTE]
>
>每當您撤銷DRM政策時，任何已發行的授權都不會自動撤銷。 它只會防止依據該DRM政策發行額外授權。

## 更新策略更新清單{#update-policy-update-lists}

使用DRM策略更新清單涉及對象的 `PolicyUpdateListFactory` 使用。 如果要建立DRM策略更新清單，則需要載入現有的DRM策略更新清單，然後使用Java API檢查DRM策略是否已更新或撤銷。

要使用DRM策略更新清單：

1. 設定您的開發環境並包括在項目中設定開發環境時包含的所有JAR檔案。
1. 建立 `ServerCredentialFactory` 例項以載入簽署所需的認證。
1. 使用 `PolicyUpdateListFactory` 您建立的實例 `ServerCredential` 建立實例。
1. 指定您要撤銷的DRM原則ID。
1. 使用 `PolicyRevocationEntry` 您剛建立的DRM策略ID創 `String` 建對象，然後將其傳遞到DRM策略更新清單中 `PolicyUpdateListFactory.addRevocationEntry()`。
1. 呼叫以產生新的DRM原則更新清單 `PolicyUpdateListFactory.generatePolicyUpdateList()`。

   同樣地，您也可以使用將DRM策略更新到清單 `PolicyUpdateEntry`。
1. 如果DRM策略更新清單已存在，則可以通過調用將其序列化以載入 `PolicyUpdateList.getBytes()`。

   若要載入清單，請呼 `PolicyUpdateListFactory.loadPolicyUpdateList()` 叫並在序號清單中傳遞。
1. 透過呼叫，確認簽名有效且清單已由正確的授權伺服器憑證簽署 `PolicyUpdateList.verifySignature()`。
1. 將DRM策略ID傳遞 `String` 到 `PolicyUpdateList.isRevoked()` 中，以驗證條目是否已撤銷。

   或者，您可以將清單傳遞至授 `HandlerConfiguration` 權發放時，清單就會強制執行。
如果要向現有條目添加更多條目， `PolicyUpdateList`則需要載入現有的DRM策略更新清單。 因此，您需要建立新的DRM `PolicyUpdateListFactory` 實例。 呼 `PolicyUpdateListFactory.addEntries` 叫將舊清單中的所有條目添加到新清單中。 呼 `PolicyUpdateListFactory.addRevocationEntry` 叫或 `addUpdatedEntry` 將任何新的撤銷或更新條目添加到DRM PolicyUpdateList。

有關示範如何建立DRM策略更新清單的示例代碼，請參 `com.adobe.flashaccess.samples.policyupdatelist` 見 `.CreatePolicyUpdateList` 「參 *考實施命令行工具*[!DNL samples] 」目錄。
