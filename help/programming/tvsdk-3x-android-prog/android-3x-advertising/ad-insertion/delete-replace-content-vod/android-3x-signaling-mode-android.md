---
description: 可以使用不同的廣告信令模式和廣告元資料組合來標籤、刪除和替換VOD流中的時間範圍。 不同的信令模式和元資料組合導致不同的行為。
title: 廣告信令模式和廣告元資料組合對廣告插入和刪除的影響
exl-id: f42a2db5-642f-4944-87f6-2d7d902a2837
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# 廣告信令模式和廣告元資料組合對廣告插入和刪除的影響 {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

可以使用不同的廣告信令模式和廣告元資料組合來標籤、刪除和替換VOD流中的時間範圍。 不同的信令模式和元資料組合導致不同的行為。

>[!TIP]
>
>當時間範圍和廣告信令模式之間存在衝突時，TVSDK給予時間範圍優先順序。

下表提供了有關信令模式和元資料組合行為的詳細資訊：

**伺服器映射**

| **廣告元資料** | **已建立解析器** | **`PlacementInformations`建立** | **結果行為** |
|--- |--- |--- |--- |
|  | 刪除 | 刪除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已刪除範圍 |
| 刪除，審核 | 刪除，審核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),` <br>`PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 刪除範圍，插入廣告 |
| 奧迪 | 奧迪 | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 插入的廣告 |
| 替換，審慎 | 刪除，審核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 已替換範圍 |
| 標籤 | 自定義廣告 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標籤的範圍 |
| 馬克，奧迪 | CustomAd、Auditue | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標籤範圍，未插入廣告 |

**清單提示**

| 廣告元資料 | 已建立解析器 | `PlacementInformations` 建立 | 結果行為 |
|--- |--- |--- |--- |
| 奧迪 | 奧迪 | `PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | 插入的廣告 |
| 刪除，審核 | 刪除，審核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)`<br>`PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | 刪除範圍，插入廣告 |
| 馬克，奧迪 | 馬克，奧迪 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標籤範圍，未插入廣告 |
| 刪除 | 刪除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已刪除範圍 |
| 標籤 | 自定義廣告 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標籤的範圍 |
| 替換，審慎 | 刪除，審核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 已替換範圍 |

**自定義時間範圍**

| 廣告元資料 | 已建立解析器 | `PlacementInformations` 建立 | 結果行為 |
|--- |--- |--- |--- |
| 刪除 | 刪除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已刪除範圍 |
| 刪除，審核 | 刪除，審核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已刪除範圍，未插入廣告 |
| 奧迪 | 奧迪 | 無 | 未插入廣告 |
| 替換，審慎 | 刪除，審核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 用廣告替換的範圍 |
| 標籤 | 自定義廣告 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標籤的範圍 |
| 馬克，奧迪 | 定制廣告，審美 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標籤範圍，未插入廣告 |

**未設定（預設）**

| 廣告元資料 | 已建立解析器 | `PlacementInformations` 建立 | 結果行為 |
|--- |--- |--- |--- |
| 刪除 | 刪除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已刪除範圍 |
| 刪除，審核 | 刪除，審核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 刪除範圍，插入廣告 |
| 奧迪 | 奧迪 | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 插入的廣告 |
| 替換，審慎 | 刪除，審核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 用廣告替換的範圍 |
| 標籤 | 自定義廣告 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標籤的範圍 |
| 馬克，奧迪 | CustomAd、Auditue | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 標籤的範圍 |
