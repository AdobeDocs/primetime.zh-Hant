---
title: 呈報程式
description: 呈報程式
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---

# 呈報程式 {#escalation-procedures}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

>[!IMPORTANT]
> 
>致電熱線： **+1-205-693-9813** 並傳送電子郵件至 **tve-support@adobe.com** 包括 **緊急 — 事件** 在主旨行。

## 簡介 {#introduction}

本文檔介紹了重大事件(**嚴重性1** 層級)影響Adobe Primetime驗證、Primetime並行監控及其合作夥伴。\
 

## SEVERITY 1級事件的定義 {#definition-of-a-severity-1-level-incident}

A **嚴重性1** 級別事件是 **LIVE** 情況， **在生產環境中發生**，則不會允許完成一個通道和一個MVPD的驗證和/或授權流程，而影響執行該流程之MVPD的大量訂閱者。


## 嚴重性為1的事件示例 {#examples-of-severity-1-incidentcs}

* 托管於的生產Access Enabler  `https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js` (或 `https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js`)無法使用。

* 針對特定MVPD，使用者選取MVPD後（在任何支援的瀏覽器中）,Adobe不再重新導向/顯示登入頁面。

* 合作夥伴會收到大量報表，指出使用者無法透過特定MVPD進行驗證/授權。

* 在驗證過程中，用戶被卡在Adobe錯誤頁上，不可能重新啟動驗證/授權流程。


| 範例為 **NOT** a嚴重性1事件 |
|---|
| 對於這些類型的問題，Adobe將提供調查支援，但不是嚴重性為1的事件：<ul><li>由於Flash版本問題(缺少Flash、Flash封鎖程式、錯誤的Flash版本)，一個或幾個訂閱者無法執行流量。</li><li>一個或幾個訂閱者無法驗證MVPD登入頁面並保留在該頁面上。</li><li>一個或幾個訂閱者已驗證，但無法播放視訊。</li><li>在程式設計師站點上，一/少/所有訂閱者遇到JavaScript錯誤</li></ul> |

## 嚴重性1升級流 {#severity-1-escalation-flows}

嚴重性為1的事件可由Adobe或Adobe Primetime驗證合作夥伴發起。 各步驟如下。

### 合作夥伴啟動的流 {#partner-initiated-flow}

1. 合作夥伴確定了嚴重性為1的事件（如上所述），需要Adobe立即注意。
1. 合作夥伴會傳送電子郵件至 **tve-support@adobe.com** 包括 **緊急 — 事件** 並新增下列資訊：
   * 標題
   * 重制說明和步驟
   * 作業系統/瀏覽器
   * SDK與版本
   * 受影響的裝置
   * 受影響的使用者百分比
   * 說明問題的HTTP追蹤或裝置記錄
   * （選用）任何展示問題的可用螢幕擷取畫面或影片擷取畫面
1. 如果Adobe在30分鐘內未回應票證，則合作夥伴會呼叫以下號碼：
   **1-205-693-9813**

   >[!IMPORTANT]
   >如果您未在票證標題中加入「URGENT-INCIDENT」，我們的通知系統將不會擷取該票證**。

### Adobe啟動流 {#adobe-initiated-flow}

#### ...Adobe Primetime驗證問題 {#adobe-initiated-flow-authn-issue}

1. Adobe可識別內部問題，並使用我們的追蹤系統開啟票證。

1. Adobe通知合作夥伴的計畫經理和技術聯繫人，指定票證編號和問題預計的影響。

1. Adobe致力於解決該事件，並隨時向所有受影響的合作夥伴通報情況。

#### ...（程式設計人員/MVPD） {#adobe-initiated-flow-partner-issue}

1. Adobe識別與MVPD或程式設計人員網站之一的整合相關的問題。

1. Adobe通知受影響的合作夥伴 <u>執行與該合作夥伴建立的支援程式</u> 並與合作夥伴的支援組織開啟票證。

1. 在影響分析期間，如果Adobe確定問題屬於事件情景的預先商定決定之一，請參閱 **事件情景的預先商定決定**，它會採取相應行動，而不等待合作夥伴的投入。

1. Adobe將等待合作夥伴的更新，並在服務還原後收到合作夥伴的通知。

## 事件情景的預先商定決定 {#pre-agreed-descn}

在某些情況下，若發生該情境，則會執行預設動作：

|  | 藍本 | 說明 | 動作 |
|---|---|---|---|
| S1 | Adobe可識別正常生產作業期間MVPD整合的問題。 | 在正常生產操作期間，Adobe識別一個MVPD的問題，這使得驗證/授權流的執行不可能（例如，過期的證書、過期的SAML響應、埠關閉、更改的參數等） | -Adobe會通知受影響的MVPD和程式設計人員。  </br> </br> -Adobe會為所有受影響的程式設計人員停用此MVPD。 </br> </br> -Adobe會依照與MVPD商定的支援程式，與MVPD開啟票證 |
| S2 | Adobe為程式設計師激活新的MVPD，程式設計師在啟動日期之前允許MVPD。 | Adobe正在為程式設計人員的站點激活新的MVPD，而站點已在選擇器中顯示新的MVPD，即使它本不應該顯示。 | -Adobe會在計畫日期之前通知程式設計師新的MVPD出現在選擇器中。 </br> </br>   — 程式設計師將採取操作，在必要時從選擇器中刪除它。 |
| S3 | Adobe會為程式設計師啟用新的MVPD，即使MVPD尚未準備好投入生產 | Adobe正在為程式設計師激活新的MVPD，但MVPD尚未部署對整合的支援，因此無法執行驗證/授權流 |  — 只有在程式設計師提出要求時，Adobe才執行部署 </br> </br>  — 程式設計師將負責確保所有測試都執行完畢後MVPD的許可。 |

## 嚴重性為1的事件的響應預期 {#response-expectations-for-severity-one-incidents}

* 初始響應：30分(24/7)
* 行動計畫：1小時(24/7)
* 解決方法：盡快(24/7)
