---
title: 降級API概述
description: 降級API概述
exl-id: c7d6685b-a235-42eb-9c9c-0ffa1747f614
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# 降級API概述 {#degradation-api-overview}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 一般資訊 {#general_info}

>[!NOTE]
>
>此API通常不可用。 請與Adobe代表聯繫以獲取可用性更新。

此功能提供整合(程式設計師、MVPD和Adobe)中的三個主要方中的任何一個，它們能夠臨時繞過特定的MVPD身份驗證和授權端點。 通常是程式設計師模擬此類操作，但無論誰觸發降級事件，該操作都取決於先前與受影響的MVPD商定的安排。

此功能的主要用例是在現場運動或大型活動期間。 在如此高的流量情況下，特定MVPD端點上的負載可能變得過高，從而導致用戶的響應時間很長。 為了在這種情況下保持良好的用戶體驗，程式設計師可以決定觸發可臨時自動驗證/自動授權用戶的降級規則，或通過從可用MVPD清單中刪除MVPD來禁用MVPD。

退化規則僅應用於固定時間段。 儘管此功能的主要客戶是體育頻道和即時新聞頻道，但任何程式設計師都可能希望訪問此功能，因為MVPD服務會時不時地停止。

退化說明：

* 此功能設計為與使用情況監視API一起使用，它提供有關每個MVPD的身份驗證和授權數、平均授權延遲以及完整服務概述所需的其他度量的即時資訊。
* 此功能不允許繞過AdobePrimetim身份驗證服務。 如果黃金時段驗證處於下方，則服務中沒有可用於允許用戶查看內容的機制。 然而，這些網站或應用可以自己繞過黃金時段驗證。
* Adobe當前不會直接引發降級 — 該決定必須始終由與MVPD同意此類條件的特定程式設計師決定。 將來，如果可以通過MVPD達到協定（SLA保護），則黃金時段身份驗證可能會主動觸發降級規則。

<!--
## Related Information {#related}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->
