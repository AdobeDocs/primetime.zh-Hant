---
title: 將Primetime驗證伺服器端資料整合至Adobe Analytics
description: 將Primetime驗證伺服器端資料整合至Adobe Analytics
exl-id: c1f1f2a3-c98c-4aed-92ad-1f9bfd80b82b
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 4%

---

# 將Primetime驗證伺服器端資料整合至Adobe Analytics

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

Adobe Primetime驗證客戶想要在Adobe Analytics儀表板中檢視Primetime驗證(Adobe Pass)伺服器端資料，以方便使用。

資料將用於追蹤重要的TVE量度，例如每個MVPD的驗證轉換率、根據MVPD使用者ID的不重複使用者等等。

若使用者端實作已存在，則其不代表取代該使用者端實作，因為若無訪客ID，則無法追蹤使用者活動超過下列特定事件。 如果客戶在Pass呼叫上提供訪客ID，我們可以解鎖其他型別的Analytics整合 — 即時 — 可與現有客戶資料聯結所有Pass事件，如需深入瞭解這種可能整合的新型別，請前往： 」[在Primetime驗證中使用Experience CloudID](/help/authentication/exp-cloud-id-authn.md)&quot;

## 包含的量度 {#metrics-included-int-authn-analyt}

| 事件 | 說明 |
|----------------------------|----------------------------------------------------------------------------------------------------------------------|
| 已要求AuthN | 已起始的驗證流程數 |
| AuthN擱置中 | 成功產生的驗證Token數量（無論使用者端是否實際取得） |
| 驗證正常 | 使用者成功取得的驗證權杖數量 |
| 已要求AuthZ | 嘗試授權的數量 |
| AuthZ確定 | 成功的授權數目 |
| AuthZ失敗 | 應用程式層級的MVPD拒絕授權數目 |
| 播放要求 | 產生的簡短媒體權杖數量（與播放要求數量相同） |
| 已要求登出 | 已起始的登出流程數 |
| 登出完成 | 成功完成的登出流程數 |
| 登出失敗 | 失敗的登出流程數目 |
| 已要求預先授權 | 已起始的預先授權流程數 |
| 預先授權確定 | 使用已預先授權的資源的成功預先授權事件數 |
| 預先授權遭拒 | 具有被拒絕預先授權的資源的預先授權事件數 |
| 預先授權失敗 | 失敗的預先授權事件數 |

| Adobe Analytics名稱 | 說明 |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 頻道 | 用來執行軟體權利檔案要求的要求者ID |
| MVPD | 負責將權利授予使用者的MVPD |
| 代理 | Proxy MVPD （對於直接整合而言將是「直接」的） |
| SDK型別 | 使用的使用者端SDK (Flash、HTML5、Android原生、iOS、無使用者端等) |
| SDK版本 | Adobe Primetime驗證使用者端SDK的版本 |
| 資源ID | 授權請求中涉及的實際資源標題（從MRSS裝載擷取，作為專案/標題，如果提供） |
| AuthZ錯誤型別 | 失敗的原因，如Adobe Primetime驗證所報告 <br/> 以下是一些最常見的值 <br/> **noAuthZ** = MVPD回覆使用者在其封裝中沒有管道<br/> **網路** =我們無法連線MVPD （MVPD在通話時發生問題且未回覆）<br/> **norefreshtoken** =這僅適用於OAuth實作，而且如果使用者變更其密碼或MVPD因某項原因而拒絕密碼，則可能會導致此情況。 這通常會導致新的驗證<br/> **不相符** =如果請求來自與具有驗證Token的裝置不同的裝置。 如果使用者嘗試欺騙系統，但大多數此類情況發生在舊版JavaScript SDK的上下文中，其中裝置ID使用IP位址作為計算的一部分，則可能會導致。 如果使用者在家看過TVE，然後在工作中會觸發此錯誤，且必須重新驗證<br/> **無效** =無效的請求，引數遺失或無效<br/>  **authzNone** =程式設計師可以拒絕特定channelxMVPD組合的授權。 這會由程式設計師有權存取的後端API觸發<br/> **詐騙** =這是一種保護機制。 如果使用者未通過授權，然後在短時間間隔（秒）內再次請求授權，我們直接拒絕呼叫。 這通常發生在程式設計師的實作中有錯誤，在失敗時經常要求授權。 |
| 權杖型別 | 當權杖是因AuthZ All和AuthN All而建立時，我們必須知道降級測量所導致的情況。<br/> 包括：<br/> &quot;normal&quot; =正常大小寫<br/> &quot;authnall&quot; =啟用「全部驗證」時<br/> &quot;authzall&quot; =啟用「全部驗證」時<br/>  &quot;hba&quot; =啟用HBA時 |
| 無使用者端裝置型別 | 裝置平台（替代方案），目前用於無使用者端。<br/> 值可以是：<br/> 不適用 — 事件並非源自無使用者端SDK<br/> 未知 — 由於來自 **無使用者端API** 是選用專案，有些呼叫不包含任何值。<br/> 透過傳送的任何其他值 **無使用者端API**. 例如，xbox、appletv和roku。 |
| MVPD使用者ID | 取代Cookie型訪客ID |


