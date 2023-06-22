---
title: 概觀
description: 概觀
copied-description: true
exl-id: 15733120-b1bb-46a7-90d2-4eb11c539d62
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 概觀  {#overview}

使用Adobe® Access™，內容提供者可以將原則套用至媒體檔案。 使用原則管理API，管理員可以建立、檢視詳細資訊和更新原則。

A *原則* 定義使用者檢視內容的方式；這是包含安全性設定、驗證要求和使用許可權的資訊集合。 套用原則時，加密和簽署可讓內容提供者維持對其內容的控制，無論其散佈的範圍有多廣。 受保護檔案可透過Adobe®Flash®Media Server或HTTP伺服器傳送。 可透過iOS適用的Adobe® AIR®、Adobe®Flash®Player和Adobe® Primetime SDK建立自訂播放器，下載並播放這些區段。 原則是許可證伺服器產生許可證時使用的範本。 使用者端也可以在請求授權之前參考原則，以判斷在向伺服器發出授權請求之前是否需要提示使用者進行驗證。

原則指定授予使用者端的一或多個許可權。 通常，原則至少會包含「向右播放」。 也可以指定多個播放許可權，每個許可權都有不同的限制。 當使用者端遇到具有多個播放許可權的授權時，它會使用第一個符合所有限制的授權。 例如，此功能可用於在不同的平台上強制執行不同的輸出保護設定。 如需說明此範例的範常式式碼，請參閱 `CreatePolicyWithOutputProtection.java` 在「參考實作命令列工具」的「範例」目錄中。

您可以使用原則管理API完成下列工作：

* 建立和更新原則
* 檢視原則詳細資訊
* 管理原則更新清單

如需本章所述Java API的詳細資訊，請參閱 *Adobe存取API參考*.

如需Policy Manager參考實作的相關資訊，請參閱 *使用Adobe存取參考實作*.
