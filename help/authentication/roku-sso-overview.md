---
title: Roku SSO概觀
description: 關於Roku SSO
exl-id: 77b154bc-c09f-49d4-b1af-cc33bc6dd22b
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Roku SSO概觀 {#overview}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 簡介 {#roku-sso-intro}

本檔案說明在Roku裝置上利用單一登入功能所需的資訊。 Adobe Primetime Authentication與Roku共同作業，改善登入使用者體驗，並促進電視訂閱者在TV Everywhere應用程式上的單一登入。

此解決方案是以Adobe Primetime驗證的Clienless REST API為基礎，因此大多數程式設計師不需要更新其應用程式即可從單一登入中獲益。

## 啟用Roku SSO {#enable-roku-sso}

Roku SSO預設為啟用，除非程式設計師或MVPD要求停用SSO。

每個程式設計師都可以在Roku平台上針對特定整合啟用/停用SSO。

### 程式設計師應該如何做才能讓Roku SSO運作 {#make-roku-sso-work}

對於在使用者端裝置上實作REST API的程式設計師應用程式，Roku SSO將無任何變更即可運作。 Roku OS會對任何傳送至Adobe Primetime驗證端點的請求新增兩個HTTP標頭。

若是程式設計師的應用程式實作適用於REST api的伺服器對伺服器解決方案，程式設計師應聯絡Roku團隊並要求設定以將這兩個標頭傳送至所有api流程上的網域。

使用Roku提供的訂閱者ID，而非應用程式傳遞的任何裝置ID，以確保跨應用程式（和跨裝置） SSO。

如需所需標題格式的特定詳細資訊，請聯絡您的Adobe代表。

### 可能的問題 {#possible-issues}

程式設計師應確認其目前根據Adobe的無客戶端REST API進行的實施不會妨礙Roku的平台 — SSO。 請參閱以下的可能問題清單以及應如何解決這些問題。

|問題 |可能的原因 |可能的解決方案 | |-|-|-| |沒有傳送至Adobe的Roku SSO標頭|對Adobe Primetime驗證網域呼叫使用HTTP而非HTTPS|使用HTTPS| |SSO權杖未顯示/未更新MVPD標誌|UI依賴本機儲存|應用程式應在檢查驗證後更新UI （和本機儲存，如有需要）| |無AuthZ時觸發的登出|應用程式設計應更新為永不於背景執行登出|

## 常見問題集 {#faq}

* **SSO如何運作？**

   SSO將在與同一Roku使用者相關聯的所有Roku裝置上，跨由Adobe Primetime驗證提供支援的所有程式設計人員應用程式運作。
並非所有MVPD都允許Roku SSO。

* **驗證TTL是否有任何變更？**

   第一個有效的驗證Token將用於執行SSO，在此情況下，所有其他將透過SSO驗證的應用程式將使用相同的TTL，直到它過期為止。 因此，從一個應用程式導覽至另一個應用程式時，第二個應用程式會共用第一個驗證之應用程式的TTL。

* **其他Adobe功能會如以前般運作嗎？**

   所有Primetime驗證功能都將像之前一樣運作。

* **Roku平台上的SSO是否會讓程式設計師選擇加入/選擇退出程式受益？**

   這將是AdobeTVE儀表板中的設定變更。 每個程式設計師都可以在Roku平台上針對特定整合啟用/停用SSO。
