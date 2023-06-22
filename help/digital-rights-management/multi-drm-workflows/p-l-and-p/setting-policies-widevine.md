---
title: 使用輸出保護原則
description: 使用輸出保護原則
copied-description: true
exl-id: d91c9181-a6b2-4982-a3ba-57c4b56428eb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# 使用輸出保護原則{#using-output-protection-policies}

**Widevine輸出保護原則**

Widevine原生支援類比與數位輸出保護限制。 請參閱您的Widevine服務提供者提供的檔案，瞭解如何將這些原則附加至產生的授權。

如果您使用Expressplay作為Widevine服務提供者，則透過hdcpOutputControl旗標在產生權杖時附加數位輸出保護原則：允許值為0、1、2，其中0 = HDCP_NONE、1 = HDCP_V1、2 = HDCP_V2。 HDCP_V1和HDCP_V2分別強制執行HDCP 1.X版和2.X版。

Expressplay目前不支援附加類比輸出限制

**PlayReady輸出保護原則**

PlayReady本身也支援類比與數位輸出保護限制。 您可以設定的輸出保護等級值。 頁面 [輸出保護等級](https://msdn.microsoft.com/en-us/library/dn468831.aspx) 記錄您可以設定的值及其預期的使用者端行為。

如果您使用Expressplay，請透過compressedDigitalAudioOPL、uncompressedDigitalAudioOPL、compressedDigitalVideoOPL、uncompressedDigitalVideoOPL和unknownOutputBehavior旗標，在產生Token時附加輸出保護等級值。 這些記錄在 [PlayReady授權Token要求](https://www.expressplay.com/developer/restapi/#playready-license-token-request)
