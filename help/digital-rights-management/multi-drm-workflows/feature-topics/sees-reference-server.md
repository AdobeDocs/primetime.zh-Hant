---
description: 協調許可和策略實施的一種方法是將這些功能構建到權利伺服器上。 Adobe提供了SEES參考權利伺服器，您可以使用它來構建自己的伺服器。
title: 參考伺服器示例ExpressPlay權利伺服器(SEES)
exl-id: aa5b63f4-dffc-4808-8aa6-6b8f63df592c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# 參考伺服器：示例ExpressPlay權利伺服器(SEES) {#reference-server-sample-expressplay-entitlement-server-sees}

協調許可和策略實施的一種方法是將這些功能構建到權利伺服器上。 Adobe提供了SEES參考權利伺服器，您可以使用它來構建自己的伺服器。

參考伺服器SEES演示了ExpressPlay權利服務，其中顯示了兩個服務：基本基於時間的權利和設備綁定權利。

SEES構建在兩個ExpressPlay Fairplay服務之上：

1. Expressplay令牌請求服務
1. ExpressPlay記錄檢索服務

ExpressPlay令牌請求的URL格式有兩種形式，一種用於生產，另一種用於test環境：

**生產**:ht<span></span>tps://fp-gen。{prod_domain/hms/fp/token

**Test**:ht<span></span>tps://fp-gen.test.expressplay.com/hms/fp/token

ExpressPlay記錄檢索的URL格式有兩種形式，一種用於生產，另一種用於test環境：

**生產**:ht<span></span>tps://api。{prod_domain/cmiapi/getrecord/

**Test**:ht<span></span>tps://api.test.expressplay.com/cmiapi/getrecord/
