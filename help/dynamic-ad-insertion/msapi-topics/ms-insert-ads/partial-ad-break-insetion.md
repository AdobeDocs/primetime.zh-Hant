---
description: 部分廣告插播(PABI)功能模仿電視的體驗，其中，如果使用者加入中間廣告插播內的即時串流，則會顯示中間廣告，而非前段廣告或板片廣告。
seo-description: 部分廣告插播(PABI)功能模仿電視的體驗，其中，如果使用者加入中間廣告插播內的即時串流，則會顯示中間廣告，而非前段廣告或板片廣告。
seo-title: 部分插入廣告分段
title: 部分插入廣告分段
uuid: a0c1ae34-0f8d-4401-97fe-45a2ea40d08d
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# 部分廣告插入{#partial-ad-break-insertion}

部分廣告插播(PABI)功能模仿電視的體驗，其中，如果使用者加入中間廣告插播內的即時串流，則會顯示中間廣告，而非前段廣告或板片廣告。

當廣告伺服器傳回即時串流的前段廣告時，資訊清單伺服器會在即時點之前插入前段廣告插播，並插入EXT-X-START標籤，其TIMEOFFSET值指向前段廣告插播的開始。 此預設行為可確保在即時點播放內容之前播放整個前段廣告插播。 如果使用者在即時點接近中段廣告插播時加入串流，則使用者會在即時點顯示中段廣告插播前段廣告插播。

PABI功能指示資訊清單伺服器忽略前段廣告插播，並將EXT-X-START:TIMEOFFSET值設定為即時點中段廣告的開頭。 如此可確保使用者不必檢視前段廣告插播，就能看到目前在即時點播放的整個中段廣告。

>[!NOTE]
>
>此功能僅適用於即時串流。 資訊清單伺服器依預設會將前段廣告插入VOD播放清單上。

>[!NOTE]
>
>若要啟用PABI，您需要在引導URL中指定[query_params](../../msapi-topics/ms-getting-started/ms-api-query-params.md)。

>[!NOTE]
>
>[EXT-X-START](https://tools.ietf.org/html/rfc8216#section-4.3.5.2)是標準HLS標籤，指示播放清單中的首選起點。

## 建議{#section_4CF0733B14504F2A99690310B9F3B130}

* 使用用戶端追蹤，因為用戶端對追蹤信標的觸發有更多的控制權。
* 如果播放器支援EXT-X-START，則部分廣告插播應僅用於伺服器端追蹤模式。