## 詳細資料 {#details-int-authn-analyt}

* 量度將透過Adobe Analytics資料插入API以事件/事件方式插入特定報表套裝中
* 插入將批次化，並每30分鐘傳送一次。 因此，報告需要加上時間戳記
* 每位客戶都將有一或多個報表套裝。 一個請求者ID （管道）將只會對應至一個報表套裝。 多個請求者ID只能對應至一個報表套裝。
* 可以提供歷史資料，但由於流量/效能考量，需要特別小心。
* 不重複訪客變數已設為MVPD使用者ID
* 無法設定事件和eVar的對應。


## SLA {#sla-int-authn-serv-anal}

由於這不是關鍵元件，因此整合沒有SLA保證。

## 報表套裝設定 {#report-suite-config}

報表必須有時間戳記，因為事件會以批次傳送。

### 事件 {#report-suite-config-events}


>[!NOTE]
>所有專案都應設定為：
>
>* 計數器（無子關聯）


| 事件 | Adobe Analytics事件 |
|---------------------------------------|-----------------------|
| 已要求AuthN | event1 |
| AuthN擱置中 | event2 |
| 驗證正常 | event3 |
| 已要求AuthZ | event4 |
| AuthZ確定 | event5 |
| AuthZ失敗 | event6 |
| 播放要求 | event7 |
| AuthN失敗 | event8 |
| 無使用者端驗證N權杖請求正常 | event9 |
| 無使用者端驗證權杖請求失敗 | event10 |
| 播放要求失敗 | event11 |
| 登出請求 | event12 |
| 登出完成 | event13 |
| 登出失敗 | event14 |
| 預檢要求 | event15 |
| 預檢失敗 | event16 |
| 已授與預檢 | event17 |
| 預檢遭拒 | event18 |


### eVar {#evars}


>[!NOTE]
>所有專案都應設定為：
>
>* 配置：最近（上一個）
>* 過期時間：點選
>* 型別：文字字串


| 屬性 | eVar |
|-----------------------------------|--------------------------------|
| 頻道 | eVar1 |
| MVPD | eVar2 |
| 代理 | eVar3 |
| SDK型別 | eVar4 |
| SDK版本 | eVar5 |
| 資源ID | eVar6 |
| AuthZ錯誤型別 | eVar7 |
| 權杖型別 | eVar8 |
| 無使用者端裝置型別 | eVar9 |
| MVPD使用者ID | visitorID （自動完成） |
| MVPD使用者ID | eVar10 |
| 裝置型別 | eVar11 |
| 作業系統 | eVar12 |
| 主要硬體型別 | eVar13 |
| TTL | eVar14 |
| 驗證型別 | eVar15 |
| 伺服器架構版本 | eVar16 |
| 外部驗證提供者 | eVar17 |
| 延遲 | eVar18 |
| 訪客Id | eVar19 |
| SSO機制 | eVar20 |
| 裝置型號 | eVar21 |
| 裝置版本 | eVar22 |
| 裝置硬體型號 | eVar23 |
| 裝置硬體廠商 | eVar24 |
| 裝置硬體製造商 | eVar25 |
| 裝置硬體版本 | eVar26 |
| 裝置作業系統名稱 | eVar27 |
| 裝置作業系統系列 | eVar28 |
| 裝置作業系統廠商 | eVar29 |
| 裝置作業系統版本 | eVar30 |
| 裝置瀏覽器名稱 | eVar31 |
| 裝置瀏覽器廠商 | eVar32 |
| 裝置瀏覽器版本 | eVar33 |
| 標準化無使用者端裝置型別 | eVar34 |

## 定價 {#pricing}

如需詳細資訊，請聯絡您的TAM。