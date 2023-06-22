---
title: 使用DRM原則更新清單
description: 使用DRM原則更新清單
copied-description: true
exl-id: 140f1fff-2078-427b-ade2-8ec18a14216f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# DRM原則更新清單 {#drm-policy-update-lists}

如果您在封裝任何內容之後更新DRM原則中的使用規則，授權伺服器需要擁有最新版本，才能核發使用更新版DRM原則的授權。 一種方法是透過DRM原則更新清單來達成此目的。

DRM政策更新清單由檔案表示，該檔案包括已更新或已撤銷DRM政策的清單。 每當您更新DRM原則時，都需要產生新的DRM原則更新清單，並定期將該清單推送到所有授權伺服器。

## 使用DRM原則更新清單 {#working-with-drm-policy-update-lists}

對於無法存取資料庫以儲存DRM政策相關資訊的授權伺服器，您可能想要使用DRM政策更新清單來通知授權伺服器任何更新的DRM政策。 DRM原則更新清單可能包含DRM原則的更新版本或已撤銷的DRM原則ID清單。 如果原則更新清單包含在 `HandlerConfiguration`，SDK會在核發授權時強制執行此清單。

如果內容擁有者或發行者想要中止依照特定DRM政策發行授權，您也可以撤銷任何DRM政策。 DRM原則更新清單可用來強制執行SDK中的DRM原則撤銷。 您也可以套用DRM原則更新清單，以提供SDK的已更新DRM原則清單。

>[!NOTE]
>
>每當您撤銷DRM政策時，任何已核發的授權都不會自動撤銷。 它只會防止根據該DRM政策簽發額外的授權。

## 更新原則更新清單{#update-policy-update-lists}

使用DRM原則更新清單涉及使用 `PolicyUpdateListFactory` 物件。 如果要建立DRM原則更新清單，您需要載入現有的DRM原則更新清單，然後使用Java API檢查DRM原則是否已更新或撤銷。

使用DRM原則更新清單：

1. 設定您的開發環境，並包含您在專案中設定開發環境時包含的所有JAR檔案。
1. 建立 `ServerCredentialFactory` 執行個體以載入簽署所需的認證。
1. 建立 `PolicyUpdateListFactory` 執行個體，使用 `ServerCredential` 您所建立的。
1. 指定您要撤銷的DRM原則ID。
1. 建立 `PolicyRevocationEntry` 物件（使用DRM原則ID） `String` 您剛建立的DRM原則更新清單，然後將其傳入，以將其新增至 `PolicyUpdateListFactory.addRevocationEntry()`.
1. 呼叫，產生新的DRM原則更新清單 `PolicyUpdateListFactory.generatePolicyUpdateList()`.

   同樣地，您可以使用將DRM政策更新至清單 `PolicyUpdateEntry`.
1. 如果DRM原則更新清單已經存在，您可以呼叫，將其序列化以便載入 `PolicyUpdateList.getBytes()`.

   若要載入清單，請呼叫 `PolicyUpdateListFactory.loadPolicyUpdateList()` 並在序列化清單中傳遞。
1. 透過呼叫，確認簽章有效且清單已由正確的授權伺服器憑證簽署 `PolicyUpdateList.verifySignature()`.
1. 傳遞DRM原則ID `String` 到 `PolicyUpdateList.isRevoked()` 驗證專案是否已撤銷。

   或者，您也可以將清單傳遞至 `HandlerConfiguration` 每當核發授權時，就會強制執行。
如果您想要將更多專案新增至現有專案 `PolicyUpdateList`，您需要載入現有的DRM原則更新清單。 因此，您需要建立新的DRM `PolicyUpdateListFactory` 執行個體。 呼叫 `PolicyUpdateListFactory.addEntries` 將舊清單中的所有專案新增至新清單。 呼叫 `PolicyUpdateListFactory.addRevocationEntry` 或 `addUpdatedEntry` 將任何新的撤銷或更新專案新增至DRM PolicyUpdateList。

如需示範如何建立DRM原則更新清單的範常式式碼，請參閱 `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` 在 *參考實作命令列工具* [!DNL samples] 目錄。
