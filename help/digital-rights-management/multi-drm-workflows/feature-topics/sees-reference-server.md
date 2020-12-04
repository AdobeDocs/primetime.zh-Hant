---
description: 協調授權與政策執行的一種方式，是將這些功能建置在權益伺服器中。 Adobe提供SEES參考權益伺服器，您可使用它來建立自己的伺服器。
seo-description: 協調授權與政策執行的一種方式，是將這些功能建置在權益伺服器中。 Adobe提供SEES參考權益伺服器，您可使用它來建立自己的伺服器。
seo-title: 參考伺服器範例ExpressPlay權益伺服器(SEES)
title: 參考伺服器範例ExpressPlay權益伺服器(SEES)
uuid: 99e42f76-7730-42fc-a9a9-f6396ac12c02
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# 參考伺服器：範例ExpressPlay Entitlement Server(SEES){#reference-server-sample-expressplay-entitlement-server-sees}

協調授權與政策執行的一種方式，是將這些功能建置在權益伺服器中。 Adobe提供SEES參考權益伺服器，您可使用它來建立自己的伺服器。

參考伺服器SEES會示範ExpressPlay Entitlement Service，其中顯示兩項服務：基本的時間型權益和裝置系結權益。

SEES建立在兩個ExpressPlay Fairplay服務之上：

1. Expressplay Token請求服務
1. Expressplay Record Retrieving Service

ExpressPlay Token請求的URL格式採用兩種格式，一種用於生產，另一種用於測試環境：

**生產**:<span></span>https://fp-gen。{prod_domain}/hms/fp/token

**測試**:<span></span>https://fp-gen.test.expressplay.com/hms/fp/token

ExpressPlay記錄檢索的URL格式採用兩種形式，一種用於生產，另一種用於測試環境：

**生產**:<span></span>https://api。{prod_domain}/cmiapi/getrecord/

**測試**:<span></span>https://api.test.expressplay.com/cmiapi/getrecord/
