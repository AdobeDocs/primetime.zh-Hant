---
description: 您可以使用不同的廣告訊號模式和廣告中繼資料組合，標籤、刪除和取代VOD串流中的時間範圍。 訊號模式和中繼資料的不同組合會產生不同的行為。
title: 對從廣告訊號模式和廣告中繼資料組合中插入和刪除廣告的影響
exl-id: f42a2db5-642f-4944-87f6-2d7d902a2837
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# 對從廣告訊號模式和廣告中繼資料組合中插入和刪除廣告的影響 {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

您可以使用不同的廣告訊號模式和廣告中繼資料組合，標籤、刪除和取代VOD串流中的時間範圍。 訊號模式和中繼資料的不同組合會產生不同的行為。

>[!TIP]
>
>當時間範圍和廣告訊號模式之間發生衝突時，TVSDK會提供時間範圍優先順序。

下表提供有關訊號模式和中繼資料組合行為的詳細資訊：

**伺服器對應**

| **廣告中繼資料** | **解析器已建立** | **`PlacementInformations`已建立** | **產生的行為** |
|--- |--- |--- |--- |
|  | 刪除 | 刪除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已刪除範圍 |
| 刪除，稽核 | 刪除，稽核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),` <br>`PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 刪除範圍，插入廣告 |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 廣告已插入 |
| 取代，稽核 | 刪除，稽核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 範圍已取代 |
| 標籤 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標示的範圍 |
| 標籤，Auditude | CustomAd， Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 已標籤範圍，未插入廣告 |

**資訊清單提示**

| 廣告中繼資料 | 解析器已建立 | `PlacementInformations` 已建立 | 產生的行為 |
|--- |--- |--- |--- |
| Auditude | Auditude | `PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | 廣告已插入 |
| 刪除，稽核 | 刪除，稽核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)`<br>`PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | 刪除範圍，插入廣告 |
| 標籤，Auditude | 標籤，Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 已標籤範圍，未插入廣告 |
| 刪除 | 刪除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已刪除範圍 |
| 標籤 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標示的範圍 |
| 取代，稽核 | 刪除，稽核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 範圍已取代 |

**自訂時間範圍**

| 廣告中繼資料 | 解析器已建立 | `PlacementInformations` 已建立 | 產生的行為 |
|--- |--- |--- |--- |
| 刪除 | 刪除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已刪除範圍 |
| 刪除，稽核 | 刪除，稽核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 範圍已刪除，未插入廣告 |
| Auditude | Auditude | 無 | 未插入任何廣告 |
| 取代，稽核 | 刪除，稽核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 範圍已取代為廣告 |
| 標籤 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標示的範圍 |
| 標籤，Auditude | 自訂廣告，Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 已標籤範圍，未插入廣告 |

**未設定（預設）**

| 廣告中繼資料 | 解析器已建立 | `PlacementInformations` 已建立 | 產生的行為 |
|--- |--- |--- |--- |
| 刪除 | 刪除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已刪除範圍 |
| 刪除，稽核 | 刪除，稽核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 刪除範圍，插入廣告 |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 廣告已插入 |
| 取代，稽核 | 刪除，稽核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 範圍已取代為廣告 |
| 標籤 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標示的範圍 |
| 標籤，Auditude | CustomAd， Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標示的範圍 |
