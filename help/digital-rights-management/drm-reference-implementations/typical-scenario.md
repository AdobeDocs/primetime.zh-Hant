---
title: 典型工作流
description: 典型工作流
copied-description: true
exl-id: c2020b48-7e97-4df5-a453-7b76e2e1d458
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 典型工作流{#typical-workflow}

這是典型的黃金時段DRM參考實現工作流，該工作流同時具有命令行工具和許可證伺服器：

1. 使用「策略」命令行工具建立DRM策略。
1. 使用Packager命令行工具加密內容。
1. 部署引用實現許可證伺服器。
1. 將視頻播放器上載到Web伺服器。
1. 使用上傳的視頻播放器獲取許可證並播放加密內容。

由於此典型工作流同時使用命令行工具和許可證伺服器，因此您需要在繼續之前安裝和配置這兩個元件。
