---
title: 預檢功能、如何啟用、疑難排解或判斷問題
description: 預檢功能、如何啟用、疑難排解或判斷問題
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---


# 預檢功能：如何啟用、疑難排解或判斷問題 {#preflight-feature}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

Adobe Primetime驗證計算preAuthorizeResources的方式已有所變更。 PreAuthorization API有新的實作。 此實作會取代舊版解決方案，此舊版解決方案僅包含進行多個授權呼叫。
預授權API的外部介面未更改，程式設計師應用程式中不需要更新。

計算預檢資源的方法有三種：

* **MVPD的分叉與連接方法**:這包括Adobe對MVPD進行多個授權呼叫（不過用戶端仍須進行一個預檢呼叫）。
* **管道排列**:MVPD會在SAML驗證回應中向登入使用者顯示通道行，而Adobe會據此傳回授權資源。 SAML追蹤器中的SAML authN回應應會公開該清單。
* **多通道授權**:用戶端與Adobe驗證會針對一組資源對MVPD進行單一呼叫。

無論MVPD為何，用戶端應用程式都會對預檢端點(checkPreauthorizedResources API)進行單一呼叫，並傳遞一組resourceID。 根據MVPD支援的上述其中一種方式，Adobe會傳回預先授權的resourceID。

如果Preflight是以分叉與連接方法為基礎，Adobe Primetime驗證後端會檢查其設定中為「最大預授權呼叫」所設定的值。 這是由Adobe設定。

「最大預授權呼叫數」設定的預設值為「5」，這表示在Preflight中，最多只能傳送5個資源，以用於分支與加入MVPD。 傳遞超過5個資源會導致例外，並傳回null清單。 這是預期的行為。 如果MVPD不支援通道陣列或多通道授權，但只有在諮詢它們為多個分支和加入授權呼叫後，它們的載入時間才會增加，我們才能將此設定為任何值。

因此，在啟用/疑難排解MVPD的預檢時，請注意下列事項：

* MVPD支援的方法（分支與連接、通道線上或多通道）。
* 如果僅支援分支和加入，則程式設計師需要詢問它在預檢呼叫中將發送多少resourceID。
* 需要咨詢MVPD，並需要了解發出「n」個分支和加入授權呼叫的影響。 之後，如果值大於5，則必須以設定進行設定。

**限制**

請注意，如果資源ID中的任何一個是假ID或其在預檢呼叫中傳送之resourceID清單中的無法識別ID，即使該清單中也包含有效和授權的資源，我們不會從預檢呼叫中傳回某些MVPD（例如AT&amp;T和TWC）的任何resourceID。

