---
title: 軟體權利檔案服務監控概述
description: 軟體權利檔案服務監控概述
exl-id: ebd5d650-0a32-4583-9045-5156356494e2
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 0%

---

# 軟體權利檔案服務監控概述 {#entitlement-service-monitoring-overview}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 簡介 {#introduction}

TVE網站和應用程式需要全天候運作，因此客戶需要即時洞察軟體權利檔案事件，以儘快偵測和修正問題。 他們也需要分析每月資料，以判斷哪些平台提供大部分的流量，以及哪些平台可能有不良的實作和不良的轉換率。

軟體權利檔案服務監控(ESM)為程式設計人員和MVPD提供資料摘要，可即時檢視其驗證和授權事件。 資料是從Adobe Primetime驗證系統收集，並透過RESTful API提供。  客戶可以直接使用資料，或是從他們自己的自訂操作儀表板中使用資料。

ESM系統的核心元素是其量度和維度。 ESM會根據維度選擇產生包含彙總量度的報表。 由於Adobe Pass事件是以PST時區記錄，因此ESM報表也以PST時區提供。 

ESM API並非一般可用功能。  如需瞭解可用性相關問題，請聯絡您的Adobe代表。

## 適用於程式設計師的ESM {#esm-for-programmers}

### 程式設計師可以監控以下量度： {#programmers-monitor-metrics}


| *量度名稱* | *說明* |
|-------------------------|--------------------------|
| authn-attempts | 已起始的驗證流程數 |
| 驗證成功 | 使用者端成功取得的驗證權杖數目 |
| authn-pending | 成功產生的驗證Token數量（無論使用者端是否實際取得） |
| 驗證失敗 | 透過外部系統執行的失敗驗證數目。 |
| 無使用者端代號 | 成功發出的無使用者端權杖數量 |
| 無使用者端失敗 | 嘗試從無使用者端API接收權杖失敗的次數 |
| authz-attempts | 嘗試授權的數量 |
| authz成功 | 成功的授權數目 |
| authz失敗 | 應用程式層級的MVPD拒絕授權數目 |
| authz-rejected | Adobe服務提供者視為惡意且因DoS攻擊預防而拒絕的授權嘗試次數 |
| authz延遲 | 在MVPD端點上花費的總毫秒數 |
| media-token | 產生的簡短媒體權杖數量（與播放要求數量相同） |
| 不重複帳戶 | 在選取的時間間隔內執行權利(AuthN / AuthZ)動作的不重複使用者數目。 （此量度僅在請求每日值時顯示。） </br> 每個個別資料中心都會計算此值。 未請求「dc」維度時，此量度不會顯示。 |
| 不重複工作階段 | 在選取的時間間隔內對Adobe Primetime驗證服務執行驗證流程呼叫的唯一工作階段數。 （此量度僅在請求每日值時顯示。） </br> 每個個別資料中心都會計算此值。 未請求「dc」維度時，此量度不會顯示。 |
| count | 事件導向報表中使用的簡單計數器 |

</br>

### 程式設計師可依下列維度篩選上方列出的量度： {#progr-filter-metrics}


