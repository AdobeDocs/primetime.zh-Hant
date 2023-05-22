---
description: 必須確保安全地頒發許可證。 考慮這些最佳做法以保護許可證伺服器
title: 保護許可證伺服器
exl-id: 88b8f44f-c140-4cbc-be0a-f67058548fc3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 0%

---

# 保護許可證伺服器 {#protecting-the-license-server}

必須確保安全地頒發許可證。 請考慮以下最佳做法來保護許可證伺服器：

## 正在使用本地生成的CRL {#consuming-locally-generated-crls}

要使用本地生成的證書吊銷清單(CRL)和策略更新清單，請使用Adobe PrimetimeDRM API驗證簽名。

以下API驗證清單是否未被篡改，以及清單是否由正確的許可證伺服器簽名：

* 呼叫 [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) 在您提供 [吊銷清單](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) 到任何API。

   有關詳細資訊，請參見 [吊銷清單工廠](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)。

* 呼叫 [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) 在提供 `PolicyUpdateList` 到任何API。

   有關詳細資訊，請參見 [策略更新清單](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html)。

## 正在使用Adobe發佈的CRL{#consuming-crls-published-by-adobe}

SDK定期下載由Adobe發佈的CRL。 必須確保不阻止對這些檔案的訪問或不阻止對這些CRL的強制執行。

SDK具有一個配置選項，可以在檢索AdobeCRL時忽略錯誤，並且您只能在開發環境中應用此選項。 在生產環境中，許可證伺服器必須從Adobe中檢索CRL。 如果許可證伺服器無法獲取有效的CRL，則發生錯誤。

## 生成CRL以補充由Adobe發佈的CRL{#generating-crls-to-supplement-those-published-by-adobe}

可以使用Adobe PrimetimeDRM建立CRL，該CRL補充由Adobe發佈的電腦CRL。

黃金時段DRM SDK檢查並強制AdobeCRL。 但是，您可以通過建立CRL來禁止其他客戶端電腦，該CRL通過將CRL傳遞到Mogine DRM SDK來撤消其他電腦憑據。 發放許可證時，SDK將檢查AdobeCRL和CRL。

要生成CRL，請參見 [吊銷清單工廠](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)。

## 回滾檢測 {#rollback-detection}

如果您的Adobe PrimetimeDRM實施使用要求客戶端維護狀態的業務規則（例如，回放窗口間隔）,Adobe建議伺服器跟蹤回滾計數器，並使用AIR或SWF允許清單。

回滾計數器在來自客戶端的大多數請求中都發送到伺服器。 如果您的Mighine DRM實現不需要回滾計數器，則可以忽略它。 否則，Adobe建議伺服器儲存隨機電腦ID，該ID是使用 [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())，以及資料庫中的當前計數器值。

有關如何遞增和跟蹤回退計數器的詳細資訊，請參見 [客戶端狀態](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) 和回滾檢測。

## 頒發許可證時的電腦計數 {#machine-count-when-issuing-licenses}

如果業務規則要求跟蹤用戶的電腦數，則許可證伺服器或域伺服器必須儲存與用戶關聯的電腦ID。

跟蹤電腦ID的最穩健方法是儲存由 [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) 中的設定。 收到新請求後，使用 [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId))。

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) 執行ID的比較以確定ID是否代表同一台電腦。 此比較僅在有少量電腦ID時才實用。 例如，如果允許用戶在其域中使用五台電腦，則可以在資料庫中搜索與用戶用戶名關聯的電腦ID，並獲取一小組資料以供比較。

此比較對於允許匿名訪問的部署不實用。 在這個例子中， [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) 可使用。 但是，如果用戶從Flash和Adobe AIR®運行時訪問內容，則此ID不能相同。

>[!NOTE]
>
>如果用戶重新格式化硬碟，ID將無法存在。

## 重放保護 {#replay-protection}

重播保護可防止攻擊者重放許可證請求消息，並可能對客戶端造成拒絕服務(DoS)攻擊。

DoS攻擊是攻擊者試圖阻止服務的合法用戶使用該服務。 例如，使用回滾計數器的重播攻擊可用於「欺騙」許可證伺服器，使其認為DRM客戶端已回滾其狀態，從而導致帳戶暫停。

要瞭解有關重播保護的詳細資訊，請參見 [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId())。

## 維護受信任內容包器的允許清單 {#maintain-a-allowlist-of-trusted-content-packagers}

允許清單是受信任實體的清單。

對於內容打包器，實體是內容所有者信任的組織，可以打包（或加密）視頻檔案並建立受DRM保護的內容。 部署Adobe PrimetimeDRM時，應維護受信任內容包的允許清單。 在頒發許可證之前，還必須驗證受DRM保護檔案的DRM元資料中內容打包器的身份。

要瞭解如何獲取有關打包內容的實體的資訊，請參見 [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo())。

## 驗證令牌超時{#timeout-for-authentication-tokens}

由Adobe PrimetimeDRM SDK生成的所有驗證令牌都有一個超時間隔，以保護應用程式安全。

在處理驗證請求時，使用黃金時段DRM SDK指定驗證令牌的過期。 在令牌過期後，該令牌不再有效，用戶必須向許可證伺服器再次進行身份驗證。

要瞭解有關身份驗證請求的詳細資訊，請參見 [驗證處理程式](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html)。

## 覆蓋策略選項 {#overriding-policy-options}

發放許可證時，許可證伺服器可以覆蓋策略中指定的使用規則。

如果策略指定開始日期，則在該開始日期之前不會生成許可證。 但是，可以在生成許可證後在許可證中設定將來的開始日期。 應謹慎使用此選項，因為客戶端無法阻止用戶將系統時間提前以規避開始日期。
