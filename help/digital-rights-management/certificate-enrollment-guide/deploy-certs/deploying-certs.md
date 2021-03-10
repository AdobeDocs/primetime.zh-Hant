---
title: 部署憑證
description: 部署憑證
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# 部署憑證{#deploy-certificates}

為避免授權伺服器上的PFX密碼以明文形式提供，「參考實作」和「Adobe PrimetimeDRM Server for Protected Streaming」（受保護串流）需要在設定檔中指定密碼時加密。 有關運行擾頻實用程式的說明，請參閱&#x200B;*使用黃金時段DRM參考實施*&#x200B;或&#x200B;*使用保護流的黃金時段DRM伺服器*。 每個加密口令都包括其自己的擾碼實用程式，並且加密口令在這兩個許可證伺服器實現之間不能互換。

若要將憑證和加擾的密碼部署至您的授權伺服器，請參閱&#x200B;*使用黃金時段DRM參考實作*&#x200B;或&#x200B;*使用保護串流的Primetime DRM伺服器*。
