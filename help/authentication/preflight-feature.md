---
title: 印前檢查功能、如何啟用、故障排除或確定問題
description: 印前檢查功能、如何啟用、故障排除或確定問題
exl-id: 9e4ec343-371f-4116-915f-191e5f42cb47
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---

# 印前檢查功能：如何啟用、排除故障或確定問題 {#preflight-feature}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

Adobe Primetime身份驗證計算preAuthorizeResources的方式已發生更改。 PreAuthorization API有一個新的實現。 此實現取代了僅進行多個授權調用的舊解決方案。
預授權API的外部介面未更改，程式設計師應用程式中不需要更新。

計算印前檢查資源的方法有三種：

* **MVPD的分叉和連接方法**:這涉及Adobe對MVPD進行多個授權調用（儘管客戶端仍必須進行一個印前檢查呼叫）。
* **通道排列**:MVPD在SAML驗證響應中顯示登錄用戶的通道行，並且Adobe根據此返回授權資源。 SAML跟蹤器中的SAML authN響應應公開該清單。
* **多通道授權**:客戶端和Adobe驗證都對一組資源進行一次MVPD調用。

無論使用什麼MVPD，客戶端應用程式都將對印前檢查終結點(checkPreauthorizedResources API)進行一次調用，並傳遞一組resourceID。 根據MVPD支援的上述方法之一，Adobe將返回預授權的resourceID。

如果預檢基於fork &amp; join方法，則Adobe Primetime身份驗證後端將檢查其配置中「最大預授權調用」的值集。 這由Adobe配置。

「max preauthorization calls」配置的預設值為「5」，這意味著在Preflith中，fork &amp; join MVPD最多只能發送5個資源。 傳遞5個以上資源將導致異常，並返回空清單。 這是預期行為。 如果MVPD不支援通道配置或多通道授權，但只有在將它們作為多個分叉和加入授權呼叫咨詢後，它們的載入時間才會增加，則我們可以將其配置為任何值。

因此，在啟用/排除MVPD的印前檢查時，需要考慮以下事項：

* MVPD支援的方法（分叉和連接、通道線路或多通道）。
* 如果只支援fork &amp; join ，則需要詢問程式設計師將在印前檢查呼叫中發送多少個resourceID。
* 需要咨詢MVPD，並需要瞭解進行「n」個分叉和聯接授權調用的影響。 之後，如果值大於5，則必須在配置中配置該值。

**限制**

請注意，如果資源ID中的任何一個是虛假ID，或它們在預檢呼叫中發送的資源ID清單中的無法識別的ID，則我們不會從預檢呼叫中返回某些MVPD（如AT&amp;T和TWC）的任何資源ID，即使我們在該清單中也具有有效的和授權資源。
