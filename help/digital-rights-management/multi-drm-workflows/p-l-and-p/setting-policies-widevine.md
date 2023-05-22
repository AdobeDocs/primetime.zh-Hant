---
title: 使用輸出保護策略
description: 使用輸出保護策略
copied-description: true
exl-id: d91c9181-a6b2-4982-a3ba-57c4b56428eb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# 使用輸出保護策略{#using-output-protection-policies}

**WideVine輸出保護策略**

Widevine本機支援模擬和數字輸出保護限制。 有關如何將這些策略附加到生成的許可證的WideVine服務提供商的文檔。

如果使用Expressplay作為Widevine服務提供商，則通過hdcpOutputControl標誌在令牌生成時附加數字輸出保護策略：允許的值為0、1、2，其中0 = HDCP_NONE、1 = HDCP_V1、2 = HDCP_V2。 HDCP_V1和HDCP_V2分別強制使用HDCP版本1.X和2.X。

Expressplay當前不支援附加模擬輸出限制

**PlayReady輸出保護策略**

PlayReady還以本機方式支援模擬和數字輸出保護限制。 可設定的輸出保護級別值。 頁面 [輸出保護級別](https://msdn.microsoft.com/en-us/library/dn468831.aspx) 記錄可以設定的值及其預期的客戶端行為。

如果使用Expressplay，則通過compressedDigitalAudioOPL、uncompressedDigitalAudioOPL、compressedDigitalVideoOPL、uncompressedDigitalVideoOPL和unknownOutputBehavior標誌在令牌生成時附加輸出保護級別值。 這些文檔記錄在 [PlayReady許可證令牌請求](https://www.expressplay.com/developer/restapi/#playready-license-token-request)
