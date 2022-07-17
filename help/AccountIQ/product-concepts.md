---
title: 帳戶IQ辭彙表
description: '產品術語表。  '
source-git-commit: 8d8aa00d693b1ca7f960a71b40053e47249c63e4
workflow-type: tm+mt
source-wordcount: '1455'
ht-degree: 0%

---

# 產品概念和辭彙表 {#glossary}

請參閱以下產品術語及其定義。

## 帳戶共用概率 {#account-sharing-probability-def}

一個儀表板面板，其中包含圖表，將共用分數的當前段分為「非常低」、「低」、「中等」、「高」和「非常高」的共用範圍類別。

## 操作 {#action-def}

與 [操作](#operation-def) 影響相關操作段（或隊列）的特徵（例如，共用分數或正在使用的設備數）。

## 聚合共用分數 {#sharing-probability-level-def}

一個儀表板面板，其中包含圖表，將共用分數的當前段分為「非常低」、「低」、「中等」、「高」和「非常高」等共用範圍類別，以及段的流總量的每個類別百分比。

## 身份驗證 {#authn-def}

身份驗證或身份驗證嘗試次數。 驗證嘗試是指將當前沒有有效驗證狀態的用戶重定向到其選擇的MVPD的過程，在MVPD中，用戶將自己標識到MVPD — 通常使用用戶名和密碼。

## AuthN確定 {#authn-ok-def}

成功身份驗證的次數。 當用戶標識被MVPD確認並導致用戶被重定向回程式設計師應用或站點時，會發生成功驗證。

## 身份驗證 {#authz-def}

授權，或授權請求數。 授權請求是程式設計師通過Adobe從MVPD請求許可以開始對用戶請求的內容進行流處理的過程。 MVPD通常基於與用戶的MVPD訂閱相關聯的內容權限（例如，與內容相關聯的頻道是否在用戶的訂閱中）來授予請求。 某些授權請求響應由Adobe快取，這允許Adobe立即響應而不將請求傳遞到MVPD。

## AuthZ確定 {#authz-ok-def}

成功授權的數量。

## 頻道 {#channel-def}

頻道也稱為屬性，是與主題相關的視頻內容源。 傳統上表示來自MVPD的不同的、數字可定址的連續視頻饋送。 該頻道直接映射到通過其機頂盒(STB)提供給用戶的內容的可訪問頻道。

## 群集 {#cluster-def}

群集是位置和設備的集合。 通過在設備之間查找公共位置建立群集。 已在公共位置看到的設備將被視為屬於同一群集。 兩個設備可以位於同一群集中，即使它們沒有公共位置，但可以通過其他設備的位置進行連接。

### 移動集群 {#mobile-cluster-def}

沒有靜態設備的群集。

### 靜態群集 {#static-cluster-def}

具有至少一個靜態設備的群集。

## 併發 {#consurrency-def}

併發由兩個（或多個）同時播放或非常接近的時間流定義，因此它們之間的間隔不能通過以正常速度行進來被證明。
併發使用率是使用2個不同群集之間的最大速度（英里/小時）計算的。 如果用戶在小於124英里的距離上的速度大於124米/小時，或者在大於124英里的距離上的速度大於400米/小時，則被視為同時使用。 計算來自不同簇的位置之間的距離。 允許在同一群集中使用併發。

## 設備 {#device-def}

一種數字視頻硬體產品，能夠播放Everywhere內容並受Adobe Pass支援。 例如，智慧電話、筆記型電腦和台式電腦、遊戲機和智慧電視。

## 地理範圍 {#geographical-span-def}

一組位置中最遠點之間的距離。

## 粒度 {#granularity-def}

在參考時間幀時，週期的大小；比如一週或一個月。

## 行業平均指數 {#industry-avg-index-def}

在所選時間範圍內為所有程式設計師和MVPD中的每個風險索引（帳戶、使用、總體）計算的值。

## IP {#ip-def}

由Internet服務提供商分配給設備的Internet協定地址。 例如，電纜服務提供商和小區服務提供商。

## 隔離模式 {#isolation-mode-def}

一種共用分析類型，其中帳戶的評估僅限於在選定段中程式設計師上直接發生的事件。  通常，會評估所有帳戶事件，從而提供更準確的共用估計。  某些MVPD資料的結構方式僅允許隔離模式分析。

## 位置 {#location-def}

地球上獨一無二的點。 也稱為使用Pass資料檢測的特定播放請求的地理位置，精度為1000mx1000m（1平方公里）。

<!-- ### Home location {#home-location-def}

the precision is 0.01 ~ 2000mx2000m (4 square km) - at this moment the home location is detected using an ML algo, based on data provided by two mvpds. The probability is ~ 80%. We are not using the zip code for the majority of the users. Currently, this information is not used in assessing the sharing probability. -->

## 媒體公司 {#media-company-def}

媒體公司是擁有一組媒體網路的公司。

## 度量 {#metric}

度量是訂戶帳戶的屬性（例如，其MVPD、其流內容的程式設計師和通道、使用的設備數）。

## 移動裝置 {#mobile-device-def}

一種具有高移動性的設備。 例如手機和平板電腦。

## MVPD {#mvpd-def}

MVPD又稱「分銷商」，是媒體公司視頻內容的聚合器、轉銷商和分銷商。

## 操作 {#operation-def}

操作是為跟蹤特定對象的影響而建立的記錄 [動作](#action-def) 段。 操作的示例可以是對段標識的帳戶允許的併發流數的限制。

## 總體共用分數 {#overall-sharing-score}

一個值，幫助用戶瞭解程式設計師屬性或MVPD訂戶上密碼共用的程度，並為他們提供採取行動的緊迫感。

<!--**Aggregated Risk Index**
Also known as Risk Index and Sharing Risk Index, it is a value that helps users understand the magnitude of password sharing on Programmer properties or by MVPD subscribers and provides them a sense of urgency to act upon it.-->

<!--**Risk Index - Overall**
A value computed as an average of "Risk Index - Accounts" and the "Risk Index - Usage". Overall Sharing Risk Index-->

## 播放請求 {#play-requests-def}

客戶端應用或站點向Adobe請求媒體令牌以記錄和保護流啟動的請求。

## 程式設計師 {#programmer-def}

程式設計師又稱網路，是一家擁有和管理一個或多個渠道的較大公司（公司）的子公司。

## 請求者ID {#requestorid-def}

媒體公司用於標識自己或MVPD子公司的ID。  根據程式設計師實施情況，這可以映射到媒體公司、程式設計師或渠道。  媒體公司用於標識自己或MVPD子公司的最常見ID。  根據程式設計師實施情況，這可以映射到媒體公司、程式設計師或渠道。  傳統上，此映射到通道。  隨著MML(March Madres Live)等偽通道的建立以及技術驅動的解決MVPD驅動資料限制的舉措，請求者ID開始與媒體公司更加相關。

## 資源ID {#resource-id-def}

最終用戶請求的內容。  傳統上，這會標識與用戶請求的內容關聯的渠道。  系統增強允許該ID表示特定程式（例如具有特定分級），該ID繼續標識關聯的通道。

## 風險指數 — 使用情況 {#risk-index-usage}

也稱為「來自共用帳戶的使用」，它是根據每個帳戶的播放請求數計算的值，該請求數由每個帳戶的共用概率加權。 也稱為「按共用帳戶使用風險索引」。

## 段 {#segmet-def}

段是一組滿足選定度量指定的用戶定義條件的帳戶（例如，「MVPD A、B、C、D或E的用戶，這些用戶已觀看X、Y或Z頻道」）。

## 共用級別 {#sharing-level-def}

也稱為「風險索引 — 帳戶」或「共用帳戶風險索引」，它是根據在所選時間範圍內從選定程式設計師通道之一流式傳輸的一組選定MVPD中每個帳戶計算的共用概率的平均值計算的值。

## 靜態設備 {#static-device-def}

一種移動性很低的設備。 例如，遊戲機、機頂盒和電視機。

## 時間框 {#time-frame-def}

也稱為時段或時隙，它是包含從開始到結束在用戶介面和表中表示的播放請求活動的時間窗口。

## 段中的頂級MVPD {#top-mvpds-def}

所選段中的頂部（最多10個）MVPD按「共用」級別、「來自共用帳戶的使用情況」或「總體共用分數」作為度量。

## 趨勢 {#trend-def}

當前時段和上一時段之間關聯度量的百分比差異（例如，播放請求總數的百分比）。

## 唯一訂閱者 {#unique-subscriber-def}

在特定時段內與程式設計師TV Everywhere應用程式或網站交互的唯一MVPD帳戶的數量，這些應用程式或網站涉及Adobe Pass。  該互動包括程式設計師應用或網站上導致呼叫Adobe Pass服務的任何活動。 例如，檢查authN或authZ狀態、驗證和授權。 如果程式設計師使用AdobeTempPass（即免費預覽）是段的一部分，則唯一訂閱者總數還將包括唯一設備數。

## 用法 {#usage-defs}

### Avid用戶 {#avid-user-def}

每月37次以上的播放請求。

### 不頻繁的用戶 {#infrequent-users-def}

每月播放請求少於9次。

### 常規用戶 {#regular-user-def}

每月9到37次播放請求。

## 使用模式 {#usage-patern-def}

應用於帳戶的一組有限類別標籤中的一個，該標籤最能說明帳戶用戶的社會群體或行為（例如，小家庭、旅行者或通勤者、社會共用等）。

## 郵遞區號 {#zip-code-def}

與美國境內的地點關聯的美國郵遞區號
