---
seo-title: 回滾檢測
title: 回滾檢測
uuid: fc80c98f-7ee5-414b-87fe-0dbb8d4f6019
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# 回滾檢測{#rollback-detection}

如果您的Adobe Access實作使用要求用戶端維持狀態（例如播放視窗間隔）的業務規則，Adobe強烈建議伺服器追蹤回滾計數器，並使用AIR或SWF允許清單。

回滾計數器在客戶端發出的大多數請求中都發送到伺服器。 如果您的Adobe Access實作不需要回滾計數器，則可以忽略它。 否則，Adobe建議伺服器儲存使用`MachineToken.getMachineId().getUniqueId()`取得的隨機機器ID，以及資料庫中目前的計數器值。 如需有關遞增和追蹤回滾計數器的詳細資訊，請參閱&#x200B;*Adobe Access API Reference*&#x200B;和&#x200B;*使用Adobe Access SDK保護內容*&#x200B;中的&#x200B;*回滾偵測*&#x200B;中的ClientState。
