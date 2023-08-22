---
title: 軟體權利檔案服務監視概觀
description: 軟體權利檔案服務監視概觀
exl-id: ebd5d650-0a32-4583-9045-5156356494e2
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 0%

---

# 軟體權利檔案服務監視概觀 {#entitlement-service-monitoring-overview}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要Adobe的目前授權。 不允許未經授權的使用。

## 簡介 {#introduction}

TVE網站和應用程式需要全天候可用，因此客戶需要即時洞察權益事件，以儘快偵測和更正問題。 他們也需要分析每月資料，以判斷哪些平台提供大部分的流量，以及哪些平台可能有不良的實作和不良的轉換率。

軟體權利檔案服務監控(ESM)為程式設計師和MVPD提供資料摘要，可即時顯示其驗證和授權事件。 資料是從Adobe Primetime驗證系統收集，並透過RESTful API提供。  客戶可以直接使用資料，或是從他們自己的自訂運作控制面板中使用資料。

ESM系統的核心元素是其量度和維度。 ESM會根據維度選取專案產生內含彙總量度的報表。 由於Adobe Pass事件是以PST時區記錄，因此ESM報表也以PST時區提供。

ESM API並非為一般可用功能。  如需瞭解可用性問題，請聯絡您的Adobe代表。

## 適用於程式設計師的ESM {#esm-for-programmers}

### 程式設計師可以監控以下量度： {#programmers-monitor-metrics}


| *量度名稱* | *說明* |
|-------------------------|--------------------------|
| authn-attempts | 已起始的驗證流程數 |
| 驗證成功 | 使用者端成功取得之驗證權杖的數量 |
| authn-pending | 成功產生的驗證權杖數（無論使用者端是否實際取得） |
| authn-failed | 透過外部系統執行的失敗驗證數目。 |
| 無使用者端權杖 | 成功發出的無使用者端權杖數量 |
| 無使用者端失敗 | 嘗試從無使用者端API接收權杖失敗的次數 |
| authz嘗試 | 嘗試授權的次數 |
| authz成功 | 成功的授權數目 |
| authz失敗 | MVPD在應用程式層級拒絕授權的數目 |
| authz-rejected | Adobe服務提供者視為惡意授權，且因DoS攻擊預防而拒絕的授權嘗試次數 |
| authz延遲 | 在MVPD端點上花費的總毫秒數 |
| media-token | 產生的簡短媒體代號數量（與播放要求數量一致） |
| 不重複帳戶 | 在選取的時間間隔內執行權利(AuthN / AuthZ)動作的不重複使用者數目。 （此量度僅在要求每日值時顯示。） </br> 每個個別資料中心都會計算此值。 當未要求「dc」維度時，將不會顯示此量度。 |
| 不重複工作階段 | 在選取的時間間隔內，對Adobe Primetime驗證服務執行驗證流程呼叫的唯一工作階段數目。 （此量度僅在要求每日值時顯示。） </br> 每個個別資料中心都會計算此值。 當未要求「dc」維度時，將不會顯示此量度。 |
| count | 用於事件導向報表中的簡單計數器 |

</br>

### 程式設計師可依下列維度篩選上述量度： {#progr-filter-metrics}


