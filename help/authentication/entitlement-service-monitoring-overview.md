---
title: 權利服務監視概述
description: 權利服務監視概述
exl-id: ebd5d650-0a32-4583-9045-5156356494e2
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 0%

---

# 權利服務監視概述 {#entitlement-service-monitoring-overview}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 導言 {#introduction}

TVE網站和應用需要全天候可用，因此客戶需要即時瞭解權利事件以便盡快發現和糾正問題。 他們還需要分析每月資料，以確定哪些平台提供了大部分流量，哪些平台可能實施不善，轉換率也差。

權利服務監控(ESM)為程式設計師和MVPD提供資料饋送，以即時查看其身份驗證和授權事件。 從Adobe Primetime認證系統收集資料，並通過REST風格API提供資料。  客戶可以直接使用資料，也可以在自己定製的操作控制板內使用資料。

ESM系統的核心要素是其指標和維度。 ESM根據維選擇生成包含聚合度量的報告。 當Adobe Pass事件記錄在PST時區中時，ESM報告也可在PST時區中提供。 

ESM API通常不可用。  有關可用性問題，請與Adobe代表聯繫。

## 面向程式設計師的ESM {#esm-for-programmers}

### 程式設計師可以監視以下度量： {#programmers-monitor-metrics}


| *度量名稱* | *說明* |
|-------------------------|--------------------------|
| authn嘗試 | 啟動的驗證流數 |
| 授權成功 | 客戶端成功獲取的驗證令牌數 |
| 授權掛起 | 成功生成的驗證令牌數（忽略客戶端是否實際獲得） |
| 驗證失敗 | 通過外部系統執行的失敗身份驗證數。 |
| 無客戶端令牌 | 成功發出的無客戶端令牌數 |
| 無客戶端故障 | 嘗試從無客戶端API接收令牌失敗的次數 |
| authz嘗試 | 嘗試的授權數 |
| authz成功 | 成功授權數 |
| authz失敗 | 應用程式級MVPD拒絕的授權數 |
| authz拒絕 | 由於DoS攻擊預防而被Adobe服務提供商視為惡意並被拒絕的授權嘗試數 |
| authz延遲 | 在MVPD的終結點上花費的總毫秒數 |
| 媒體令牌 | 生成的短媒體令牌數（與播放請求數同步） |
| 唯一帳戶 | 在所選時間間隔內執行權利(AuthN / AuthZ)操作的唯一用戶數。 （此度量僅在請求每日值時才顯示。） </br> 這是為每個單獨的資料中心計算的。 未請求「dc」維時，將不顯示此度量。 |
| 唯一會話 | 在所選時間間隔內對Adobe Primetime身份驗證服務執行身份驗證流調用的唯一會話數。 （此度量僅在請求每日值時才顯示。） </br> 這是為每個單獨的資料中心計算的。 未請求「dc」維時，將不顯示此度量。 |
| 計數 | 用於面向事件的報告的簡單計數器 |

</br>

### 程式設計師可以按以下維篩選上面列出的度量： {#progr-filter-metrics}


