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

AIR是首個提供應用程式允許清單的平台，以及您用於允許列出非SWF應用程式(Adobe AIR、iOS、Android等)的屬性的名稱。 保留其原名： `policy.allowedAIRApplication.n`。 這允許在發佈前使用簽名證書籤名的所有非Flash應用程式回放內容。 這稱為 *應用程式ID*。 可以使用 [!DNL AdobePublisherIDUtility.jar] 工具欄。 此允許清單將在支援Mogifale DRM的任何客戶端上強制執行。

應用程式ID是從用於對特定應用程式進行簽名的簽名證書的公鑰派生的。 如果證書中的公鑰過期，則所有先前允許的內容只允許在使用舊證書籤名的應用上播放，將不會在新應用（使用新證書籤名）上播放。

如果您有一個允許將內容庫列出到已使用特定簽名證書籤名的應用程式，且該證書過期並且您獲得了新證書（使用其他公共/私鑰對），則舊內容將不會在新應用程式上播放 *除非* 執行下列任一操作：

* 使用 `PolicyUpdateList` 在您的許可證伺服器上覆蓋傳入策略，並在新簽名證書的摘要中插入新的「應用程式允許」清單條目。
* 更新許可證伺服器的邏輯以覆蓋傳入策略並插入新的「應用程式允許」清單條目。
* 請求籤名證書頒發者向您頒發使用與先前證書相同的公共/私鑰對的新證書。
* 如果您正在提供引用URL終結點以檢索HDS/HLS內容 `DRMMetadata`，可再生 `DRMMetadata` （使用Mogfire DRM Java SDK）插入包含已更新的「應用程式允許」清單條目的新DRM策略。

* 使用具有新簽名證書摘要的新DRM策略重新打包所有舊內容。

請參閱 `policy.allowedAIRApplication.n` 在 *配置屬性* 的雙曲餘切值。

>[!NOTE]
>
>允許列出iOS應用程式需要您採用一種特殊的方法。 請參閱 [允許列出您的iOS應用程式](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) 的 *《 TVSDK foriOS程式設計師指南》*。
