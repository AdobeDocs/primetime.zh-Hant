---
description: 部分廣告中斷插入(PABI)功能模仿電視的體驗，其中，如果用戶在中間滾動中斷內加入即時流，則用戶被顯示為中間滾動廣告，而不是預滾動廣告或石板。
title: 部分廣告分段插入
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# 部分廣告分段插入 {#partial-ad-break-insertion}

部分廣告中斷插入(PABI)功能模仿電視的體驗，其中，如果用戶在中間滾動中斷內加入即時流，則用戶被顯示為中間滾動廣告，而不是預滾動廣告或石板。

當廣告伺服器返回即時流的預滾廣告時，清單伺服器將在即時點之前注入預滾廣告中斷，並插入EXT-X-START標籤，其TIMEOFFSET值指向預滾廣告中斷的開始。 此預設行為可確保在即時點上的內容之前播放整個預播廣告片段。 如果用戶在即時點接近中間滾動和中斷時加入流，則用戶將在即時點中中間滾動和中斷之前顯示預滾動和中斷。

PABI功能指示清單伺服器忽略前滾和中斷，並將EXT-X-START:TIMEOFFSET值設定為即時點上出現的中滾和開始。 這確保用戶能夠看到當前在即時點播放的整個中間卷廣告，而不必查看預卷廣告片段。

>[!NOTE]
>
>此功能僅適用於即時流。 預設情況下，清單伺服器將前滾和中斷插入VOD播放清單上。

>[!NOTE]
>
>要啟用PABI，您需要指定 [查詢_params](/help/primetime-ad-insertion/~old-msapi-topics/ms-getting-started/ms-api-query-params.md) 的子菜單。

>[!NOTE]
>
>的 [EXT-X-START](https://tools.ietf.org/html/rfc8216#section-4.3.5.2) 是標準HLS標籤，它指示播放清單中的首選起始點。

## Recommendations {#section_4CF0733B14504F2A99690310B9F3B130}

* 使用客戶端跟蹤，因為客戶端對跟蹤信標的觸發具有更大的控制。
* 僅當播放器支援EXT-X-START時，部分廣告中斷才應與伺服器端跟蹤模式一起使用。