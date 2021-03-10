---
description: 您可以使用Primetime Player Objective-C API來自訂播放器的行為。
title: 媒體播放器類別
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# 媒體播放器類{#media-player-classes}

您可以使用Primetime Player Objective-C API來自訂播放器的行為。

這些類別會說明您的媒體播放器及其資源。

| 類別 | 說明 |
|---|---|
| PTABRControlParameters | 封裝所有自適應位速率控制參數。 支援的參數包括：<ul><li>minBitRate</li><li>maxBitRate</li><li>initialBitRate</li></ul> |
| PTDefaultMediaPlayerClientFactory | 在TVSDK中預設實作PTMediaPlayerClientFactory。 它提供了availablePTOportunityResolver、PTContentResolver和PTAdPolicySelector實例。 |
| PTMediaPlayer | 定義Primetime Player架構的根元件。應用程式會建立此類別的例項，以播放媒體。 此元件會派單通知，讓您的應用程式隨時得知播放器的狀態。 |
| PTMediaPlayerClientFactory | 描述定制媒體播放器客戶端工廠應實施的方法的協定，以提供可用的PTOportunityResolver、PTContentResolver和PTAdPolicySelector實例。 |
| PTMediaPlayerItem | 代表特定的音訊——視訊媒體。 |
| PTMediaPlayerView | 管理Primetime Player架構的檢視元件。 |
| PTMediaProfile | 代表變型播放清單中單一串流的描述檔。 |
| PTMediaSelectionOption | 代表視聽媒體資源，以適應不同的語言偏好、協助工具需求或自訂應用程式組態。 有效的選項類型：<ul><li>字幕(PTMediaSelectionOptionTypeSubtitle)</li><li>替代音訊(PTMediaSelectionOptionTypeAudio)</li><li>隱藏字幕(PTMediaSelectionOptionTypeCC)</li><li>未定義(PTMediaSelectionOptionTypeUndefined)</li></ul> |
| PTOportunityResolver類，PTOportunityResolver協定 | 用於處理資訊清單內提示的類別，這些類別將用作Adobe Primetime廣告決策程式的位置。 |
| PTOportunityResolverDelegate | 描述自定義業務機會解析器(PTOportunityResolver)應用於向委派通信業務機會解析狀態的方法的協定。 |
| PTSDK | 說明TVSDK的版本及其功能。 |
| PTSDKConfig | 公開TVSDK全域設定，並允許應用程式訂閱自訂HLS標籤。 |
| PTTextStyleRule | 定義表示構成規則字典的文本樣式屬性鍵的常數。 |
