---
title: 清除中內容的初始部分
description: 清除中內容的初始部分
copied-description: true
exl-id: f291e0f5-ce26-41c4-b468-36b111cb7a1c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# 清除中內容的初始部分{#initial-portion-of-content-in-the-clear}

此可選參數指定內容開始後將保持未加密的時間（秒）。

示例用例：這允許在Mighile DRM客戶端在後台下載許可證時更快的回放啟動時間。 視頻的未加密部分在初始化和許可證獲取發生在後台時立即開始回放。 關閉此功能後，用戶可能會注意到播放體驗的延遲，因為客戶端電腦在任何視頻播放發生之前都會執行所有許可步驟。
