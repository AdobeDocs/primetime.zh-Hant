---
title: 概觀
description: 概觀
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 概觀  {#overview}

使用Adobe® Access™，內容提供者可以將原則套用至媒體檔案。 使用原則管理API，管理員可以建立、檢視詳細資料和更新原則。

A *原則* 定義使用者檢視內容的方式；這是包含安全性設定、驗證要求和使用許可權的資訊集合。 套用原則時，加密和簽署可讓內容提供者維持對其內容的控制，無論其散佈的範圍有多廣。 受保護的檔案可透過使用Adobe®Flash®Media Server或HTTP伺服器來傳送。 您可透過iOS適用的Adobe® AIR®、Adobe®Flash®Player和Adobe® Primetime SDK建立自訂播放器，下載並播放這些影片。 原則是許可證伺服器產生許可證時使用的範本。 使用者端也可以在請求授權之前參考原則，以確定在向伺服器發出授權請求之前它是否需要提示使用者進行驗證。

原則會指定一或多個授與使用者端的許可權。 一般而言，原則至少會包含「向右播放」。 您也可以指定多個播放許可權，每個許可權有不同的限制。 當使用者端遇到具有多個播放許可權的授權時，它會使用第一個符合所有限制的授權。 例如，此功能可用於在不同的平台上強制實施不同的輸出保護設定。 如需說明此範例的範常式式碼，請參閱 `CreatePolicyWithOutputProtection.java` 在「參考實作」命令列工具「範例」目錄中。

您可以使用原則管理API完成下列工作：

* 建立和更新原則
* 檢視原則詳細資訊
* 管理原則更新清單

如需本章所述Java API的詳細資訊，請參閱 *Adobe存取API參考*.

如需Policy Manager參考實作的相關資訊，請參閱 *使用Adobe存取參考實作*.
