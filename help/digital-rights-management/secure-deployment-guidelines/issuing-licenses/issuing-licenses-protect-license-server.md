---
description: '您必須確保您安全地發行授權。 請考慮這些最佳做法以保護許可證伺服器 '
seo-description: '您必須確保您安全地發行授權。 請考慮這些最佳做法以保護許可證伺服器 '
seo-title: 保護許可證伺服器
title: 保護許可證伺服器
uuid: 7b5de17d-d0a7-41df-9651-4ff51c9965c6
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 0%

---


# 保護許可證伺服器 {#protecting-the-license-server}

您必須確保您安全地發行授權。 請考慮以下最佳做法來保護許可證伺服器：

## 使用本機產生的CRL {#consuming-locally-generated-crls}

若要使用本機產生的憑證撤銷清單(CRL)和政策更新清單，請使用Adobe Primetime DRM API來驗證簽名。

下列API會確認清單未遭竄改，且清單已由正確的授權伺服器簽署：

* 請呼 [叫RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) ，以在您將 [RevocationList提供給任何API之前檢查簽](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) 名。

   如需詳細資訊，請參 [閱RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)。

* 在提 [供給任何API之前，請呼叫PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) ，以檢查 `PolicyUpdateList` 簽名。

   如需詳細資訊，請參 [閱PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html)。

## 使用Adobe發佈的CRL{#consuming-crls-published-by-adobe}

SDK會定期下載由Adobe發佈的CRL。 您必須確保不會封鎖對這些檔案的存取，或不會妨礙這些CRL的執行。

SDK有設定選項，可在擷取Adobe CRL時忽略錯誤，而您只能在開發環境中套用此選項。 在生產環境中，授權伺服器必須從Adobe擷取CRL。 如果授權伺服器無法取得有效的CRL，就會發生錯誤。

## 產生CRL以補充Adobe發佈的CRL{#generating-crls-to-supplement-those-published-by-adobe}

您可以使用Adobe Primetime DRM來建立CRL，以補充Adobe所發佈之機器CRL。

Primetime DRM SDK會檢查並強制執行Adobe CRL。 不過，您可以建立CRL，將CRL傳遞至Primetime DRM SDK，以廢止其他電腦認證的CRL，以禁止其他用戶端電腦。 當您核發授權時，SDK會檢查Adobe CRL和您的CRL。

要生成CRL，請參 [閱RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)。

## 回滾檢測 {#rollback-detection}

如果您實作的Adobe Primetime DRM使用需要用戶端維持狀態（例如播放視窗間隔）的業務規則，Adobe建議伺服器追蹤回滾計數器，並使用AIR或SWF允許清單。

回滾計數器在客戶端發出的大多數請求中都發送到伺服器。 如果您的Primetime DRM實作不需要回滾計數器，則可以忽略它。 否則，Adobe建議伺服器儲存隨機機器ID(使用 [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()))，以及資料庫中的目前計數器值。

有關如何增加和跟蹤回滾計數器的詳細資訊，請參 [閱ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) 和Rollback檢測。

## 核發授權時的機器計數 {#machine-count-when-issuing-licenses}

如果業務規則要求跟蹤用戶的電腦數，則許可證伺服器或域伺服器必須儲存與用戶關聯的電腦ID。

追蹤機器ID的最強穩方式，是將 [](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) MachineId.getBytes()方法傳回的值儲存在資料庫中。 收到新請求時，請使用 [MachineId.matches()比較請求中的機器ID與已知的機器ID](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId))。

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) 會執行ID比較，以判斷ID是否代表相同的機器。 只有在機器ID數很少時，此比較才實用。 例如，如果用戶在其域中允許有五台電腦，則可以搜索資料庫中與用戶的用戶名相關聯的電腦ID，並獲取一小組資料以進行比較。

此比較不適用於允許匿名存取的部署。 在此例中， [可使用MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) 。 不過，如果使用者從Flash和Adobe AIR®執行階段存取內容，此ID就不能相同。

>[!NOTE]
>
>如果使用者重新格式化硬碟，ID將無法存留。

## 重放保護 {#replay-protection}

重放保護可防止攻擊者重放許可證請求消息，並可能導致對客戶端的拒絕服務(DoS)攻擊。

DoS攻擊是攻擊者試圖阻止服務的合法用戶使用該服務。 例如，使用回滾計數器的重放攻擊可用於「誘騙」許可證伺服器，使其認為DRM客戶端已回滾其狀態，從而導致帳戶暫停。

如需有關重放保護的詳細資訊，請 [ 參閱AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId())。

## 維護受信任內容封裝器的允許清單 {#maintain-a-allowlist-of-trusted-content-packagers}

允許清單是受信任實體的清單。

對於內容封裝者，實體是受內容擁有者信任的組織，可封裝（或加密）視訊檔案並建立受DRM保護的內容。 部署Adobe Primetime DRM時，您應維護受信任內容封裝器的允許清單。 您還必須在簽發許可之前，先驗證DRM保護檔案的DRM元資料中的內容包裝器的身份。

如要瞭解如何取得封裝內容之實體的相關資訊，請參 [閱V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo())。

## 驗證Token的逾時{#timeout-for-authentication-tokens}

所有由Adobe Primetime DRM SDK產生的驗證Token都有逾時間隔，以保護應用程式的安全性。

在處理驗證請求時，使用Primetime DRM SDK指定驗證Token的有效期。 Token過期後，此Token即不再有效，使用者必須向授權伺服器再次驗證。

若要進一步瞭解驗證請求，請參 [閱AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html)。

## 覆蓋策略選項 {#overriding-policy-options}

當您發行授權時，授權伺服器可以覆寫原則中指定的使用規則。

如果原則指定開始日期，則不會在該開始日期之前產生授權。 不過，您可以在產生授權後，在授權中設定未來的開始日期。 此選項應謹慎使用，因為用戶端無法阻止使用者將系統時間向前移動，以規避開始日期。