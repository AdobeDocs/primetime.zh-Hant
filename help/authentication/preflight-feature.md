---
title: 預檢功能、如何啟用、疑難排解或判斷問題
description: 預檢功能、如何啟用、疑難排解或判斷問題
exl-id: 9e4ec343-371f-4116-915f-191e5f42cb47
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---

# 預檢功能：如何啟用、疑難排解或判斷問題 {#preflight-feature}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

Adobe Primetime驗證計算preAuthorizeResources的方式已變更。 PreAuthorization API有新的實作。 此實作會取代僅進行多個授權呼叫的舊解決方案。
PreAuthorization API的外部介面未變更，程式設計師的應用程式中不需要更新。

預檢資源的計算方式有三種：

* **MVPD的分叉及連線方法**：這涉及Adobe對MVPD進行多次授權呼叫（使用者端仍須進行一個預檢呼叫）。
* **管道排列**： MVPD會在SAML驗證回應中公開登入使用者的頻道行，且Adobe會根據該來源傳回授權資源。 SAML追蹤器中的SAML authN回應應該會公開該清單。
* **多頻道授權**：使用者端和Adobe驗證作業都會針對一組資源對MVPD發出單一呼叫。

不論MVPD為何，使用者端應用程式都會對Preflight端點(checkPreauthorizedResources API)進行單一呼叫，並傳遞一組resourceID。 根據MVPD支援的上述方法之一，Adobe會傳回預先授權的resourceID。

如果Preflight是以fork &amp; join方法為基礎，則Adobe Primetime Authentication後端會檢查其設定中為「最大預先授權呼叫」設定的值。 這是由Adobe設定。

&#39;max preauthorization calls&#39;設定的預設值為&#39;5&#39;，這表示在分叉並加入MVPD的Preflight中最多只能傳送5個資源。 傳遞超過5個資源會產生例外狀況，並會傳回null清單。 這是預期行為。 如果MVPD不支援管道排列或多管道授權，我們可以將此設定為任何值，但必須諮詢他們是否為多個取用和加入授權呼叫會增加其載入時間。

因此，在啟用/疑難排解MVPD的印前檢查時，需要注意以下幾點：

* MVPD支援的方法（分叉和聯結、頻道排列或多頻道）。
* 如果只支援分支並加入，則需要詢問程式設計師將在Preflight呼叫中傳送多少資源ID。
* 需要諮詢MVPD，並需要瞭解發出「n」個分叉與加入授權呼叫的影響。 之後，如果值大於5，則必須在config中設定值。

**限制**

請注意，對於某些MVPD （例如AT&amp;T和TWC），如果任何resourceID是假的ID，或是在預檢呼叫中傳送的resourceID清單中無法辨識的ID，我們並不會從預檢呼叫中取得任何resourceID，即使我們在該清單中也有有效且已授權的資源。
