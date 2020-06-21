---
seo-title: 非SWF應用程式允許清單
title: 非SWF應用程式允許清單
uuid: d4f93b15-e556-4749-95ab-f7f58b1061d7
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# 非SWF應用程式允許清單 {#non-swf-application-allowlisting}

AIR是第一個提供應用程式允許清單的平台，以及您用來允許清單非SWF應用程式（Adobe AIR、iOS、Android等）的屬性名稱 保留其原名： `policy.allowedAIRApplication.n`. 這可讓所有非Flash應用程式在發佈前，先使用簽署憑證來簽署內容。 這稱為應用程 *式ID*。 您可以使用工具擷取應用程式 [!DNL AdobePublisherIDUtility.jar] ID。 此允許清單將強制執行於支援Primetime DRM的任何用戶端。

應用程式ID衍生自用於簽署特定應用程式之簽署憑證的公開金鑰。 如果憑證中的公開金鑰過期，則所有先前的內容都允許列在僅播放使用舊憑證簽署的應用程式時，新應用程式將不會播放（使用新憑證簽署）。

如果您有內容庫可讓您列在使用特定簽署憑證簽署的應用程式中，且該憑證會過期，而您會獲得新憑證（使用不同的公用／私用鑰匙對），則舊內容將不會在新應用程式上播放， ** 除非您執行下列任何動作：

* 在您的 `PolicyUpdateList` 授權伺服器上使用來覆寫傳入的原則，並插入新的「允許應用程式」清單項目以及新簽署憑證的摘要。
* 更新您的授權伺服器邏輯以覆寫傳入的原則，並插入新的「允許應用程式」清單項目。
* 請求您的簽署憑證發行者簽發新憑證，該憑證會使用您先前憑證使用的相同公開／私用金鑰配對。
* 如果您要傳送參照URL端點的HDS/HLS內容來擷取 `DRMMetadata`，則可以重新產生 `DRMMetadata` （使用Primetime DRM Java SDK）以插入新的DRM政策，其中包含更新的「允許應用程式」清單項目。

* 使用包含新簽署憑證摘要的新DRM原則，重新封裝所有舊內容。

如需詳 `policy.allowedAIRApplication.n` 細資 *訊，請參閱* 「設定屬性」。

>[!NOTE]
>
>若要允許列出iOS應用程式，您必須有特殊的方法。 請參 [閱「iOS程式設計人員指南](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) 」中 *的「允許清單您的iOS應用程式」*。
