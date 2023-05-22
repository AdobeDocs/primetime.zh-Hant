---
title: Adobe Primetime身份驗證2.63發行說明
description: Adobe Primetime身份驗證2.63發行說明
exl-id: 40987328-6d41-4948-aa4a-bab31f98a18a
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Adobe Primetime身份驗證2.63發行說明 {#pt-authn-263-rn}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

本頁介紹此版本的新功能、更改和已知問題：

## 伺服器端和Web客戶端 {#server-side-web-clients-263}

* [內部版本號](#build-number)
* [新功能](#new-features)

### 內部版本號 {#build-number-263}

Adobe Primetime驗證：adobe-pass-**二塊六毛三**
發佈日期： **09/20/2022 - 09/22/2022**

### 新功能 {#new-features-263}

#### 改進平台識別機制 {#pf-identification-mech}

* 從此版本開始，我們改進了用於識別設備的機制，不再依賴於客戶端實現。 這將在平台級別應用業務規則時提供更準確的粒度，並更好地瞭解ESM報告中的通信量值。

* 很快，新的ESM發佈將陸續發佈，新的和改進的報告將公佈平台相關領域。

* 有關計畫更改的詳細資訊，請聯繫您的TAM。

#### MVPD自退化 {#mvpd-self-degradation}

此功能使MVPD能夠在各個端點上的負載過高時臨時繞過它們自己的身份驗證和授權端點，以應對高流量情況。


#### 在授權調用的標頭中添加代理ID {#add-proxied-id}

此功能將在授權調用的標頭中添加Synacor代理的MVPD的ID。 這使Synacor能夠為每個代理設定業務規則(例如 按代理MVPD路由到不同域)。


#### TVE儀表板 {#tve-dashboard}

在此版本中，我們解決了在配置報告中未正確計算MVPD級別的authN或authZ TTL集的問題。


#### JavaScript SDK 4.6.0 {#js-sdk}

* 已刪除 `eval` 使SDK與內容安全策略相容。
* 修復了在合作夥伴應用程式明確清除瀏覽器的本地儲存時阻止身份驗證流成功完成的問題。
