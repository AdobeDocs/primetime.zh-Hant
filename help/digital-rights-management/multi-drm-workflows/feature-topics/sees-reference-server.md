---
description: 協調授權和原則執行的一個方法是將這些功能建置到權益伺服器。 Adobe提供SEES參考軟體權利檔案伺服器，您可以使用它來建置您自己的伺服器。
title: 參考伺服器範例ExpressPlay軟體權利檔案伺服器(SEES)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# 參考伺服器：範例ExpressPlay軟體權利檔案伺服器(SEES) {#reference-server-sample-expressplay-entitlement-server-sees}

協調授權和原則執行的一個方法是將這些功能建置到權益伺服器。 Adobe提供SEES參考軟體權利檔案伺服器，您可以使用它來建置您自己的伺服器。

參考伺服器SEES會示範ExpressPlay軟體權利檔案服務，顯示兩種服務：基本時間型軟體權利檔案和裝置繫結軟體權利檔案。

SEE是以兩種ExpressPlay Fairplay服務為基礎所建置：

1. Expressplay Token要求服務
1. Expressplay記錄擷取服務

ExpressPlay權杖請求的URL格式採用兩種格式，一種用於生產，另一種用於測試環境：

**生產**： ht<span></span>tps://fp-gen.{prod_domain}/hms/fp/token

**測試**： ht<span></span>tps://fp-gen.test.expressplay.com/hms/fp/token

擷取ExpressPlay記錄的URL格式有兩個表單，一個用於生產，另一個用於測試環境：

**生產**： ht<span></span>tps://api.{prod_domain}/cmiapi/getrecord/

**測試**： ht<span></span>tps://api.test.expressplay.com/cmiapi/getrecord/
