---
title: 升級過程
description: 升級過程
exl-id: 1d754e5a-d5fa-4411-8932-2a36294da6eb
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---

# 升級過程 {#escalation-procedures}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

>[!IMPORTANT]
> 
>撥打熱線： **+1-205-693-9813** 併發送電子郵件至 **tve-support@adobe.com** 包括 **緊急 — 事件** 的下界。

## 導言 {#introduction}

本文檔介紹了針對主要事件(**嚴重性1** 影響Adobe Primetime認證、Mogine Concurrency Monitoring及其合作夥伴。\
 

## 嚴重性為1級事件的定義 {#definition-of-a-severity-1-level-incident}

A **嚴重性1** 級別事件是 **活動** 情況， **在生產環境中發生**，這不允許完成一個通道和一個MVPD的驗證和/或授權流，從而影響執行該流的MVPD的大量訂戶。


## 嚴重性為1的事件示例 {#examples-of-severity-1-incidentcs}

* 托管在以下位置的生產Access Enabler  `https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js` 或 `https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js`)不可用。

* 對於特定MVPD，在用戶選擇MVPD（在任何受支援的瀏覽器中）後，Adobe不再重定向/顯示登錄頁。

* 合作夥伴收到大量報告，用戶無法通過特定MVPD進行身份驗證/授權。

* 在驗證過程中，用戶被困在Adobe錯誤頁上，而不可能重新啟動驗證/授權流。


| 示例 **不** 嚴重性為1的事件 |
|---|
| 對於此類問題，Adobe將為調查提供支援，但不是嚴重級別為1的事件：<ul><li>由於Flash版本問題(缺少Flash、Flash阻止程式、Flash版本錯誤)，一個或多個訂閱者無法執行流。</li><li>一個或幾個訂戶無法驗證並保留在MVPD登錄頁上。</li><li>一個或幾個訂戶被驗證但無法播放視頻。</li><li>在程式設計師站點上，一個/幾個/所有訂閱者遇到JavaScript錯誤</li></ul> |

## 嚴重性1升級流 {#severity-1-escalation-flows}

嚴重級別為1的事件可能由Adobe或Adobe Primetime身份驗證合作夥伴啟動。 每個步驟的步驟如下。

### 合作夥伴啟動的流 {#partner-initiated-flow}

1. 合作夥伴確定嚴重性為1的事件（如上所述），需要Adobe立即注意。
1. 合作夥伴向 **tve-support@adobe.com** 包括 **緊急 — 事件** 添加以下資訊：
   * 標題
   * 要再現的說明和步驟
   * 作業系統/瀏覽器
   * SDK和版本
   * 受影響的設備
   * 受影響的用戶數
   * HTTP跟蹤或設備日誌演示此問題
   * （可選）任何顯示問題的可用螢幕截圖或視頻捕獲
1. 如果Adobe在30分鐘內未響應票證，則合作夥伴將調用以下號碼：
   **1-205-693-9813**

   >[!IMPORTANT]
   >如果您未在票證標題中包括「URGENT-INCIDENT」，則我們的通知系統將不會收到該通知**。

### Adobe啟動的流 {#adobe-initiated-flow}

#### ...Adobe Primetime驗證問題 {#adobe-initiated-flow-authn-issue}

1. Adobe識別內部問題並使用我們的跟蹤系統開啟票證。

1. Adobe通知合作夥伴的計畫經理和技術聯繫人，指定票證編號和問題的估計影響。

1. Adobe致力於解決該事件，並隨時向所有受影響的合作夥伴通報情況。

#### ...合作夥伴問題（程式設計師/MVPD） {#adobe-initiated-flow-partner-issue}

1. Adobe標識與MVPD或某個程式設計師站點的整合相關的問題。

1. Adobe通知受影響的合作夥伴 <u>遵循與該合作夥伴一起實施的支援程式</u> 並與合作夥伴的支援組織開啟票證。

1. 如果在影響分析期間，Adobe發現該問題屬於事件情景的預先商定決定之一，請參閱 **事件情景的預先商定決定**&#x200B;這樣，它就會相應地行動，而不等待合作夥伴的投入。

1. Adobe將等待合作夥伴的更新以及服務恢復後合作夥伴的通知。

## 事件情景的預先商定決定 {#pre-agreed-descn}

在某些情況下，在出現該方案時將執行預設操作：

|  | 方案 | 說明 | 操作 |
|---|---|---|---|
| S1 | Adobe在正常生產操作期間識別MVPD整合的問題。 | 在正常生產操作期間，Adobe會發現MVPD中的一個問題，這使得無法執行身份驗證/授權流（例如，過期的證書、過期的SAML響應、埠關閉、更改的參數等） | -Adobe將通知受影響的MVPD和程式設計師。  </br> </br> -Adobe將為所有受影響的程式設計師停用此MVPD。 </br> </br> -Adobe將根據與MVPD的協定支援過程與MVPD開啟票證 |
| S2 | Adobe為程式設計師激活新的MVPD，程式設計師允許在啟動日期之前使用MVPD。 | Adobe正在為程式設計師站點激活新MVPD，並且該站點已在機械臂中顯示新MVPD，即使不應該。 | -Adobe將在計畫日期之前通知程式設計師在選取器中顯示的新MVPD。 </br> </br>   — 如有必要，程式設計師將從機械臂中刪除它。 |
| S3 | Adobe為程式設計師激活新MVPD，即使MVPD未準備好投入生產 | Adobe正在為程式設計師激活新MVPD，但MVPD尚未部署對整合的支援，因此無法執行身份驗證/授權流 |  — 只有在程式設計師提出要求時，Adobe才會執行部署 </br> </br>  — 程式設計師將負責確保在執行所有test後獲得MVPD許可。 |

## 嚴重級別為1的事件的響應預期 {#response-expectations-for-severity-one-incidents}

* 初始響應：30分鐘（24/7張）
* 行動計畫：1小時(24/7)
* 解決方案：盡快(24/7)
