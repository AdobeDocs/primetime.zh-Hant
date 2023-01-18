---
title: 帳戶IQ字彙表
description: 產品術語表。
exl-id: 2ee54442-9538-4c30-b999-265310b3935f
source-git-commit: 4eb5ba53fb3e0a0c314695fcd30cf15c7242b53c
workflow-type: tm+mt
source-wordcount: '1456'
ht-degree: 0%

---

# 產品概念和字彙表 {#glossary}

請參閱下列產品術語及其定義。

## 帳戶共用機率 {#account-sharing-probability-def}

控制面板，其中包含圖表，可將目前區段共用分數分成「非常低」、「低」、「中」、「高」和「非常高」的共用範圍類別。

## 動作 {#action-def}

與 [操作](#operation-def) 會影響相關操作區段（或同類群組）的特性（例如共用分數或使用中的裝置數）。

## 匯總分享分數 {#sharing-probability-level-def}

控制面板，其中包含圖表，可將目前區段共用分數分成「非常低」、「低」、「適中」、「高」和「非常高」等共用範圍類別，以及該區段串流總量的每個類別百分比。

## AuthN {#authn-def}

驗證或驗證嘗試次數。 驗證嘗試是指將當前沒有有效驗證狀態的用戶重定向到其所選MVPD的過程，在MVPD中，他們將自己標識到MVPD（通常使用用戶名和密碼）。

## AuthN確定 {#authn-ok-def}

成功驗證的次數。 當MVPD確認用戶標識並導致用戶被重新定向回程式設計師應用程式或站點時，將發生成功驗證。

## AuthZ {#authz-def}

授權，或授權請求的數量。 授權請求是程式設計師通過Adobe從MVPD請求許可以開始流式傳輸用戶請求的內容的過程。 MVPD通常會根據與使用者的MVPD訂閱相關聯的內容權限（例如與內容相關聯的頻道是否在使用者的訂閱中）來授與請求。 有些授權要求回應會由Adobe快取，這可讓Adobe立即回應，而不需將要求傳遞至MVPD。

## AuthZ確定 {#authz-ok-def}

成功授權的數量。

## 管道 {#channel-def}

管道也稱為屬性，是以主題相關的視訊內容來源。 傳統上代表來自MVPD的不同、數值可定址的連續視訊饋送。 該頻道直接映射到通過其機頂盒(STB)提供給用戶的可訪問的內容頻道。

## 叢集 {#cluster-def}

群集是位置和設備的集合。 群集是通過在設備之間查找公共位置而建立的。 已在共同位置看到的裝置將視為屬於相同叢集。 即使兩台設備沒有共同位置，但可以通過其他設備的位置連接，它們也可以位於同一群集中。

### 行動叢集 {#mobile-cluster-def}

沒有靜態設備的群集。

### 靜態群集 {#static-cluster-def}

具有至少一個靜態設備的群集。

## 並行 {#consurrency-def}

併發由兩個（或多個）同時播放或非常接近的時間流定義，因此它們之間的間隔不能通過以正常速度行駛來證明。
並行使用量是使用2個不同叢集之間的最大速度（英里/小時）計算。 如果用戶的速度在小於124英里的距離上大於124米/小時，或者其速度在大於124英里的距離上大於400米/小時，則被視為同時使用。 計算來自不同簇的位置之間的距離。 同一叢集中允許同時使用。

## 裝置 {#device-def}

一種數位視訊硬體產品，可播放Verywhere內容，並受Adobe Pass支援。 例如，智慧手機、筆記型電腦和台式電腦、遊戲機和智慧電視。

## 地理範圍 {#geographical-span-def}

一組位置中最遠點之間的距離。

## 粒度 {#granularity-def}

參考時間範圍，時段的大小；例如一週或一個月。

## 行業平均指數 {#industry-avg-index-def}

在所選時間範圍內為所有程式設計師和MVPD的每個風險索引（帳戶、使用、整體）計算的值。

## IP {#ip-def}

由網際網路服務提供商分配給設備的網際網路協定地址。 例如，電纜服務提供商和小區服務提供商。

## 隔離模式 {#isolation-mode-def}

一種共用分析，其中帳戶的評估僅限於在所選段中直接發生在程式設計師上的事件。  通常會評估所有帳戶事件，以提供更精確的共用估計。  某些MVPD資料的結構方式僅允許進行隔離模式分析。

## 位置 {#location-def}

地球上獨一無二的地方。 這也稱為特定播放請求的地理位置，使用Pass資料偵測，精度為1000mx1000m（一平方公里）。

<!-- ### Home location {#home-location-def}

the precision is 0.01 ~ 2000mx2000m (4 square km) - at this moment the home location is detected using an ML algo, based on data provided by two mvpds. The probability is ~ 80%. We are not using the zip code for the majority of the users. Currently, this information is not used in assessing the sharing probability. -->

## 媒體公司 {#media-company-def}

媒體公司是擁有一組媒體網路的公司。

## 量度 {#metric}

量度是訂閱者帳戶的屬性（例如其MVPD、其串流內容的程式設計人員和頻道、使用的裝置數量）。

## 行動裝置 {#mobile-device-def}

高移動性的設備。 例如行動電話和平板電腦。

## MVPD {#mvpd-def}

MVPD又稱「經銷商」，是媒體公司視訊內容的整合商、經銷商和經銷商。

## 操作 {#operation-def}

操作是為跟蹤特定效果而建立的記錄 [動作](#action-def) 在關聯的區段上。 動作的範例可以是對區段所識別之帳戶允許的同時資料流數量設定限制。

## 整體共用分數 {#overall-sharing-score}

一個值，可幫助用戶了解程式設計師屬性或MVPD訂閱者的密碼共用程度，並為用戶提供對其採取行動的緊迫感。

<!--**Aggregated Risk Index**
Also known as Risk Index and Sharing Risk Index, it is a value that helps users understand the magnitude of password sharing on Programmer properties or by MVPD subscribers and provides them a sense of urgency to act upon it.-->

<!--**Risk Index - Overall**
A value computed as an average of "Risk Index - Accounts" and the "Risk Index - Usage". Overall Sharing Risk Index-->

## 播放要求 {#play-requests-def}

由用戶端應用程式或網站提出的Adobe請求，以請求媒體Token來記錄和保護資料流啟動。

## 程式設計師 {#programmer-def}

程式設計師（又稱Network）是一家大公司（公司）的子公司，擁有和管理一個或多個渠道。

## requestorID {#requestorid-def}

媒體公司用來識別自己或MVPD之子公司的ID。  根據程式設計師實施，這可以映射到媒體公司、程式設計師或渠道。  媒體公司用來識別自己或MVPD子公司的最常見ID。  根據程式設計師實施，這可以映射到媒體公司、程式設計師或渠道。  傳統上，這會對應至管道。  隨著MML(March Extradis Live)等假頻道的建立，以及技術驅動的解決MVPD導向資料限制的動作，requestorID開始與媒體公司更相關聯。

## resourceID {#resource-id-def}

一般使用者要求的內容。  傳統上，這會識別與使用者要求內容相關聯的管道。  系統增強功能允許該ID代表特定節目（例如具有特定評等），該ID會繼續識別相關的頻道。

## 風險指數 — 使用情況 {#risk-index-usage}

也稱為「來自共用帳戶的使用量」，此值是根據每個帳戶所發出的播放請求數，以每個帳戶的共用機率加權而計算。 它也稱為「按共用帳戶列出的使用情況風險索引」。

## 區段 {#segmet-def}

區段是一組帳戶，符合選取量度所指定的使用者定義條件（例如「已觀看頻道X、Y或Z的MVPD A、B、C、D或E的使用者」）。

## 共用層級 {#sharing-level-def}

它也稱為風險索引 — 帳戶或共用帳戶風險索引，它是根據在所選時間範圍內從選定程式設計師通道之一流化的選定MVPD集合中每個帳戶的共用概率的平均值計算的值。

## 靜態裝置 {#static-device-def}

移動性很低的設備。 例如遊戲機、機頂盒和電視機。

## 時間範圍 {#time-frame-def}

這也稱為時段或時段，它是包含從頭到尾在使用者介面和表格中呈現的播放請求活動的時段。

## 區段中排名最前的MVPD {#top-mvpds-def}

選取區段中排名最前（最多10個）的MVPD，可依「共用」層級、「來自共用帳戶的使用量」或「整體共用分數」來測量。

## 趨勢 {#trend-def}

目前與上一個期間之間，相關聯量度的百分比差異（例如播放請求總數的百分比）。

## 不重複訂閱者 {#unique-subscriber-def}

在指定時段內，唯一MVPD的數量會與程式設計師TV Everywhere應用程式或網站互動，這些應用程式或網站涉及Adobe Pass。  該互動包括程式設計師應用程式或網站上導致呼叫Adobe Pass服務的任何活動。 例如，檢查authN或authZ狀態、驗證和授權。 如果程式設計人員使用AdobeTempPass（免費預覽）是區段的一部分，則不重複訂閱者的總數也會包含不重複裝置的數量。

## 使用狀況 {#usage-defs}

### Avid用戶 {#avid-user-def}

每月超過37個播放請求。

### 不頻繁用戶 {#infrequent-users-def}

每月播放請求少於9個。

### 一般使用者 {#regular-user-def}

每月9到37個播放請求。

## 使用模式 {#usage-patern-def}

適用於帳戶的一組有限類別標籤中的一個，該標籤以社交群體或行為（例如，小家庭、旅行者或通勤者、社交分享等）為帳戶的使用者提供最佳特徵。

## 郵遞區號 {#zip-code-def}

與美國境內位置相關聯的美國郵遞區號
