---
title: 封裝內容
description: 封裝內容
copied-description: true
exl-id: d408889c-f96d-43d3-af50-62cb5ecc2e28
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 封裝內容{#packaging-content}

封裝遠端金鑰傳遞的內容時，請使用指定需要遠端金鑰傳遞的原則。 HLS內容的M3U8 （資訊清單檔案）中必須包含金鑰伺服器URL。 Primetime DRM金鑰伺服器URL的格式為：

```
https://key-server-host:port/faxsks/tenant-name/key
```

例如，金鑰伺服器主機名稱 [!DNL mykeyserver.com] 接聽連線埠443和名為的租使用者 `tenant1`，則可在M3U8中指定的金鑰伺服器URL為：

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

iOS和Xbox 360使用者端均可使用相同的URL。 或者，如果伺服器針對每種使用者端型別設定了不同的租使用者，則可能會使用不同的URL。

只要授權伺服器URL指向正確設定的執行中授權伺服器，就可以在不需要金鑰伺服器的使用者端上播放相同的內容。
