---
title: 生成隨機數
description: 生成隨機數
copied-description: true
exl-id: 9a816570-753e-4b05-a6ea-2d4b20ffa3d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---

# 生成隨機數{#generating-random-numbers}

硬體隨機數生成器可用於Linux伺服器，以確保生成足夠的熵。 如果電腦無法生成足夠的熵，則需要隨機性源的Adobe訪問操作將在等待來自的資料時阻塞 `/dev/random`。
