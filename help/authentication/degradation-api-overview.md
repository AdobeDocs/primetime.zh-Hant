---
title: 降級API概述
description: 降級API概述
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# 降級API概述 {#degradation-api-overview}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 一般資訊 {#general_info}

>[!NOTE]
>
>此API不公開提供。 請連絡您的Adobe代表以取得可用性更新。

此功能提供整合(程式設計人員、MVPD和Adobe)中的三大主要方之一，可暫時略過特定MVPD驗證和授權端點。 通常是程式設計人員模擬此類操作，但無論誰觸發了降級事件，該操作都取決於先前與受影響的MVPD達成的協定。

此功能的主要使用案例發生在即時運動或大型活動期間。 在如此高的流量情況下，特定MVPD端點的負載可能會變得過高，導致使用者的回應時間很長。 為了在這種情況下保持良好的用戶體驗，程式設計師可以決定觸發可臨時自動驗證/自動授權用戶的降級規則，或者通過從可用的MVPD清單中刪除MVPD來禁用MVPD。

退化規則只適用於固定時間段。 雖然此功能的主要客戶是體育頻道和即時新聞頻道，但是任何程式設計師都可能希望訪問此功能，因為MVPD服務確實會時不時地關閉。

退化說明：

* 此功能與使用情況監控API搭配使用，可提供每個MVPD的驗證和授權數量、平均授權延遲和完整服務概覽所需的其他量度的即時資訊。
* 此功能不允許略過AdobePrimetim驗證服務。 如果Primetime驗證關閉，服務內沒有可用來讓使用者查看內容的機制。 不過，這些網站或應用程式可自行繞過Primetime驗證。
* Adobe目前不會直接引發降級 — 此決定必須始終由與MVPD協定的特定程式設計師負責。 未來若能與MVPD達成協定（SLA保護）,Primetime驗證可能會主動觸發降級規則。

<!--
## Related Information {#related}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->