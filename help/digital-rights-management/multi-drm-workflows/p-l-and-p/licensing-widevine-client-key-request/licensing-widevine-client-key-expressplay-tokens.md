---
description: 通過將令牌請求發送到相應的Expressplay令牌伺服器，可以為其加密內容生成Expressplay令牌。
title: 表達式令牌
exl-id: 38faba06-6737-4dec-ac97-27db3124b993
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# 表達式令牌 {#expressplay-tokens}

通過將令牌請求發送到相應的Expressplay令牌伺服器，可以為其加密內容生成Expressplay令牌。

示例如下：

```
https://wv-gen.service.expressplay.com/hms/wv/
token?customerAuthenticator=<your expressplay customer authenticator>
&kid=fd1a706ac2b36002888f6d4a414333c3
&contentKey=5438b719bf47a2f5678237477db2f9e6
&securityLevel=1
&hdcpOutputControl=0
```

提供給的內容加密密鑰儲存ID或CEKSID `kid` 參數和內容加密密鑰，或 `contentKey` 參數必須與用於打包的內容加密密鑰儲存ID和內容加密密鑰匹配。 以下文本是令牌伺服器響應的示例：

```
https://wv.service.expressplay.com/hms/wv/rights/
?ExpressPlayToken=AQAAABIDKbgAAABQbt68jktab0YRY-r9mo6VP
 VqDDvkHq78x4V9_AyBUTtcNFHw5JtNKlKrMt-4HBdJ3Fopr7fqFSBp
 SJ4o-d8teAkUZUtW3Od5V-SHsCLnAlbFW84K71h2xNUiMAvRcUFBG3bjxMQ
```

你可以

* 將返回的URL和查詢用作許可證伺服器URL，或
* 從URL中取出查詢，然後作為HTTPPOST標頭分別傳入ExpressPlayToken
