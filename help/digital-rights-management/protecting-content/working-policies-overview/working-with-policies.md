---
title: 使用DRM原則概述
description: 使用DRM原則概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# 概觀 {#working-with-drm-policies-overview}

內容提供者可使用Primetime DRM SDK將DRM政策套用至媒體檔案。 然後，管理員可以使用原則管理API來建立、檢視和更新DRM原則。

A *`DRM policy`* 是包含安全性設定、驗證要求和使用許可權的資訊集合。 此原則會定義使用者檢視內容的方式。 DRM原則、加密和簽署可讓內容提供者維持對其內容的控制，無論內容散佈的範圍有多廣。

DRM原則可作為許可證伺服器產生許可證時使用的範本。 使用者端在請求授權之前也可以參考DRM政策，以決定使用者端在發出授權請求給伺服器之前是否需要提示使用者進行驗證。

您可以使用AdobeFlash Media Server或HTTP伺服器來傳送受保護的內容。 使用者可在以Primetime DRM SDK建置的自訂播放器中下載及播放受保護的內容。

DRM政策指定授予使用者端的一或多個許可權。 通常，DRM政策至少包含 *`Play Right`*. 您也可以指定多個播放許可權，每個許可權都有不同的限制。 使用者端收到具有多項播放許可權的授權時，會使用符合所有限制的第一個授權。 例如，您可以在不同平台上強制執行不同的輸出保護設定。

另請參閱 `CreatePolicyWithOutputProtection.java` 在參照實作命令列工具中 [!DNL samples] 範常式式碼的目錄，說明此範例。

您可以使用Primetime DRM原則管理API完成下列工作：

* 建立和更新原則
* 檢視DRM原則詳細資訊
* 管理DRM原則更新清單

請參閱 *Primetime DRM API參考* 以取得有關Java API的詳細資料。

請參閱 *使用Primetime DRM參考實作* 有關Primetime DRM Policy Manager的資訊指南。
