---
title: 權利服務監視概述
description: 權利服務監視概述
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 0%

---


# 權利服務監視概述 {#entitlement-service-monitoring-overview}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 簡介 {#introduction}

TVE網站和應用程式需要24/7供使用，因此客戶需要即時掌握權益事件，以便盡快偵測及修正問題。 他們也需要分析每月資料，以判斷哪些平台提供大量流量，哪些平台可能實施錯誤且轉換率不彰。

權利服務監控(ESM)為程式設計師和MVPD提供資料摘要，以便即時查看其驗證和授權事件。 資料會從Adobe Primetime驗證系統收集，並透過RESTful API提供。  客戶可以直接使用資料，或從自訂的操作控制面板內使用。

ESM系統的核心要素是其指標和維度。 ESM會根據維選擇生成包含聚合度量的報告。 由於Adobe Pass事件記錄在PST時區，因此ESM報告也可在PST時區中使用。 

ESM API不普遍可用。  如有可用性問題，請聯絡您的Adobe代表。

## 面向程式設計師的ESM {#esm-for-programmers}

### 程式設計師可以監控下列量度： {#programmers-monitor-metrics}


| *量度名稱* | *說明* |
|-------------------------|--------------------------|
| authn-attempts | 啟動的驗證流數 |
| authn-successful | 客戶端成功獲取的驗證令牌數 |
| authn-pending | 成功生成的驗證令牌數（忽略客戶端是否實際獲取） |
| authn-failed | 通過外部系統執行的失敗身份驗證數。 |
| 無用戶端代號 | 已成功發出無客戶端令牌的數量 |
| 無客戶端故障 | 嘗試從無用戶端API接收代號失敗的次數 |
| authz-attempts | 嘗試的授權數 |
| authz-successful | 成功授權數 |
| authz失敗 | MVPD在應用程式級別拒絕的授權數 |
| authz-rejected | 由於DoS攻擊預防而被Adobe服務提供者視為惡意且遭拒的授權嘗試數 |
| authz-latency | 在MVPD端點上逗留的毫秒總數 |
| media-tokens | 產生的短媒體代號數（與播放請求數同化） |
| 唯一帳戶 | 在所選時間間隔內執行權限(AuthN / AuthZ)動作的不重複使用者人數。 （此量度只會在請求每日值時顯示。） </br> 這會針對每個個別資料中心進行計算。 未要求「dc」維度時，將不會顯示此量度。 |
| 不重複工作階段 | 在所選時間間隔內對Adobe Primetime驗證服務執行驗證流調用的唯一會話數。 （此量度只會在請求每日值時顯示。） </br> 這會針對每個個別資料中心進行計算。 未要求「dc」維度時，將不會顯示此量度。 |
| 計數 | 用於事件導向報表的簡單計數器 |

</br>

### 程式設計師可依下列維度篩選上述量度： {#progr-filter-metrics}


