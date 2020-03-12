---
seo-title: 使用輸出保護策略
title: 使用輸出保護策略
uuid: f00d2a97-0036-41a6-ab44-391cc40b146e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用輸出保護策略{#using-output-protection-policies}

**Widevine輸出保護策略**

Widevine本機支援模擬和數字輸出保護限制。 請參閱Widevine服務供應商的檔案，瞭解如何將這些原則附加至產生的授權。

如果您使用Expressplay做為Widevine服務提供者，則會透過hdcpOutputControl標幟在代號產生時附加數位輸出保護原則：允許的值為0、1、2，其中0 = HDCP_NONE、1 = HDCP_V1、2 = HDCP_V2。 HDCP_V1和HDCP_V2分別執行HDCP 1.X和2.X版。

Expressplay目前不支援附加模擬輸出限制

**播放就緒輸出保護政策**

PlayReady也支援模擬和數位輸出保護限制。 可設定的輸出保護級別值。 「輸 [出保護級別](https://msdn.microsoft.com/en-us/library/dn468831.aspx) 」頁記錄了您可以設定的值及其預期的客戶端行為。

如果您使用Expressplay，則會透過compressedDigitalAudioOPL、uncompressedDigitalAudioOPL、compressedDigitalVideoOPL、uncompressedDigitalVideoOPL和unknownOutputBehavior標幟，在代號產生時附加輸出保護等級值。 這些記錄在 [PlayReady授權Token要求中](https://www.expressplay.com/developer/restapi/#playready-license-token-request)
