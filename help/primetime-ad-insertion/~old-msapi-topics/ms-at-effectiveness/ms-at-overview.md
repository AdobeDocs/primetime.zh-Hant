---
description: 大部分廣告商都需要詳細資訊，瞭解廣告的檢視時間、時間長度，以及成功程度。 最有效的方式是讓用戶端播放器在播放廣告時傳送報表，但資訊清單伺服器也支援伺服器端和混合式廣告追蹤。
seo-description: 大部分廣告商都需要詳細資訊，瞭解廣告的檢視時間、時間長度，以及成功程度。 最有效的方式是讓用戶端播放器在播放廣告時傳送報表，但資訊清單伺服器也支援伺服器端和混合式廣告追蹤。
seo-title: 廣告追蹤
title: 廣告追蹤
uuid: 184b8c36-5e51-42a7-b905-53f2b7b15e49
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# 廣告追蹤{#ad-tracking}

大部分廣告商都需要詳細資訊，瞭解廣告的檢視時間、時間長度，以及成功程度。 最有效的方式是讓用戶端播放器在播放廣告時傳送報表，但資訊清單伺服器也支援伺服器端和混合式廣告追蹤。

啟用和追蹤用戶端時，會指定下列其中一個方法：

* **用** 戶端伺服器會連同廣告銜接播放清單，傳送JSON、VMAP或資訊清單內結構給用戶端，指定追蹤事件和URL。此方法符合互動式廣告局(IAB)的規範

* **伺服** 器端用戶端不參與廣告追蹤。伺服器會傳送任何可以傳送的廣告追蹤資訊。 追蹤資料僅在伺服器端計算，可能與用戶端播放活動不符。 例如，如果使用者未檢視整個廣告，在傳送區段後，伺服器仍會考慮要播放的廣告。

* **Hybrid** 這就像用戶端追蹤，但用戶端會傳送其報表至資訊清單伺服器，並將報表中繼至適當的URL。廣告商會收到與用戶端追蹤相同的資訊。 此模式可容納使用受限Internet訪問的客戶端。