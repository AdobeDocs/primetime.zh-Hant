---
seo-title: 授權預覽
title: 授權預覽
uuid: 3171647d-1437-48ab-9659-3eb363993618
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 授權預覽{#license-preview}

用戶端可傳送授權預覽要求，這表示應用程式可先執行預覽作業，再要求使用者購買內容，以判斷使用者的機器是否實際符合播放所需的所有標準。 *授權預覽* ：指客戶預覽授權（查看授權允許的權利）的能力，而非預覽內容（在決定購買之前檢視內容的一小部分）。 每部機器的某些參數是：輸出可用及其保護狀態、可用的運行時/DRM版本和DRM客戶機安全級別。 許可預覽模式允許運行時/DRM客戶端測試許可伺服器業務邏輯並向用戶提供資訊，以便他能夠做出知情決定。 因此，用戶端可以看到有效授權的外觀，但實際上無法收到解密內容的金鑰。 支援授權預覽是可選的，而且只有在您實作使用此功能的自訂用戶端時，才需要。

若要判斷用戶端是傳送預覽請求還是授權取得請求，請呼叫 `LicenseRequestMessage.getRequestPhase()`並比較它與 `LicenseRequestMessage.RequestPhase.Acquire`
