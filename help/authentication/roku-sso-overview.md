---
title: Roku SSO概述
description: 關於Roku SSO
exl-id: 77b154bc-c09f-49d4-b1af-cc33bc6dd22b
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Roku SSO概述 {#overview}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 導言 {#roku-sso-intro}

本文檔介紹利用Roku設備上的單點登錄功能所需的資訊。 Adobe Primetime認證與Roku合作，改進登錄用戶體驗，並為電視訂戶跨TV Everywhere應用程式的單一登錄提供便利。

該解決方案基於Adobe Primetime驗證的無客戶端REST API，因此大多數程式設計師無需更新其應用程式即可從單點登錄中獲益。

## 啟用Roku SSO {#enable-roku-sso}

預設情況下啟用Roku SSO，除非程式設計師或MVPD請求禁用SSO。

每個程式設計師都可以在Roku平台上啟用/禁用SSO以進行特定整合。

### 程式設計師應該為Roku SSO做什麼才能工作 {#make-roku-sso-work}

對於程式設計師在客戶端設備上實現REST API的應用程式，Roku SSO將在不進行任何更改的情況下工作。 Roku OS將在任何請求中添加兩個HTTP頭到Adobe Primetime驗證端點。

對於程式設計師的應用程式，實施針對REST api的「伺服器到伺服器」解決方案，程式設計師應聯繫Roku團隊，並詢問配置，在配置中，這兩個標頭將在所有api流中發送到其域。

要使用的Roku提供的用戶ID，而不是應用程式傳遞的任何設備ID，以確保跨應用程式（和跨設備）SSO。

有關所需標題格式的特定詳細資訊，請與Adobe代表聯繫。

### 可能的問題 {#possible-issues}

程式設計師應檢查他們基於Adobe的無客戶端REST API的當前實現是否不會妨礙Roku的平台SSO。 請參見下面的可能問題清單，以及應如何解決這些問題。

|問題 |可能的原因 |可能的解決方案 | |-|-|-| |未將Roku SSO標頭髮送到Adobe|使用HTTP代替HTTPS調用Adobe Primetime身份驗證域|使用HTTPS| 未顯示/未更新SSO令牌的|MVPD徽標|UI依賴於本地儲存|應用程式應在檢查身份驗證後更新UI（和本地儲存，如果需要）| |在沒有AuthZ|應用程式設計|應用程式時觸發的註銷應更新，以便永遠不在後台執行註銷|

## 常見問題 {#faq}

* **SSO將如何工作？**

   SSO將跨所有程式設計師應用程式工作，這些程式設計師應用程式由Adobe Primetime驗證提供支援，並且與同一Roku用戶關聯的所有Roku設備上都使用SSO。
並非所有MVPD都允許Roku SSO。

* **驗證TTL是否有任何更改？**

   第一個有效的身份驗證令牌將用於執行SSO，在這種情況下，將通過SSO進行身份驗證的所有其他應用程式將使用相同的TTL，直到其過期。 因此，當從一個應用程式導航到另一個應用程式時，第二個應用程式將共用驗證的第一個應用程式的TTL。

* **其他Adobe功能是否能像以前一樣工作？**

   所有黃金時段驗證功能將一如既往地正常工作。

* **是否有程式設計師選擇加入/選擇退出流程從Roku平台上的SSO中受益？**

   這將是Adobe的TVE儀表板中的配置更改。 每個程式設計師都可以在Roku平台上啟用/禁用SSO以進行特定整合。
