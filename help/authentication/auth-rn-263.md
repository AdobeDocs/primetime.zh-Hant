---
title: Adobe Primetime authentication 2.63發行說明
description: Adobe Primetime authentication 2.63發行說明
exl-id: 40987328-6d41-4948-aa4a-bab31f98a18a
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Adobe Primetime Authentication 2.63發行說明 {#pt-authn-263-rn}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

本頁說明此版本的新功能、變更和已知問題：

## 伺服器端和Web使用者端 {#server-side-web-clients-263}

* [建置編號](#build-number)
* [新功能](#new-features)

### 建置編號 {#build-number-263}

Adobe Primetime驗證： adobe-pass-**2.63**
發行日期： **09/20/2022 - 09/22/2022**

### 新功能 {#new-features-263}

#### 改善平台識別機制 {#pf-identification-mech}

* 自此發行版本開始，我們改進了用於識別裝置的機制，不再依賴使用者端實施。 這樣可在平台層級套用商業規則時，提供更準確的詳細程度，並可更清楚瞭解ESM報表中的流量值。

* 隨後將推出新的ESM版本，其中包含公開平台相關欄位的全新及改進報告。

* 如需計畫變更的詳細資訊，請洽詢您的TAM。

#### MVPD自我降級 {#mvpd-self-degradation}

此功能可讓MVPD在流量高的狀況下，當個別端點的負載變得過高時，暫時略過自己的驗證和授權端點。


#### 在授權呼叫的標頭中新增代理的ID {#add-proxied-id}

此功能會在授權呼叫的標頭中新增Synacor代理MVPD的ID。 如此一來，Synacor就能為每個代理的個人(例如 路由至不同的網域（根據代理的MVPD）。


#### TVE儀表板 {#tve-dashboard}

在這個版本中，我們修正了設定報表中未正確計算在MVPD層級設定的authN或authZ TTL的問題。


#### JavaScript SDK 4.6.0 {#js-sdk}

* 已移除的 `eval` 函式，藉此讓SDK符合內容安全性原則。
* 修正合作夥伴應用程式明確清除瀏覽器的本機儲存時，驗證流程無法成功完成的問題。
