---
title: 授權預覽
description: 授權預覽
copied-description: true
exl-id: 7e6b1062-7240-4dae-86bb-bd26e7be1f14
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 授權預覽{#license-preview}

使用者端可以傳送授權預覽請求，這表示應用程式可以在要求使用者購買內容之前執行預覽操作，以確定使用者的電腦是否實際符合播放所需的所有條件。

*`License preview`* 是指使用者端預覽授權（檢視授權允許哪些權利）的能力，與預覽內容（在決定購買之前檢視一小部分內容）的能力不同。 每一台機器都有一些獨特的引數：可用的輸出及其保護狀態、可用的執行階段/DRM版本，以及DRM使用者端安全性等級。 許可證預覽模式允許執行階段/DRM使用者端測試許可證伺服器商業邏輯並向使用者提供資訊，以便他能夠做出明智的決策。 因此，使用者端可以看到有效的授權看起來是什麼樣子，但實際上不會收到解密內容的金鑰。 支援授權預覽為選用，且只有在您實作使用此功能的自訂使用者端時才有必要。

若要判斷使用者端是否傳送了預覽請求或授權贏取請求，請呼叫 `LicenseRequestMessage.getRequestPhase()`並將其與 `LicenseRequestMessage.RequestPhase.Acquire`
