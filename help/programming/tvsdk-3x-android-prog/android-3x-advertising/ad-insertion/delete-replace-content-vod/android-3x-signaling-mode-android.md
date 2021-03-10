---
description: 您可以使用不同的廣告信令模式和廣告中繼資料組合來標籤、刪除和取代VOD串流中的時間範圍。 不同的信令模式和元資料組合導致不同的行為。
title: 從廣告信號模式和廣告中繼資料組合中對廣告插入和刪除的影響
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---


# 從廣告信號模式和廣告中繼資料組合{#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}對廣告插入和刪除的影響

您可以使用不同的廣告信令模式和廣告中繼資料組合來標籤、刪除和取代VOD串流中的時間範圍。 不同的信令模式和元資料組合導致不同的行為。

>[!TIP]
>
>當時間範圍與廣告信令模式發生衝突時，TVSDK會給予時間範圍優先順序。

下表提供有關信令模式和元資料組合行為的詳細資訊：

**伺服器地圖**

| **廣告中繼資料** | **已建立解析器** | **`PlacementInformations`已建立** | **結果行為** |
|--- |--- |--- |--- |
|  | 刪除 | 刪除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已刪除範圍 |
| 刪除， Auditude | 刪除， Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),` <br>`PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 刪除範圍，插入廣告 |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 插入的廣告 |
| 取代，Auditude | 刪除， Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 已取代範圍 |
| 標籤 | 自訂廣告 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標籤的範圍 |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標籤範圍，未插入廣告 |

**資訊清單提示**

| 廣告中繼資料 | 已建立解析器 | `PlacementInformations` 已建立 | 結果行為 |
|--- |--- |--- |--- |
| Auditude | Auditude | `PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | 插入的廣告 |
| 刪除， Auditude | 刪除， Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)`<br>`PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | 刪除範圍，插入廣告 |
| Mark, Auditude | Mark, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標籤範圍，未插入廣告 |
| 刪除 | 刪除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已刪除範圍 |
| 標籤 | 自訂廣告 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標籤的範圍 |
| 取代，Auditude | 刪除， Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 已取代範圍 |

**自訂時間範圍**

| 廣告中繼資料 | 已建立解析器 | `PlacementInformations` 已建立 | 結果行為 |
|--- |--- |--- |--- |
| 刪除 | 刪除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已刪除範圍 |
| 刪除， Auditude | 刪除， Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已刪除範圍，未插入廣告 |
| Auditude | Auditude | 無 | 未插入廣告 |
| 取代，Auditude | 刪除， Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 以廣告取代範圍 |
| 標籤 | 自訂廣告 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標籤的範圍 |
| Mark, Auditude | 自訂廣告、Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標籤範圍，未插入廣告 |

**未設定（預設）**

| 廣告中繼資料 | 已建立解析器 | `PlacementInformations` 已建立 | 結果行為 |
|--- |--- |--- |--- |
| 刪除 | 刪除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已刪除範圍 |
| 刪除， Auditude | 刪除， Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 刪除範圍，插入廣告 |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 插入的廣告 |
| 取代，Auditude | 刪除， Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 以廣告取代範圍 |
| 標籤 | 自訂廣告 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標籤的範圍 |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標籤的範圍 |