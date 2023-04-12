---
title: Adobe Primetime authentication 2.63發行說明
description: Adobe Primetime authentication 2.63發行說明
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Adobe Primetime Authentication 2.63發行說明 {#pt-authn-263-rn}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

本頁面說明此版本的新功能、變更和已知問題：

## 伺服器端和Web用戶端 {#server-side-web-clients-263}

* [建置編號](#build-number)
* [新功能](#new-features)

### 建置編號 {#build-number-263}

Adobe Primetime驗證：adobe-pass-**2.63**
發行日期： **09/20/2022 - 09/22/2022**

### 新功能 {#new-features-263}

#### 改進平台識別機制 {#pf-identification-mech}

* 自此版本開始，我們改善了用於識別裝置的機制，且不再依賴用戶端實作。 這樣，在平台層級應用業務規則時，可提供更準確的粒度，並更好地了解ESM報告中的流量值。

* 隨後將發佈新的ESM版本，新的和改進的報告將公開平台相關欄位。

* 欲知有關計畫更改的詳細資訊，請聯繫您的TAM。

#### MVPD自退化 {#mvpd-self-degradation}

此功能可讓MVPD在這些端點的負載過高時，暫時略過其本身的驗證和授權端點，以應對高流量情況。


#### 在授權呼叫的標題中新增代理ID {#add-proxied-id}

此功能會在授權呼叫的標題中新增Syncor代碼MVPD的ID。 這使Synacor能夠為每個單獨代理設定業務規則(例如 每個代理的MVPD路由至不同網域)。


#### TVE儀表板 {#tve-dashboard}

在此版本中，我們修正了在MVPD層級設定的authN或authZ TTL未在設定報表中正確計算的問題。


#### JavaScript SDK 4.6.0 {#js-sdk}

* 移除 `eval` 功能，使SDK符合內容安全性原則。
* 修正當合作夥伴應用程式明確清除瀏覽器的本機儲存時，驗證流程無法成功完成的問題。