| *Dimension名稱* | *說明* |
|---|---|
| 年 | 4位數的年份 |
| 月 | 月份(1-12) |
| 天 | 當月(1-31) |
| 小時 | 一天中的第幾個小時 |
| 分鐘 | 該小時的分鐘 |
| 媒體公司 | 擁有啟動用戶權限進程的網站的媒體公司 |
| dc | （資料中心）收到請求的首頁區域。 |
| 代理 | 代理MVPD（直接整合的「直接」） |
| mvpd | 負責授與使用者權限的MVPD |
| requestor-id | 用於執行權限要求的要求者ID |
| 頻道 | 管道網站，從資源欄位擷取（如果提供，則從MRSS裝載擷取為管道/標題，如果不是RSS格式，則對應至資源值）。 |
| resource-id | 授權請求中涉及的實際資源標題(從MRSS裝載中提取，作為項目/標題（如果提供）) |
| 裝置 | 裝置平台（PC、行動裝置、主控台等） |
| eap | 當通過外部系統執行驗證流時，外部驗證提供程式。 </br> 值可以是： </br>  — 不適用 — 驗證是由Primetime驗證提供 </br> - Apple — 提供驗證的外部系統為Apple |
| os系列 | 在設備上運行的作業系統 |
| 瀏覽器系列 | 用於存取Adobe Primetime驗證的使用者代理 |
| cdt | 裝置平台（替代），目前用於無用戶端。 </br>  值可以是： </br>  — 不適用 — 事件並非源自於無用戶端SDK </br>  — 未知 — 由於來自無用戶端API的deviceType參數為選用，因此有些呼叫不包含任何值。 </br>  — 透過無用戶端API傳送的任何其他值，例如xbox、appletv、roku等。 </br> |
| platform-version | 無用戶端SDK的版本 |
| os-type | 在設備上運行的作業系統，替代（當前未使用） |
| browser-version | 使用者代理版本 |
| sdk-type | 使用的用戶端SDK(Flash、HTML5、Android原生、iOS、無用戶端等) |
| sdk-version | Adobe Primetime驗證用戶端SDK的版本 |
| 事件 | Adobe Primetime驗證事件名稱 |
| 原因 | 失敗的原因，如Adobe Primetime驗證報告 |
| sso-type | 基礎的SSO機制：platform/passive/adobe。 指出授權權杖是透過重複使用不同應用程式中的AuthN而發出 |

## MVPD的ESM {#esm-for-mvpds}

### MVPD可監控下列量度：

| *量度名稱* | *說明* |
|---|---|
| authn-attempts | 啟動的驗證流數 |
| authn-successful | 客戶端成功獲取的驗證令牌數 |
| authn-pending | 成功生成的驗證令牌數（忽略客戶端是否實際獲取） |
| authn-failed | 通過外部系統執行的失敗身份驗證數。 |
| authz-attempts | 嘗試的授權數 |
| authz-successful | 成功授權數 |
| authz失敗 | MVPD在應用程式級別拒絕的授權數 |
| authz-rejected | 由於DoS攻擊預防而被Adobe服務提供者視為惡意且遭拒的授權嘗試數 |
| authz-latency | 在MVPD端點上逗留的毫秒總數 |

### MVPD可依下列維度篩選上述量度：

| *Dimension名稱* | *說明* |
|---|---|
| 年 | 4位數的年份 |
| 月 | 月份(1-12) |
| 天 | 當月(1-31) |
| 小時 | 一天中的第幾個小時 |
| 分鐘 | 該小時的分鐘 |
| requestor-id | 用於執行權限要求的要求者ID |
| eap | 當通過外部系統執行驗證流時，外部驗證提供程式。 </br> 值可以是： </br>  — 不適用 — 驗證是由Primetime驗證提供 </br> - Apple — 提供驗證的外部系統為Apple |
| cdt | 裝置平台（替代），目前用於無用戶端。 </br>  值可以是： </br>  — 不適用 — 事件並非源自於無用戶端SDK </br>  — 未知 — 由於來自無用戶端API的deviceType參數為選用，因此有些呼叫不包含任何值。 </br>  — 透過無用戶端API傳送的任何其他值，例如xbox、appletv、roku等。 </br> |
| sdk-type | 使用的用戶端SDK(Flash、HTML5、Android原生、iOS、無用戶端等) |


## 使用案例 {#use-cases}

您可以將ESM資料用於以下使用案例：

- **監控**  — 作業或監控團隊可以建立每分鐘呼叫API的控制面板或圖表。 使用顯示的資訊，他們可以在問題出現的那一刻（透過Primetime驗證或MVPD）偵測到問題。  

- **除錯/品質測試**  — 因為資料也會依平台、裝置、瀏覽器和作業系統進行劃分，分析使用模式可找出特定組合（例如OSX上的Safari）的問題。  

- **Analytics**  — 提供的資料可用來補充/稽核透過Adobe Analytics或其他分析工具收集的用戶端資料。

<!--
## Related Information {#related-information}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->