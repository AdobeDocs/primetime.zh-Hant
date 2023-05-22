---
description: 您可以使用Mogine Player Objective-C API自定義播放器的行為。
title: 媒體播放器類
exl-id: b58efff0-2455-4db5-93a0-4624291dc526
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# 媒體播放器類 {#media-player-classes}

您可以使用Mogine Player Objective-C API自定義播放器的行為。

這些類描述媒體播放器及其資源。

| 類 | 說明 |
|---|---|
| PTABRControlParameters | 封裝所有自適應比特率控制參數。 支援的參數有：<ul><li>最小比特率</li><li>最大比特率</li><li>初始比特率</li></ul> |
| PTDefaultMediaPlayerClientFactory | TVSDK中PTMediaPlayerClientFactority的預設實現。 它提供可用的PTOpportunityResolver、PTContentResolver和PTAdPolicySelector實例。 |
| PTMediaPlayer | 定義Mogfire Player框架的根元件。應用程式建立此類的實例以回放媒體。 此元件將派發通知，以通知您的應用程式在任何給定時間瞭解播放器的狀態。 |
| PTMediaPlayerClientFactory | 描述自定義媒體播放器客戶端工廠應實施的方法以提供可用的PTOpportunityResolver、PTContentResolver和PTAdPolicySelector實例的協定。 |
| PTMediaPlayerItem | 表示特定的音頻 — 視頻媒體。 |
| PTMediaPlayerView | 管理Mogine Player框架的視圖元件。 |
| PTMedia配置檔案 | 表示變型播放清單中單個流的配置檔案。 |
| PTMediaSelection選項 | 表示一個視聽媒體資源，以適應不同的語言首選項、輔助功能要求或自定義應用程式配置。 有效選項類型：<ul><li>字幕(PTMediaSelectionOptionTypeSubtilet)</li><li>備用音頻(PTMediaSelectionOptionTypeAudio)</li><li>隱藏字幕(PTMediaSelectionOptionTypeCC)</li><li>未定義(PTMediaSelectionOptionTypeUndefined)</li></ul> |
| PTOpportunityResolver類，PTOpportunityResolver協定 | 用於處理清單內提示的類，該類將用作Adobe Primetime和決策過程的放置。 |
| PTOpportunityResolverDelegate | 描述自定義機會解析器(PTOpportunityResolver)應用於向委託傳遞解決機會狀態的方法的協定。 |
| PTSDK | 描述TVSDK的版本及其功能。 |
| PTSDKConfig | 公開TVSDK全局設定並允許應用程式訂閱自定義HLS標籤。 |
| PTTextStyleRule | 定義表示構成規則字典的文本樣式屬性鍵的常數。 |
