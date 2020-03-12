---
seo-title: 封裝內容
title: 封裝內容
uuid: 366c8470-b7ef-4a39-83c2-151ba9be9a32
translation-type: tm+mt
source-git-commit: 1547eb3dd220fafc08df923f40504736c16a866c

---


# 封裝內容{#packaging-content}

封裝內容以進行遠端金鑰傳送時，請使用指定需要遠端金鑰傳送的原則。 HLS內容的M3U8（manifest檔案）中必須包含關鍵伺服器URL。 Primetime DRM金鑰伺服器URL的格式為：

```
https://key-server-host:port/faxsks/tenant-name/key
```

例如，若是位於連接埠443 [!DNL mykeyserver.com] 監聽的Key Server主機名稱，以及名為租用戶 `tenant1`，則M3U8中要指定的Key Server URL是：

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

iOS和Xbox 360用戶端都可使用相同的URL。 或者，如果伺服器針對每種用戶端類型設定了不同的租客，則可能會使用不同的URL。

只要授權伺服器URL指向正確設定的執行授權伺服器，即可在不需要關鍵伺服器的用戶端上播放相同的內容。
