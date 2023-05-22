---
title: 策略關鍵程度
description: 策略關鍵程度
copied-description: true
exl-id: 6c6971fe-0c0a-4998-917c-aebbf1c4a9df
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# 策略關鍵程度{#policy-criticality}

如果策略中使用了新的使用規則，並且這些策略用於為較舊的許可證伺服器打包的內容（這些伺服器不瞭解新的使用規則），則可以指定較舊的許可證伺服器應該如何運行。 預設情況下，策略重要性為「true」，這意味著許可證伺服器必須瞭解策略的所有部分，才能使用策略生成許可證。 如果策略重要性設定為「false」，則舊版許可證伺服器可能會忽略它不理解的策略的部分，而由伺服器生成的許可證將不包含新的使用規則。

Adobe使用SDK版本2.0.2及更高版本的訪問伺服器將遵守策略關鍵性設定。
