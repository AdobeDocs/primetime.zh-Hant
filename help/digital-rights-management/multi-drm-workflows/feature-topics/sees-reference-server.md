---
description: 協調授權和原則執行的一個方法是將這些功能建置到權益伺服器。 Adobe會提供SEES參考軟體權利檔案伺服器，您可以用它來建立自己的伺服器。
title: 參考伺服器範例ExpressPlay軟體權利伺服器(SEES)
exl-id: aa5b63f4-dffc-4808-8aa6-6b8f63df592c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# 參考伺服器：範例ExpressPlay軟體權利檔案伺服器(SEES) {#reference-server-sample-expressplay-entitlement-server-sees}

協調授權和原則執行的一個方法是將這些功能建置到權益伺服器。 Adobe會提供SEES參考軟體權利檔案伺服器，您可以用它來建立自己的伺服器。

參考伺服器SEES會示範ExpressPlay軟體權利檔案服務，顯示兩種服務：基本時間型軟體權利檔案和裝置繫結軟體權利檔案。

SEES是以兩種ExpressPlay Fairplay服務為基礎所建置：

1. Expressplay Token要求服務
1. Expressplay記錄擷取服務

ExpressPlay Token請求的URL格式有兩種形式，一種用於生產環境，一種用於測試環境：

**生產**： ht<span></span>tps://fp-gen.{prod_domain}/hms/fp/token

**測試**： ht<span></span>tps://fp-gen.test.expressplay.com/hms/fp/token

ExpressPlay記錄擷取的URL格式有兩種形式，一種用於生產，一種用於測試環境：

**生產**： ht<span></span>tps://api.{prod_domain}/cmiapi/getrecord/

**測試**： ht<span></span>tps://api.test.expressplay.com/cmiapi/getrecord/
