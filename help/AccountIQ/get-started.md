---
title: 帳戶IQ開始使用帳戶IQ、先決條件和開始
description: '如何板載、必備項和開始使用帳戶IQ。 '
source-git-commit: 258ce10297aa15086a3ed1c1a825af2a30d34d24
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 如何開始使用帳戶IQ {#onboarding}

閱讀以瞭解使用帳戶智商的先決條件，以及您的公司如何開始查看共用大量訂閱者的帳戶。

## 先決條件 {#prerequisites}

* 組織必須在 [!DNL Adobe Marketing Cloud] 組織。

* 該組織中的用戶應分配給TVE儀表板讀寫或TVE儀表板只讀。

### 瀏覽器先決條件 {#browser-prerequisites}

帳戶IQ是托管Web服務。 它與以下瀏覽器的最新版本相容：

* Google鉻
* Mozilla Firefox
* Safari版本

### 如何將組織安裝在帳戶IQ上？ {#steps-to-onboard}


這就是我們目前的情況。 計畫是取消dma_mighine檢查，並為AIQ提供專用配置檔案。 需要訪問控制台的用戶需要該用戶配置檔案。 但目前尚未落實。

1. 讓他們的組織在Adobe Marketing Cloud@Eric或@Peter，你能接受這個。  我想它現在叫做&quot;Experience Cloud&quot;，但那是次要的。  有更多細節嗎？ 這是否由其他組管理？ 如果是，我們是否提供連結、聯繫人等？ 此外，還應附上一個警告，說明檢查其組織是否已屬於Experience Cloud。

2. 將「 TVE Dashboard Read-Write 」或「 TVE Dashboard Read Only 」配置檔案分配給其用戶，位於http://adminconsole.adobe.com/。
@Eric，你知道怎麼做嗎？  是否有子步驟？  我們能否向客戶解釋他們為什麼選擇「讀寫」與「只讀」？
@Cristina，您能簡單地解釋一下，這是一種臨時的方法，也許它在下一個版本中將如何工作？

3. 在AIQ端@Cristina上列出其組織ID ，我們是否可以建立一個流程來管理此問題？  例如，使用組織的組織ID等向「DL-AdobePass-Eng AdobePass-Eng@adobe.com」發送電子郵件。

<!-- these user groups set dma_primetime product context for the user accounts. In AIQ code we’re checking for this product context when providing access. Internally, in the code we have an additional condition: the org id should be whitelisted in order for the users to get access to their data. -->

訪問Adobe企業控制面板時，您將在Adobe Marketing Cloud組織中看到兩個新建立的用戶組：

TVE Dashboard讀寫 — 此組的成員在儀表板的所有可編輯部分具有完全權限TVE Dashboard只讀 — 此組的成員只有整個儀表板的查看權限請將帳戶添加到TVE Dashboard讀寫用戶組、Adobe企業儀表板，然後登錄Adobe PrimetimeTVE Dashboard。  之後，您將能夠通過添加和刪除上述兩個用戶組中的用戶，在Adobe企業儀表板中管理用戶權限。

...........

在您提供的文檔中，有一部分稱為「黃金時段TVE儀表板用戶設定入門」，該部分適用於Adobe Pass控制台，但AIQ也應類似。
http://tve.helpdocsonline.com/primetime-tve-dashboard-user-guide對AIQ感興趣的組織應是在Adobe Marketing Cloud組織註冊的組織。 該組織中的用戶應分配給TVE儀表板讀寫或TVE儀表板只讀。
僅針對您的知識，這些用戶組將為用戶帳戶設定dma_mighide產品上下文。 在AIQ代碼中，我們在提供訪問時正在檢查此產品上下文。 在內部，代碼中還有一個附加條件：應將組織ID白列，以便用戶訪問其資料。
這就是我們目前的情況。 計畫是取消dma_mighine檢查，並為AIQ提供專用配置檔案。 需要訪問控制台的用戶需要該用戶配置檔案。 但目前尚未落實。

..........................

1. 讓他們的組織在Adobe Marketing Cloud
2. 將「 TVE Dashboard Read-Write 」或「 TVE Dashboard Read Only 」配置檔案分配給其用戶，位於http://adminconsole.adobe.com/。
3. 在AIQ端將其組織ID白列
