---
title: Adobe存取認證
description: Adobe存取認證
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Adobe訪問憑據{#adobe-access-credentials}

若要核發Adobe存取用戶端所接受的有效授權，「保護串流的Adobe Access Server」必須設定由Adobe核發的一組憑證。 這些憑據可以儲存在PKCS#12(.pfx)檔案或HSM中。

.pfx檔案可以位於任何位置，但為方便設定，我們建議將。pfx檔案放入租用戶的設定目錄。 如需詳細資訊，請參閱「[授權伺服器組態檔](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)」。