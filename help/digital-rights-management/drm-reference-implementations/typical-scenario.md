---
title: 典型工作流程
description: 典型工作流程
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 典型工作流程{#typical-workflow}

這是典型的Primetime DRM參考實作工作流程，同時具有命令列工具和許可證伺服器：

1. 使用「原則」命令列工具建立DRM原則。
1. 使用Packager命令列工具加密內容。
1. 部署參考實作授權伺服器。
1. 將視訊播放器上傳至網頁伺服器。
1. 使用上傳的視訊播放器來取得授權並播放您的加密內容。

由於此典型工作流程同時使用命令列工具和許可證伺服器，因此您會想要在繼續之前安裝和設定這兩個元件。
