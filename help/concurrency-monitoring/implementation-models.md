---
title: 實作模型
description: 實作模型
source-git-commit: ac0c15b951f305e29bb8fa0bd45aa2c53de6ad15
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---


# 實作模型 {#imp-models}

## 伺服器端原則 {#ss-policies}

此模型將使用CM作為原則決定點，從而將存取決定委派給服務。

由於使用者端不應就套用的原則做出任何假設，因此實施作業需要在心率回應播放期間定期檢查工作階段初始化決策。
