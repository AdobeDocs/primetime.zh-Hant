---
description: 您可以使用Primetime播放器Objective-C API來自訂播放器的行為。
title: 媒體播放器類別
exl-id: b58efff0-2455-4db5-93a0-4624291dc526
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# 媒體播放器類別 {#media-player-classes}

您可以使用Primetime播放器Objective-C API來自訂播放器的行為。

這些類別會說明您的媒體播放器及其資源。

| 類別 | 說明 |
|---|---|
| PTABRControlParameters | 封裝所有自適應位元速率控制引數。 支援的引數包括：<ul><li>minBitRate</li><li>maxBitRate</li><li>initialBitrate</li></ul> |
| PTDefaultMediaPlayerClientFactory | TVSDK中PTMediaPlayerClientFactory的預設實作。 它提供availablePTOpportunityResolver、PTContentResolver和PTAdPolicySelector執行個體。 |
| PTMediaPlayer | 定義Primetime播放器架構的根元件。應用程式會建立此類別的執行個體來播放媒體。 此元件會傳送通知，讓您的應用程式隨時知道播放器的狀態。 |
| PTMediaPlayerClientFactory | 描述自訂媒體播放器使用者端工廠應實作的方法，以提供可用的PTOpportunityResolver、PTContentResolver和PTAdPolicySelector執行個體的通訊協定。 |
| PTMediaPlayerItem | 代表特定的音訊 — 視訊媒體。 |
| PTMediaPlayerView | 管理Primetime播放器架構的檢視元件。 |
| PTMediaProfile | 代表變體播放清單中單一資料流的設定檔。 |
| PTMediaSelectionOption | 代表視聽媒體資源，可因應不同的語言偏好設定、協助工具要求或自訂應用程式設定。 有效的選項型別：<ul><li>字幕(PTMediaSelectionOptionTypeSubtitle)</li><li>替代音訊(PTMediaSelectionOptionTypeAudio)</li><li>隱藏式字幕(PTMediaSelectionOptionTypeCC)</li><li>未定義(PTMediaSelectionOptionTypeUndefined)</li></ul> |
| PTOpportunityResolver類別，PTOpportunityResolver通訊協定 | 用於處理資訊清單內提示的類別，這些提示將用作Adobe Primetime廣告決策程式的版位。 |
| PTOpportunityResolverDelegate | 說明自訂機會解析器( PTOpportunityResolver )應該用來與委派通訊機會解析狀態的通訊協定。 |
| PTSDK | 說明TVSDK的版本及其功能。 |
| PTSDKConfig | 公開TVSDK全域設定，並允許應用程式訂閱自訂HLS標籤。 |
| PTTextStyleRule | 定義組成規則字典的文字樣式屬性索引鍵的常數。 |
