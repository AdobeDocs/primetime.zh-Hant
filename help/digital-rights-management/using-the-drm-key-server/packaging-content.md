---
title: 封裝內容
description: 封裝內容
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# 封裝內容{#packaging-content}

封裝內容以進行遠端金鑰傳送時，請使用指定需要遠端金鑰傳送的原則。 HLS內容的M3U8（manifest檔案）中必須包含關鍵伺服器URL。 Primetime DRM金鑰伺服器URL的格式為：

```
https://key-server-host:port/faxsks/tenant-name/key
```

例如，若是位於連接埠443的Key Server主機名稱[!DNL mykeyserver.com]監聽，以及名為`tenant1`的租用戶，M3U8中要指定的Key Server URL為：

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

iOS和Xbox 360用戶端都可使用相同的URL。 或者，如果伺服器針對每種用戶端類型設定了不同的租客，則可能會使用不同的URL。

只要授權伺服器URL指向正確設定的執行授權伺服器，即可在不需要關鍵伺服器的用戶端上播放相同的內容。
