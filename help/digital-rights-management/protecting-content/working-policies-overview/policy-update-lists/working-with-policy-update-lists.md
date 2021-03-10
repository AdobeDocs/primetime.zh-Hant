---
title: 使用DRM策略更新清單
description: 使用DRM策略更新清單
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---


# DRM策略更新清單{#drm-policy-update-lists}

如果您在封裝任何內容後更新DRM原則中的使用規則，授權伺服器必須擁有最新版本，才能核發使用更新DRM原則的授權。 要做到這一點，一個方法是通過DRM策略更新清單。

DRM策略更新清單由包括更新或撤銷的DRM策略清單的檔案表示。 每當您更新DRM策略時，都需要生成新的DRM策略更新清單，並定期將清單推送到所有許可證伺服器。

## 使用DRM策略更新清單{#working-with-drm-policy-update-lists}

對於沒有存取資料庫以儲存有關DRM策略的資訊的許可證伺服器，您可能希望使用DRM策略更新清單來通知許可證伺服器任何更新的DRM策略。 DRM策略更新清單可包括已撤銷的DRM策略的更新版本或DRM策略ID的清單。 如果`HandlerConfiguration`包含原則更新清單，SDK會在發出授權時強制執行此清單。

如果內容擁有者或發佈者想要根據特定DRM政策停止發行授權，您也可以撤銷任何DRM政策。 DRM策略更新清單可用於在SDK中強制DRM策略撤銷。 您也可以套用DRM原則更新清單，以提供更新後的DRM原則清單至SDK。

>[!NOTE]
>
>每當您撤銷DRM政策時，任何已發行的授權都不會自動撤銷。 它只會防止依據該DRM政策發行額外授權。

## 更新策略更新清單{#update-policy-update-lists}

使用DRM策略更新清單涉及使用`PolicyUpdateListFactory`對象。 如果要建立DRM策略更新清單，則需要載入現有的DRM策略更新清單，然後使用Java API檢查DRM策略是否已更新或撤銷。

要使用DRM策略更新清單：

1. 設定您的開發環境並包括在項目中設定開發環境時包含的所有JAR檔案。
1. 建立`ServerCredentialFactory`例項以載入簽署時所需的憑證。
1. 使用您建立的`ServerCredential`建立`PolicyUpdateListFactory`實例。
1. 指定您要撤銷的DRM原則ID。
1. 使用剛建立的DRM策略ID `String`建立`PolicyRevocationEntry`對象，然後將其傳遞到`PolicyUpdateListFactory.addRevocationEntry()`，將其添加到DRM策略更新清單。
1. 通過調用`PolicyUpdateListFactory.generatePolicyUpdateList()`生成新的DRM策略更新清單。

   同樣地，您可以使用`PolicyUpdateEntry`將DRM策略更新到清單。
1. 如果DRM策略更新清單已存在，則可以通過調用`PolicyUpdateList.getBytes()`將其序列化以進行載入。

   若要載入清單，請呼叫`PolicyUpdateListFactory.loadPolicyUpdateList()`並將它傳入序號清單中。
1. 呼叫`PolicyUpdateList.verifySignature()`，確認簽名有效且清單已由正確的授權伺服器憑證簽署。
1. 將DRM策略ID `String`傳遞到`PolicyUpdateList.isRevoked()`以驗證條目是否已撤銷。

   或者，您可將清單傳遞至`HandlerConfiguration`，然後在每次核發授權時強制執行。
如果要向現有`PolicyUpdateList`添加更多條目，則需要載入現有的DRM策略更新清單。 因此，您需要建立新的DRM `PolicyUpdateListFactory`實例。 呼叫`PolicyUpdateListFactory.addEntries`，將舊清單中的所有條目添加到新清單中。 呼叫`PolicyUpdateListFactory.addRevocationEntry`或`addUpdatedEntry`，將任何新的撤銷或更新項目新增至DRM PolicyUpdateList。

有關演示如何建立DRM策略更新清單的示例代碼，請參見&#x200B;*參考實施命令行工具* [!DNL samples]目錄中的`com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList`。