| *Dimension名稱* | *說明* |
|---|---|
| 年 | 4位數的年份 |
| 月 | 月份(1-12) |
| 天 | 當月日期(1-31) |
| 小時 | 一天中的第幾個小時 |
| 分鐘 | 一小時中的第幾分鐘 |
| media-company | 擁有為使用者啟動權益程式的網站的媒體公司 |
| dc | （資料中心）收到請求的本位區域。 |
| proxy | Proxy MVPD （直接整合則為「直接」） |
| mvpd | 負責授與使用者權利的MVPD |
| 請求者ID | 用來執行軟體權利檔案要求的要求者ID |
| 頻道 | 頻道網站，從資源欄位擷取(若提供，從MRSS裝載擷取作為頻道/標題，否則對應至資源值（若不是RSS格式）。 |
| resource-id | 授權請求中涉及的實際資源標題（從MRSS承載中擷取，作為專案/標題，如果提供） |
| 裝置 | 裝置平台（電腦、行動裝置、主控台等） |
| eap | 透過外部系統執行驗證流程時的外部驗證提供者。 </br> 值可以是： </br> - N/A - Primetime驗證所提供的驗證 </br> - Apple — 提供驗證的外部系統為Apple |
| os系列 | 裝置上執行的作業系統 |
| browser-family | 用於存取Adobe Primetime驗證的使用者代理 |
| cdt | 裝置平台（替代方案），目前用於無使用者端。 </br>  值可以是： </br>  — 不適用 — 事件並非源自無使用者端SDK </br>  — 未知 — 由於無使用者端API中的deviceType引數是選用專案，因此有些呼叫不會包含任何值。 </br>  — 透過無使用者端API傳送的任何其他值，例如xbox、appletv、roku等。 </br> |
| platform-version | 無使用者端SDK的版本 |
| os-type | 裝置上執行的作業系統，替代方案（目前未使用） |
| browser-version | 使用者代理程式版本 |
| sdk-type | 使用的使用者端SDK (Flash、HTML5、Android原生、iOS、無使用者端等) |
| sdk-version | Adobe Primetime驗證使用者端SDK的版本 |
| 事件 | Adobe Primetime驗證事件名稱 |
| 原因 | Adobe Primetime驗證所報告的失敗原因 |
| sso-type | 底層SSO機制：platform/passive/adobe。 表示授權權杖是在其他應用程式中重複使用AuthN所發出 |

## MVPD的ESM {#esm-for-mvpds}

### MVPD可以監督下列測量結果：

| *量度名稱* | *說明* |
|---|---|
| authn-attempts | 已起始的驗證流程數 |
| 驗證成功 | 使用者端成功取得之驗證權杖的數量 |
| authn-pending | 成功產生的驗證權杖數（無論使用者端是否實際取得） |
| authn-failed | 透過外部系統執行的失敗驗證數目。 |
| authz嘗試 | 嘗試授權的次數 |
| authz成功 | 成功的授權數目 |
| authz失敗 | MVPD在應用程式層級拒絕授權的數目 |
| authz-rejected | Adobe服務提供者視為惡意授權，且因DoS攻擊預防而拒絕的授權嘗試次數 |
| authz延遲 | 在MVPD端點上花費的總毫秒數 |

### MVPD可依下列維度篩選上述量度：

| *Dimension名稱* | *說明* |
|---|---|
| 年 | 4位數的年份 |
| 月 | 月份(1-12) |
| 天 | 當月日期(1-31) |
| 小時 | 一天中的第幾個小時 |
| 分鐘 | 一小時中的第幾分鐘 |
| 請求者ID | 用來執行軟體權利檔案要求的要求者ID |
| eap | 透過外部系統執行驗證流程時的外部驗證提供者。 </br> 值可以是： </br> - N/A - Primetime驗證所提供的驗證 </br> - Apple — 提供驗證的外部系統為Apple |
| cdt | 裝置平台（替代方案），目前用於無使用者端。 </br>  值可以是： </br>  — 不適用 — 事件並非源自無使用者端SDK </br>  — 未知 — 由於無使用者端API中的deviceType引數是選用專案，因此有些呼叫不會包含任何值。 </br>  — 透過無使用者端API傳送的任何其他值，例如xbox、appletv、roku等。 </br> |
| sdk-type | 使用的使用者端SDK (Flash、HTML5、Android原生、iOS、無使用者端等) |


## 使用案例 {#use-cases}

ESM資料可用於下列使用案例：

- **監視**  — 操作或監控團隊可以建立每分鐘呼叫API的儀表板或圖表。 使用顯示的資訊，他們可以在問題出現的那一分鐘偵測到問題（Primetime驗證或MVPD）。

- **偵錯/品質測試**  — 由於資料也會依平台、裝置、瀏覽器和作業系統劃分，因此分析使用模式可以查明特定組合上的問題（例如OSX上的Safari）。

- **Analytics**  — 提供的資料可用於補充/稽核透過Adobe Analytics或其他分析工具收集的使用者端資料。

<!--
## Related Information {#related-information}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->
