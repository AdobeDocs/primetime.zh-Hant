---
title: 許可證預覽
description: 許可證預覽
copied-description: true
exl-id: 283ee661-b1ee-46b9-9337-0497c97bd785
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# 許可證預覽{#license-preview}

客戶端可以發送許可預覽請求，這意味著應用程式可以在要求用戶購買內容之前執行預覽操作，以確定用戶的電腦是否實際滿足回放所需的所有條件。 *許可證預覽* 指客戶預覽許可證（查看許可證允許的權限）的能力，而不是預覽內容（在決定購買前查看內容的一小部分）。 每台電腦所獨有的參數有：輸出可用及其保護狀態、運行時/DRM版本可用以及DRM客戶端安全級別。 許可預覽模式允許運行時/DRM客戶端test許可伺服器業務邏輯並將資訊提供回給用戶，以便他能夠作出知情的決定。 因此，客戶端可以看到有效許可證的外觀，但實際上不會收到解密內容的密鑰。 對許可證預覽的支援是可選的，並且僅當您實施使用此功能的自定義客戶端時才必要。

要確定客戶端是否發送了預覽請求或許可證獲取請求，請撥打 `LicenseRequestMessage.getRequestPhase()`並比較 `LicenseRequestMessage.RequestPhase.Acquire`
