---
title: 策略關鍵性
description: 策略關鍵性
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# 策略重要性{#policy-criticality}

如果策略中使用了新的使用規則，並且這些策略用於針對舊版許可證伺服器（這些規則不瞭解新的使用規則）的內容包裝中，則可以指定舊版許可證伺服器的行為方式。 預設情況下，策略重要性為「true」，這表示許可證伺服器必須瞭解策略的所有部分，才能使用策略生成許可證。 如果策略重要性設定為「false」，則舊版許可證伺服器可能會忽略其不瞭解的部分策略，而伺服器生成的許可證將不包含新的使用規則。

Adobe使用SDK 2.0.2版及更新版本的伺服器存取時，將會遵循原則重要性設定。
