---
description: 'null'
seo-description: 'null'
seo-title: 一般工作流程
title: 一般工作流程
uuid: aafe0030-8a59-4090-aeac-76867777eaa5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 典型工作流{#typical-workflow}

這是典型的Primetime DRM參考實作工作流程，其中同時包含命令列工具和授權伺服器：

1. 使用策略命令行工具建立DRM策略。
1. 使用Packager命令列工具加密內容。
1. 部署參考實作授權伺服器。
1. 將視訊播放器上傳至網頁伺服器。
1. 使用上傳的視訊播放器取得授權並播放您的加密內容。

由於此典型工作流同時使用命令行工具和許可證伺服器，因此，您需要在繼續操作之前安裝和配置這兩個元件。
