---
title: 回滾檢測
description: 回滾檢測
copied-description: true
exl-id: 054d3634-5ce9-4a51-ac91-e6ae60a1fd6e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# 回滾檢測 {#rollback-detection}

如果Adobe訪問的實現使用要求客戶端維護狀態的業務規則（例如，播放窗口間隔）,Adobe強烈建議伺服器跟蹤回滾計數器並使用AIR或SWF允許清單。

回滾計數器在來自客戶端的大多數請求中都發送到伺服器。 如果Adobe訪問的實現不需要回滾計數器，則可以忽略它。 否則，Adobe建議伺服器儲存隨機電腦ID — 使用 `MachineToken.getMachineId().getUniqueId()` — 和資料庫中的當前計數器值。 有關遞增和跟蹤回滾計數器的詳細資訊，請參閱中的ClientState *Adobe訪問API參考* 和 *回滾檢測* 在 *使用Adobe訪問SDK保護內容*。