| *Dimension名稱* | *說明* |
|---|---|
| 年 | 4位數年份 |
| 月 | 年月(1-12) |
| 天 | 當月(1-31) |
| 小時 | 一天中的某個小時 |
| 分鐘 | 每小時的分鐘 |
| 媒體公司 | 擁有啟動用戶權利流程的網站的媒體公司 |
| 直流 | （資料中心）接收請求的主區域。 |
| 代理 | 代理MVPD（將為直接整合的「直接」） |
| mvpd | 負責向用戶授予權利的MVPD |
| 請求者ID | 用於執行權利請求的請求者ID |
| 通道 | 通道網站，從資源欄位中提取（如果提供，則從MRSS負載中提取作為通道/標題，或者如果它不是RSS格式則映射到資源值）。 |
| 資源ID | 授權請求中涉及的實際資源標題（如果提供，則從MRSS負載中提取為項/標題） |
| 設備 | 設備平台（PC、移動、控制台等） |
| ea | 當通過外部系統執行認證流時，外部認證提供器。 </br> 值可以是： </br> - N/A — 驗證由黃金時段驗證提供 </br> -Apple — 提供身份驗證的外部系統為Apple |
| os家族 | 在設備上運行的作業系統 |
| 瀏覽器家族 | 用於訪問Adobe Primetime身份驗證的用戶代理 |
| 卡特 | 當前用於無客戶端的設備平台（備用）。 </br>  值可以是： </br> - N/A — 事件不是源於無客戶端SDK </br>  — 未知 — 由於來自無客戶端API的deviceType參數是可選的，因此有調用不包含任何值。 </br>  — 通過Clientless API發送的任何其他值，如xbox、appletv、roku等。 </br> |
| 平台版本 | 無客戶端SDK的版本 |
| os類型 | 在設備上運行的作業系統，可選（當前未使用） |
| 瀏覽器版本 | 用戶代理版本 |
| sdk類型 | 使用的客戶端SDK(Flash、HTML5、Android本機、iOS、無客戶端等) |
| sdk版本 | Adobe Primetime身份驗證客戶端SDK的版本 |
| 事件 | Adobe Primetime身份驗證事件名稱 |
| 原因 | 失敗的原因，如Adobe Primetime身份驗證報告的 |
| sso類型 | 基礎SSO機制：平台/被動/adobe。 指示通過在其他應用程式中重用AuthN而發出授權令牌 |

## MVPD的ESM {#esm-for-mvpds}

### MVPD可以監視以下度量：

| *度量名稱* | *說明* |
|---|---|
| authn嘗試 | 啟動的驗證流數 |
| 授權成功 | 客戶端成功獲取的驗證令牌數 |
| 授權掛起 | 成功生成的驗證令牌數（忽略客戶端是否實際獲得） |
| 驗證失敗 | 通過外部系統執行的失敗身份驗證數。 |
| authz嘗試 | 嘗試的授權數 |
| authz成功 | 成功授權數 |
| authz失敗 | 應用程式級MVPD拒絕的授權數 |
| authz拒絕 | 由於DoS攻擊預防而被Adobe服務提供商視為惡意並被拒絕的授權嘗試數 |
| authz延遲 | 在MVPD的終結點上花費的總毫秒數 |

### MVPD可以篩選以下維列出的度量：

| *Dimension名稱* | *說明* |
|---|---|
| 年 | 4位數年份 |
| 月 | 年月(1-12) |
| 天 | 當月(1-31) |
| 小時 | 一天中的某個小時 |
| 分鐘 | 每小時的分鐘 |
| 請求者ID | 用於執行權利請求的請求者ID |
| ea | 當通過外部系統執行認證流時，外部認證提供器。 </br> 值可以是： </br> - N/A — 驗證由黃金時段驗證提供 </br> -Apple — 提供身份驗證的外部系統為Apple |
| 卡特 | 當前用於無客戶端的設備平台（備用）。 </br>  值可以是： </br> - N/A — 事件不是源於無客戶端SDK </br>  — 未知 — 由於來自無客戶端API的deviceType參數是可選的，因此有調用不包含任何值。 </br>  — 通過Clientless API發送的任何其他值，如xbox、appletv、roku等。 </br> |
| sdk類型 | 使用的客戶端SDK(Flash、HTML5、Android本機、iOS、無客戶端等) |


## 使用案例 {#use-cases}

您可以將ESM資料用於以下使用情形：

- **監視**  — 操作或監控團隊可以建立每分鐘調用API的儀表板或圖表。 使用顯示的資訊，他們可以在問題出現時（使用黃金時段驗證或使用MVPD）檢測問題。  

- **調試/質量測試**  — 由於資料也按平台、設備、瀏覽器和作業系統進行分解，因此分析使用模式可以查明特定組合（如OSX上的Safari）上的問題。  

- **分析**  — 所提供的資料可用於補充/審計通過Adobe Analytics或其他分析工具收集的客戶端資料。

<!--
## Related Information {#related-information}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->
