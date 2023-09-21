---
title: 正在封裝內容
description: 正在封裝內容
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 正在封裝內容{#packaging-content}

封裝遠端金鑰傳遞的內容時，請使用指定需要遠端金鑰傳遞的原則。 金鑰伺服器URL必須包含在HLS內容的M3U8 （資訊清單檔案）中。 Primetime DRM金鑰伺服器URL的格式為：

```
https://key-server-host:port/faxsks/tenant-name/key
```

例如，Key Server主機名稱 [!DNL mykeyserver.com] 接聽連線埠443和名為的租使用者 `tenant1`，則在M3U8中指定的金鑰伺服器URL為：

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

iOS和Xbox 360使用者端均可使用相同的URL。 或者，如果伺服器針對每種使用者端型別設定了不同的租使用者，則可能會使用不同的URL。

只要授權伺服器URL指向正確設定的執行中授權伺服器，就可以在不需要金鑰伺服器的使用者端上播放相同的內容。
