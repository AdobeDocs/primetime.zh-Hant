---
title: Roku SSO概觀
description: 關於Roku SSO
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---


# Roku SSO概述 {#overview}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 簡介 {#roku-sso-intro}

本檔案說明在Roku裝置上運用單一登入功能所需的資訊。 Adobe Primetime驗證與Roku協作，以改善登入使用者體驗，並為電視訂閱者提供跨TV Everywhere應用程式的單一登入便利。

此解決方案以Adobe Primetime驗證的無客戶端REST API為基礎，因此大多數程式設計師無需更新其應用程式即可從單一登錄中受益。

## 啟用Roku SSO {#enable-roku-sso}

預設情況下，Roku SSO為啟用，除非程式設計師或MVPD請求禁用SSO。

每個程式設計師都可在Roku平台上啟用/停用SSO，以進行特定整合。

### 程式設計師應如何使Roku SSO工作 {#make-roku-sso-work}

對於在用戶端裝置上實作REST API的程式設計人員應用程式，Roku SSO將可正常運作，且不會有任何變更。 Roku OS會針對任何向Adobe Primetime驗證端點的要求新增兩個HTTP標題。

對於程式設計師的應用程式為REST api實施伺服器到伺服器解決方案，程式設計師應與Roku團隊聯繫，並要求提供一個配置，在該配置中，所有api流都將將這兩個標頭髮送到其域。

Roku提供的訂閱者ID，將用來取代應用程式所傳遞的任何裝置ID，以確保跨應用程式（和跨裝置）SSO。

如需所需標題格式的詳細資訊，請連絡您的Adobe代表。

### 可能的問題 {#possible-issues}

程式設計人員應檢查根據Adobe無用戶端REST API的目前實作是否不會阻礙Roku的平台SSO。 請參閱下方的可能問題清單，以及應如何解決這些問題。

|問題 |可能的原因 |可能的解決方案 | |-|-|-| |未將Roku SSO標頭傳送至Adobe|對Adobe Primetime驗證網域進行呼叫時，請使用HTTP而非HTTPS|使用HTTPS| |未針對SSO權杖顯示/未更新MVPD標誌|UI依賴本機儲存|應用程式應在檢查驗證後更新UI（若有需要）| |未在AuthZ時觸發註銷|應用程式設計|應更新應用程式，從不在後台執行註銷|

## 常見問題集 {#faq}

* **SSO如何運作？**

   SSO將可在與同一Roku用戶關聯的所有Roku設備上，使用Adobe Primetime身份驗證的所有程式設計師應用程式中工作。
並非所有MVPD都允許Roku SSO。

* **驗證TTL是否會有任何變更？**

   第一個有效的驗證Token將用於執行SSO，在此情況下，所有將透過SSO驗證的其他應用程式將使用相同的TTL，直到過期為止。 因此，在從一個應用程式導覽至另一個應用程式時，第二個應用程式會共用驗證之第一個應用程式的TTL。

* **其他Adobe功能是否如以往般運作？**

   所有Primetime驗證功能都如舊。

* **Roku平台上是否有程式設計師選擇加入/選擇退出程式受益於SSO?**

   這將是AdobeTVE儀表板中的配置更改。 每個程式設計師都可在Roku平台上啟用/停用SSO，以進行特定整合。
