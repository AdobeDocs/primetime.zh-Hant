---
description: 部分廣告插播(PABI)功能模仿電視體驗，如果使用者在中段插播中加入即時資料流，使用者會看到中段廣告，而不是前段廣告或石板。
title: 部分廣告插播插入
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# 部分廣告插播插入 {#partial-ad-break-insertion}

部分廣告插播(PABI)功能模仿電視體驗，如果使用者在中段插播中加入即時資料流，使用者會看到中段廣告，而不是前段廣告或石板。

當廣告伺服器傳回即時資料流的前段廣告時，資訊清單伺服器會在即時點之前插入前段廣告插播，並插入EXT-X-START標籤，其TIMEOFFSET值指向前段廣告插播的開始。 此預設行為可確保整個前段廣告插播會在即時點的內容之前播放。 如果使用者在即時點接近中段廣告插播時加入串流，則會在即時點處在中段廣告插播之前向使用者顯示前段廣告插播。

PABI功能會指示資訊清單伺服器忽略前段廣告插播，並將EXT-X-START：TIMEOFFSET值設定為存在於即時點的中段廣告的開頭。 這可確保使用者看到目前在即時點播放的整個中段廣告，而不必檢視前段廣告插播。

>[!NOTE]
>
>此功能僅適用於即時資料流。 根據預設，資訊清單伺服器會將前段廣告插播插入VOD播放清單上方。

>[!NOTE]
>
>若要啟用PABI，您必須指定 [query_params](/help/primetime-ad-insertion/~old-msapi-topics/ms-getting-started/ms-api-query-params.md) 啟動程式URL中的。

>[!NOTE]
>
>此 [EXT-X-START](https://tools.ietf.org/html/rfc8216#section-4.3.5.2) 是標準HLS標籤，可指出播放清單中偏好的起點。

## Recommendations {#section_4CF0733B14504F2A99690310B9F3B130}

* 使用使用者端追蹤，因為使用者端對追蹤信標的引發擁有更多控制權。
* 如果播放器支援EXT-X-START，部分廣告插播應僅用於伺服器端追蹤模式。