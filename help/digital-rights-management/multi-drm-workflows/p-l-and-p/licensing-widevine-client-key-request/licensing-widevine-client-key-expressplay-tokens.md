---
description: 您可以傳送Token請求至適當的Expressplay Token伺服器，為其加密內容產生Expressplay Token。
seo-description: 您可以傳送Token請求至適當的Expressplay Token伺服器，為其加密內容產生Expressplay Token。
seo-title: Expressplay Token
title: Expressplay Token
uuid: 6103e1b2-127d-4758-a589-15f0f3c73db1
translation-type: tm+mt
source-git-commit: d0ba1f98b16f6350ae842ca2ce1261bf49dd8a66
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Expressplay Token {#expressplay-tokens}

您可以傳送Token請求至適當的Expressplay Token伺服器，為其加密內容產生Expressplay Token。

範例如下：

```
https://wv-gen.service.expressplay.com/hms/wv/
token?customerAuthenticator=<your expressplay customer authenticator>
&kid=fd1a706ac2b36002888f6d4a414333c3
&contentKey=5438b719bf47a2f5678237477db2f9e6
&securityLevel=1
&hdcpOutputControl=0
```

內容加密密鑰儲存ID或CEKSID（指定給`kid`參數）和內容加密密鑰或CEK（指定給`contentKey`參數）必須匹配用於打包的內容加密密鑰儲存ID和內容加密密鑰。 以下文字是Token伺服器回應的範例：

```
https://wv.service.expressplay.com/hms/wv/rights/
?ExpressPlayToken=AQAAABIDKbgAAABQbt68jktab0YRY-r9mo6VP
 VqDDvkHq78x4V9_AyBUTtcNFHw5JtNKlKrMt-4HBdJ3Fopr7fqFSBp
 SJ4o-d8teAkUZUtW3Od5V-SHsCLnAlbFW84K71h2xNUiMAvRcUFBG3bjxMQ
```

然後，您可以

* 使用傳回的URL和查詢作為授權伺服器URL，或
* 從URL取出查詢，然後以HTTP POST標題的形式個別傳入ExpressPlayToken