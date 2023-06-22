---
title: 帳戶IQ字彙表
description: 產品術語辭彙表。
exl-id: 2ee54442-9538-4c30-b999-265310b3935f
source-git-commit: 4eb5ba53fb3e0a0c314695fcd30cf15c7242b53c
workflow-type: tm+mt
source-wordcount: '1456'
ht-degree: 0%

---

# 產品概念和字彙表 {#glossary}

請參閱下列產品術語及其定義。

## 帳戶共用機率 {#account-sharing-probability-def}

具有圖表的儀表板面板，可將目前共用分數的區段劃分為非常低、低、中、高和非常高的共用範圍類別。

## 動作 {#action-def}

與「 」相關聯的直接或間接事件 [作業](#operation-def) 這會影響相關作業區段（或同類群組）的特性（例如共用分數或使用中的裝置數）。

## 彙總的共用分數 {#sharing-probability-level-def}

控制面板面板，內含圖表，可將目前共用分數的區段分成非常低、低、中等、高和非常高的共用範圍類別，以及區段串流總量的每個類別百分比。

## AuthN {#authn-def}

驗證，或驗證嘗試次數。 驗證嘗試是指將目前沒有有效驗證狀態的使用者重新導向至他們選擇的MVPD的程式，在那裡，他們向MVPD識別自己 — 通常使用使用者名稱和密碼。

## 驗證正常 {#authn-ok-def}

成功驗證的次數。 當MVPD確認使用者身分識別，並導致將使用者重新導向回程式設計人員應用程式或網站時，就會發生成功的驗證。

## AuthZ {#authz-def}

授權，或授權要求的數目。 授權請求是程式設計師透過Adobe向MVPD請求許可權以開始串流使用者請求內容的程式。 MVPD通常會根據與使用者的MVPD訂閱相關聯的內容許可權（例如與內容相關聯的頻道是否位於使用者的訂閱中）來授與要求。 Adobe會快取部分授權要求回應，讓Adobe能夠立即回應，而不會將要求傳遞至MVPD。

## AuthZ確定 {#authz-ok-def}

成功的授權數目。

## 頻道 {#channel-def}

Channel （也稱為Property）是視訊內容的主題相關來源。 傳統上，代表MVPD提供的不同、數字可定址連續視訊摘要。 此頻道直接對應到訂閱者透過其機上盒(STB)可用的可存取內容頻道。

## 叢集 {#cluster-def}

叢集是位置和裝置的集合。 叢集是透過尋找裝置之間的共同位置來建立。 在共同位置看到的裝置會視為屬於相同叢集。 兩個裝置可以在同一個叢集中，即使它們沒有共同的位置，但可以透過其他裝置的位置連線。

### 行動叢集 {#mobile-cluster-def}

沒有靜態裝置的叢集。

### 靜態叢集 {#static-cluster-def}

至少有一個靜態裝置的叢集。

## 並行 {#consurrency-def}

並行是由同時播放或時間非常接近的兩個（或多個）串流所定義，因此它們之間的間隔無法透過以正常速度旅行來對齊。
同時使用率是使用2個不同叢集之間的最大速度（英里/小時）來計算。 如果使用者在距離小於124哩時具有大於124米/小時的速度，或在距離大於124哩時具有大於400米/小時的速度，則被視為同時使用。 會計算來自不同叢集的位置之間的距離。 相同叢集中允許同時使用。

## 裝置 {#device-def}

一種數位視訊硬體產品，可播放Adobe Pass支援的TV Everywhere內容。 例如，智慧型手機、筆記型電腦和桌上型電腦、遊戲機，以及智慧型電視。

## 地理範圍 {#geographical-span-def}

一組位置中最遠點之間的距離。

## 詳細程度 {#granularity-def}

參照時間範圍，期間的大小；例如一週或一個月。

## 產業平均指數 {#industry-avg-index-def}

在選取的時間範圍內，針對所有程式設計師和MVPD的每個「風險指數」（帳戶、使用狀況、整體）計算的值。

## IP {#ip-def}

網際網路服務提供者指派給裝置的網際網路通訊協定位址。 例如，纜線服務供應商和儲存格服務供應商。

## 隔離模式 {#isolation-mode-def}

一種共用分析型別，帳戶評估僅限於在所選區段中直接發生在程式設計師的事件。  一般而言，會評估所有帳戶事件，而這會提供更準確的共用預估值。  某些MVPD資料的結構方式僅允許隔離模式分析。

## 位置 {#location-def}

地球上獨一無二的地方。 也稱為特定播放要求的地理位置，使用Pass資料偵測到，精確度為1000mx1000m （1平方公里）。

<!-- ### Home location {#home-location-def}

the precision is 0.01 ~ 2000mx2000m (4 square km) - at this moment the home location is detected using an ML algo, based on data provided by two mvpds. The probability is ~ 80%. We are not using the zip code for the majority of the users. Currently, this information is not used in assessing the sharing probability. -->

## 媒體公司 {#media-company-def}

Media Company是擁有一組媒體網路的公司。

## 量度 {#metric}

量度是訂閱者帳戶的屬性（例如，訂閱者的MVPD、程式設計師和串流內容的頻道、使用的裝置數）。

## 行動裝置 {#mobile-device-def}

具有高行動性的裝置。 例如，行動電話和平板電腦。

## MVPD {#mvpd-def}

MVPD （也稱為Distributor）是Media Company視訊內容的彙總、經銷商和經銷商。

## 作業 {#operation-def}

Operation是為追蹤特定效果而建立的記錄 [動作](#action-def) 於相關區段上。 動作的範例可以是對節段所識別之科目所允許的並行資料流數量進行限制。

## 整體共用分數 {#overall-sharing-score}

一個值，可協助使用者瞭解程式設計人員屬性或MVPD訂閱者共用密碼的程度，並讓他們有緊迫感採取相應的行動。

<!--**Aggregated Risk Index**
Also known as Risk Index and Sharing Risk Index, it is a value that helps users understand the magnitude of password sharing on Programmer properties or by MVPD subscribers and provides them a sense of urgency to act upon it.-->

<!--**Risk Index - Overall**
A value computed as an average of "Risk Index - Accounts" and the "Risk Index - Usage". Overall Sharing Risk Index-->

## 播放要求 {#play-requests-def}

使用者端應用程式或網站Adobe提出的要求，用於要求媒體權杖來記錄和保護資料流開始。

## 程式設計師 {#programmer-def}

Programmer （也稱為Network）是擁有和管理一個或多個管道的大型公司（公司）的子公司。

## 請求者ID {#requestorid-def}

媒體公司用來識別自己或MVPD子公司的識別碼。  根據程式設計人員實施，這可能對應到媒體公司、程式設計人員或頻道。  媒體公司最常用來識別自己或MVPD子公司的身分ID。  根據程式設計人員實施，這可能對應到媒體公司、程式設計人員或頻道。  傳統上，這會對應至管道。  隨著MML (March Madness Live)等偽頻道的建立，以及技術驅動的行動以解決MVPD驅動的資料限制，requestorID開始與媒體公司建立更多關聯。

## resourceID {#resource-id-def}

一般使用者要求的內容。  傳統上，這已識別與使用者請求的內容相關聯的頻道。  系統增強功能可讓ID代表特定節目（例如具有特定分級），而ID會繼續識別相關聯頻道。

## 風險指數 — 使用狀況 {#risk-index-usage}

此值也稱為「共用帳戶的使用量」，是根據每個帳戶發出的播放要求數量加上每個帳戶的共用機率來計算的。 也稱為「共用帳戶使用量風險指數」。

## 區段 {#segmet-def}

「區段」是一組符合使用者定義條件的科目，由選取的量度指定（例如「曾經觀看管道X、Y或Z的MVPD A、B、C、D或E使用者」）。

## 共用層級 {#sharing-level-def}

風險指數 — 帳戶或共用帳戶風險指數也稱為，它是根據一組選定MVPD中每個帳戶計算出的平均共用機率計算出的值，該組選定MVPD在選定的時間範圍內從其中一個選定的程式設計人員管道串流。

## 靜態裝置 {#static-device-def}

行動性極低的裝置。 例如，遊戲機、機上盒和電視機。

## 時間範圍 {#time-frame-def}

也稱為Period或Time Slot，它是包含使用者介面和表格中顯示的播放要求活動的時間視窗。

## 區段中的熱門MVPD {#top-mvpds-def}

所選區段中的前MVPD （最多10個），以共用層次、共用帳戶的使用情況或整體共用分數來測量。

## 趨勢 {#trend-def}

目前時段和上一個時段之間相關量度的百分比差異（例如，播放請求總數的百分比）。

## 不重複訂閱者 {#unique-subscriber-def}

在指定期間內與程式設計人員TV Everywhere應用程式或涉及Adobe Pass的網站互動的指定期間內不重複MVPD帳戶數目。  該互動包括程式設計人員應用程式或網站上導致呼叫Adobe Pass服務的任何活動。 例如，檢查authN或authZ狀態、驗證和授權。 如果程式設計師使用AdobeTempPass （即免費預覽）是區段的一部分，不重複訂閱者的總數也將包含不重複裝置數量。

## 使用狀況 {#usage-defs}

### 狂熱使用者 {#avid-user-def}

每月超過37個播放請求。

### 不常見的使用者 {#infrequent-users-def}

每月少於9個播放請求。

### 一般使用者 {#regular-user-def}

每月有9到37個播放請求。

## 使用模式 {#usage-patern-def}

套用至帳戶的有限類別標籤之一，在社交群組或行為（例如，小家庭、旅行者或通勤者、社交分享等）方面最能描述帳戶使用者。

## 郵遞區號 {#zip-code-def}

美國境內與地點相關聯的美國郵遞區號。
