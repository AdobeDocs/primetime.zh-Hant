---
description: 您可以將權杖要求傳送至適當的Expressplay權杖伺服器，以為其加密內容產生Expressplay權杖。
title: Expressplay權杖
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# Expressplay權杖 {#expressplay-tokens}

您可以將權杖要求傳送至適當的Expressplay權杖伺服器，以為其加密內容產生Expressplay權杖。

下列URL即是範例：

```
https://wv-gen.service.expressplay.com/hms/wv/
token?customerAuthenticator=<your expressplay customer authenticator>
&kid=fd1a706ac2b36002888f6d4a414333c3
&contentKey=5438b719bf47a2f5678237477db2f9e6
&securityLevel=1
&hdcpOutputControl=0
```

指定給的內容加密金鑰儲存ID或CEKSID `kid` 引數和指定給的內容加密金鑰或CEK `contentKey` 引數必須符合用於封裝的內容加密金鑰儲存ID和內容加密金鑰。 以下文字是權杖伺服器回應的範例：

```
https://wv.service.expressplay.com/hms/wv/rights/
?ExpressPlayToken=AQAAABIDKbgAAABQbt68jktab0YRY-r9mo6VP
 VqDDvkHq78x4V9_AyBUTtcNFHw5JtNKlKrMt-4HBdJ3Fopr7fqFSBp
 SJ4o-d8teAkUZUtW3Od5V-SHsCLnAlbFW84K71h2xNUiMAvRcUFBG3bjxMQ
```

然後，您可以

* 使用傳回的URL和查詢作為許可證伺服器URL，或者
* 從URL取出查詢，並分別在ExpressPlayToken中傳入HTTPPOST標頭