| *Dimension名稱* | *說明* |
|---|---|
| 年 | 4位數的年份 |
| 月 | 月份(1-12) |
| 日 | 當月日期(1-31) |
| 小時 | 一天中的第幾個小時 |
| 分鐘 | 一小時中的第幾分鐘 |
| media-company | 擁有啟動使用者權益程式的網站的媒體公司 |
| dc | （資料中心）收到請求的本位區域。 |
| proxy | Proxy MVPD （對於直接整合而言將是「直接」的） |
| mvpd | 負責將權利授予使用者的MVPD |
| requestor-id | 用來執行軟體權利檔案要求的要求者ID |
| 頻道 | 頻道網站，從資源欄位擷取（從MRSS裝載擷取並作為頻道/標題，如果提供，或如果它不是RSS格式，則對應到資源值）。 |
| resource-id | 授權請求中涉及的實際資源標題（從MRSS裝載擷取，作為專案/標題，如果提供） |
| 裝置 | 裝置平台（個人電腦、行動裝置、主控台等） |
| eap | 透過外部系統執行驗證流程時的外部驗證提供者。 </br> 值可以是： </br> - N/A - Primetime驗證會提供驗證 </br> - Apple — 提供驗證的外部系統為Apple |
| os系列 | 裝置上執行的作業系統 |
| browser-family | 用於存取Adobe Primetime驗證的使用者代理 |
| cdt | 裝置平台（替代方案），目前用於無使用者端。 </br>  值可以是： </br> - N/A — 事件並非源自無使用者端SDK </br>  — 未知 — 由於無使用者端API中的deviceType引數是選用的，因此有些呼叫不包含任何值。 </br>  — 透過無使用者端API傳送的任何其他值，例如xbox、appletv、roku等。 </br> |
| platform-version | Clientless SDK的版本 |
| os-type | 裝置上執行的作業系統，替代方案（目前未使用） |
| browse-version | 使用者代理程式版本 |
| sdk-type | 使用的使用者端SDK (Flash、HTML5、Android原生、iOS、無使用者端等) |
| sdk-version | Adobe Primetime驗證使用者端SDK的版本 |
| 事件 | Adobe Primetime驗證事件名稱 |
| 原因 | 失敗的原因，如Adobe Primetime驗證所報告 |
| sso-type | 底層SSO機制： platform/passive/adobe。 表示授權權杖是在其他應用程式中重複使用AuthN所發出 |

## MVPD的ESM {#esm-for-mvpds}

### MVPD可以監視下列測量結果：

| *量度名稱* | *說明* |
|---|---|
| authn-attempts | 已起始的驗證流程數 |
| 驗證成功 | 使用者端成功取得的驗證權杖數目 |
| authn-pending | 成功產生的驗證Token數量（無論使用者端是否實際取得） |
| 驗證失敗 | 透過外部系統執行的失敗驗證數目。 |
| authz-attempts | 嘗試授權的數量 |
| authz成功 | 成功的授權數目 |
| authz失敗 | 應用程式層級的MVPD拒絕授權數目 |
| authz-rejected | Adobe服務提供者視為惡意且因DoS攻擊預防而拒絕的授權嘗試次數 |
| authz延遲 | 在MVPD端點上花費的總毫秒數 |

### MVPD可依下列維度篩選上述量度：

| *Dimension名稱* | *說明* |
|---|---|
| 年 | 4位數的年份 |
| 月 | 月份(1-12) |
| 日 | 當月日期(1-31) |
| 小時 | 一天中的第幾個小時 |
| 分鐘 | 一小時中的第幾分鐘 |
| requestor-id | 用來執行軟體權利檔案要求的要求者ID |
| eap | 透過外部系統執行驗證流程時的外部驗證提供者。 </br> 值可以是： </br> - N/A - Primetime驗證會提供驗證 </br> - Apple — 提供驗證的外部系統為Apple |
| cdt | 裝置平台（替代方案），目前用於無使用者端。 </br>  值可以是： </br> - N/A — 事件並非源自無使用者端SDK </br>  — 未知 — 由於無使用者端API中的deviceType引數是選用的，因此有些呼叫不包含任何值。 </br>  — 透過無使用者端API傳送的任何其他值，例如xbox、appletv、roku等。 </br> |
| sdk-type | 使用的使用者端SDK (Flash、HTML5、Android原生、iOS、無使用者端等) |


## 使用案例 {#use-cases}

您可以將ESM資料用於下列使用案例：

- **監視**  — 作業或監控團隊可建立每分鐘呼叫API的儀表板或圖表。 使用顯示的資訊，他們可以在問題出現的一分鐘偵測問題（使用Primetime驗證或MVPD）。  

- **偵錯/品質測試**  — 由於資料也會依平台、裝置、瀏覽器和OS劃分，因此分析使用模式可以查明特定組合上的問題（例如OSX上的Safari）。  

- **分析**  — 提供的資料可用於補充/稽核透過Adobe Analytics或其他分析工具收集的使用者端資料。

<!--
## Related Information {#related-information}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->
