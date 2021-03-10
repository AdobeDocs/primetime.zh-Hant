---
title: 概觀
description: 概觀
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# 概述{#overview}

使用Adobe®存取™，內容提供者可將原則套用至媒體檔案。 使用原則管理API，管理員可以建立、檢視政策的詳細資訊，以及更新政策。

*policy*&#x200B;定義使用者如何檢視內容；它是資訊的集合，其中包含安全性設定、驗證要求和使用權限。 當套用原則時，加密和簽署可讓內容提供者不論內容的散布範圍有多廣，都能維持對內容的控制。 可使用Adobe®Flash®媒體伺服器或HTTP伺服器來傳送受保護的檔案。 您可在使用Adobe® AIR®、Adobe®Flash®播放器和Adobe® Primetime SDK for iOS建立的自訂播放器中下載和播放。 策略是許可證伺服器生成許可證時要使用的模板。 客戶端在請求許可證之前也可以參考該策略，以確定是否需要在向伺服器發出許可證請求之前提示用戶進行驗證。

策略指定授予客戶機的一個或多個權限。 通常，策略至少包括「正確播放」。 您也可以指定多個「播放權」，每個「播放權」具有不同的限制。 當客戶遇到具有多重播放權限的授權時，會使用第一個符合其所有限制的授權。 例如，此功能可用於在不同平台上強制執行不同的輸出保護設定。 如需說明此範例的范常式式碼，請參閱參考實作命令列工具&quot;samples&quot;目錄中的`CreatePolicyWithOutputProtection.java`。

您可以使用原則管理API來完成下列工作：

* 建立和更新原則
* 檢視原則詳細資訊
* 管理策略更新清單

有關本章中討論的Java API的詳細資訊，請參閱&#x200B;*Adobe訪問API參考*。

有關策略管理器參考實施的資訊，請參閱&#x200B;*使用Adobe訪問參考實施*。
