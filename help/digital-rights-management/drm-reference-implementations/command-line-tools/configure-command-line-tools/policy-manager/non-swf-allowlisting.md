---
title: 非SWF應用程式允許清單
description: 非SWF應用程式允許清單
copied-description: true
exl-id: f33fb0e9-144f-49f8-8da2-8a50aea09456
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# 非SWF應用程式允許清單 {#non-swf-application-isting}

AIR是第一個推出應用程式允許清單的平台，以及您用來允許清單非SWF應用程式(Adobe AIR、iOS、Android等)的屬性名稱。 會保留其原始名稱： `policy.allowedAIRApplication.n`. 這可讓所有在發佈前已透過「簽署憑證」簽署的非Flash應用程式播放內容。 這稱為 *應用程式ID*. 您可以使用以下方式提取應用程式ID： [!DNL AdobePublisherIDUtility.jar] 工具。 此允許清單將在任何支援Primetime DRM的使用者端上強制執行。

應用程式ID衍生自用於簽署特定應用程式的簽署憑證之公開金鑰。 如果憑證中的公開金鑰過期，則所有先前內容僅允許在用舊憑證簽署的應用程式上播放，將不會在新應用程式（用新憑證簽署）上播放。

如果您的狀況是內容庫允許列出給使用特定簽署憑證簽署的應用程式，且該憑證過期且您獲得新憑證（使用不同的公開/私人金鑰組），則舊內容不會在新的應用程式上播放 *Unless* 您可以執行下列任一項作業：

* 使用 `PolicyUpdateList` 在授權伺服器上覆寫內送原則，並以您的新簽署憑證摘要插入新的應用程式允許清單專案。
* 更新您的授權伺服器的邏輯以覆寫傳入原則，並插入新的應用程式允許清單專案。
* 請要求您的簽署憑證簽發者發行新憑證，該憑證使用與先前憑證相同的公開/私密金鑰組。
* 如果您要傳送的HDS/HLS內容是參照URL端點以擷取 `DRMMetadata`，您可以重新產生 `DRMMetadata` （使用Primetime DRM Java SDK）插入包含更新應用程式允許清單專案的新DRM原則。

* 使用具有新簽署憑證摘要的新DRM原則重新封裝所有舊內容。

另請參閱 `policy.allowedAIRApplication.n` 在 *設定屬性* 以取得詳細資訊。

>[!NOTE]
>
>允許列出iOS應用程式需要您特殊的方法。 另請參閱 [允許列出您的iOS應用程式](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) 在 *iOS適用的TVSDK程式設計師指南*.
