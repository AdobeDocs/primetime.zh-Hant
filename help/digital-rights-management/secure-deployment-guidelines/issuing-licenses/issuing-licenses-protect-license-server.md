---
description: 您必須確保安全地發行授權。 請考慮以下最佳實務來保護授權伺服器
title: 保護授權伺服器
exl-id: 88b8f44f-c140-4cbc-be0a-f67058548fc3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 0%

---

# 保護授權伺服器 {#protecting-the-license-server}

您必須確保安全地發行授權。 請考慮以下最佳實務來保護授權伺服器：

## 使用本機產生的CRL {#consuming-locally-generated-crls}

若要使用本機產生的憑證撤銷清單(CRL)和原則更新清單，請使用Adobe Primetime DRM API來驗證簽名。

下列API會確認清單未被竄改，而且清單是由正確的License Server簽署：

* 呼叫 [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) 以在您提供 [撤銷清單](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) 至任何API。

   如需詳細資訊，請參閱 [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* 呼叫 [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) 以在提供 `PolicyUpdateList` 至任何API。

   如需詳細資訊，請參閱 [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

## 使用Adobe發佈的CRL{#consuming-crls-published-by-adobe}

SDK會定期下載Adobe所發佈的CRL。 您必須確保不會封鎖對這些檔案的存取，或不會阻止這些CRL的強制執行。

SDK提供可在擷取AdobeCRL時忽略錯誤的設定選項，而且您只能在開發環境中套用此選項。 在生產環境中，授權伺服器必須從Adobe擷取CRL。 如果授權伺服器無法取得有效的CRL，則會發生錯誤。

## 產生CRL以補充Adobe所發佈的CRL{#generating-crls-to-supplement-those-published-by-adobe}

您可以使用Adobe Primetime DRM來建立CRL，以補充Adobe所發佈的機器CRL。

Primetime DRM SDK會檢查並強制執行AdobeCRL。 不過，您可以建立CRL，將CRL傳遞至Primetime DRM SDK以撤銷其他電腦認證，藉此禁止使用其他使用者端電腦。 當您核發授權時，SDK會檢查AdobeCRL和您的CRL。

若要產生CRL，請參閱 [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

## 復原偵測 {#rollback-detection}

如果您的Adobe Primetime DRM實作使用要求使用者端維持狀態的商業規則（例如播放視窗間隔），Adobe建議伺服器追蹤倒回計數器，並使用AIR或SWF允許清單。

在使用者端的大部分要求中，都會將回覆計數器傳送至伺服器。 如果您的Primetime DRM實作不需要倒回計數器，則可以忽略。 否則，Adobe建議伺服器儲存隨機機器ID，此ID是使用取得 [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())，以及資料庫中目前的計數器值。

如需如何遞增及追蹤倒回計數器的詳細資訊，請參閱 [使用者端狀態](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) 和復原偵測。

## 簽發授權時的電腦計數 {#machine-count-when-issuing-licenses}

如果商業規則要求追蹤使用者的電腦數目，則License Server或Domain Server必須儲存與使用者相關聯的電腦ID。

追蹤機器ID最有效的方法是儲存 [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) 方法。 收到新請求時，請使用將請求中的電腦ID與已知的電腦ID進行比較 [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) 會執行ID的比較，以判斷ID是否代表同一部電腦。 只有少數電腦ID時，此比較才切實可行。 例如，如果使用者在其網域中允許使用五台電腦，您可以在資料庫中搜尋與使用者使用者名稱相關聯的電腦ID，並取得一小部分資料集以進行比較。

此比較不適用於允許匿名存取的部署。 在這種情況下， [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) 可使用。 但是，如果使用者從Flash和Adobe AIR®執行階段存取內容，則此ID不能相同。

>[!NOTE]
>
>如果使用者重新格式化硬碟，該ID將無法存留。

## 重播保護 {#replay-protection}

重播保護可防止攻擊者重播授權要求訊息，並可能對使用者端造成拒絕服務(DoS)攻擊。

DoS攻擊是攻擊者嘗試阻止服務的合法使用者使用該服務的行為。 例如，使用倒回計數器的重播攻擊可能用來「誘騙」License Server認為DRM使用者端已倒回其狀態，進而導致帳戶暫停。

若要進一步瞭解重播保護，請參閱 [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).

## 維護受信任內容封裝者的允許清單 {#maintain-a-allowlist-of-trusted-content-packagers}

允許清單是受信任實體的清單。

對於內容封裝者而言，實體是內容擁有者信任用來封裝（或加密）視訊檔案並建立受DRM保護內容的組織。 部署Adobe Primetime DRM時，您應保留受信任內容封裝器的允許清單。 您還必須先在受DRM保護的檔案的DRM中繼資料中驗證內容封裝者的身份，然後再簽發授權。

若要瞭解如何取得封裝內容的實體相關資訊，請參閱 [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).

## 驗證Token逾時{#timeout-for-authentication-tokens}

Adobe Primetime DRM SDK產生的所有驗證Token都有保護應用程式安全的逾時間隔。

處理驗證請求時，會使用Primetime DRM SDK指定驗證權杖的到期日。 到期後，權杖不再有效，使用者必須透過授權伺服器再次驗證。

若要進一步瞭解驗證請求，請參閱 [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).

## 覆寫原則選項 {#overriding-policy-options}

當您發行授權時，授權伺服器可以覆寫原則中指定的使用規則。

如果原則指定開始日期，則不會在該開始日期之前產生授權。 不過，您可以在授權產生後，在授權中設定未來的開始日期。 應謹慎使用此選項，因為使用者端無法防止使用者將系統時間往前移動以規避開始日期。
