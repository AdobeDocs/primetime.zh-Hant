---
description: 您可以傳送權杖請求至適當的Expressplay權杖伺服器，為其加密內容產生Expressplay權杖。
title: Expressplay權杖
exl-id: 38faba06-6737-4dec-ac97-27db3124b993
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# Expressplay權杖 {#expressplay-tokens}

您可以傳送權杖請求至適當的Expressplay權杖伺服器，為其加密內容產生Expressplay權杖。

下列URL即是範例：

```
https://wv-gen.service.expressplay.com/hms/wv/
token?customerAuthenticator=<your expressplay customer authenticator>
&kid=fd1a706ac2b36002888f6d4a414333c3
&contentKey=5438b719bf47a2f5678237477db2f9e6
&securityLevel=1
&hdcpOutputControl=0
```

提供給的內容加密金鑰儲存ID或CEKSID `kid` 引數以及指定給的內容加密金鑰或CEK `contentKey` 引數必須與用於封裝的內容加密金鑰儲存體ID和內容加密金鑰相符。 以下文字是權杖伺服器回應的範例：

```
https://wv.service.expressplay.com/hms/wv/rights/
?ExpressPlayToken=AQAAABIDKbgAAABQbt68jktab0YRY-r9mo6VP
 VqDDvkHq78x4V9_AyBUTtcNFHw5JtNKlKrMt-4HBdJ3Fopr7fqFSBp
 SJ4o-d8teAkUZUtW3Od5V-SHsCLnAlbFW84K71h2xNUiMAvRcUFBG3bjxMQ
```

然後，您可以

* 使用傳回的URL和查詢作為授權伺服器URL，或者
* 從URL中取出查詢，並分別在ExpressPlayToken中作為HTTPPOST標頭傳遞
