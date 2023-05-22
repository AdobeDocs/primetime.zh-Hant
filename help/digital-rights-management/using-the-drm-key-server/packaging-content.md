---
title: 打包內容
description: 打包內容
copied-description: true
exl-id: d408889c-f96d-43d3-af50-62cb5ecc2e28
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 打包內容{#packaging-content}

將內容打包以進行遠程密鑰傳遞時，請使用指定需要遠程密鑰傳遞的策略。 密鑰伺服器URL必須包含在HLS內容的M3U8（清單檔案）中。 黃金時段DRM密鑰伺服器URL的格式為：

```
https://key-server-host:port/faxsks/tenant-name/key
```

例如，對於密鑰伺服器主機名 [!DNL mykeyserver.com] 正在偵聽埠443，並且租戶名為 `tenant1`,M3U8中要指定的關鍵伺服器URL是：

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

同一URL可用於iOS和Xbox 360客戶端。 或者，如果為伺服器配置了每種客戶端類型的單獨租戶，則可以使用不同的URL。

只要許可證伺服器URL指向正確配置的正在運行的許可證伺服器，就可以在不需要密鑰伺服器的客戶端上播放相同的內容。
