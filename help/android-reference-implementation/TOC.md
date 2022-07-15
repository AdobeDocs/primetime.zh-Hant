---
product: primetime
audience: end-user
user-guide-title: Primetime 參考實作說明
user-guide-description: 協助了解 TVSDK 並修改功能管理員，以自訂您的個人播放器。
source-git-commit: 95626ebde981d1996652a67bc9e0cea05f24aa6d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 用於Android參考實現的PSDK 1.4 {#reference-implementation}

+ [Android參考實施概述](home.md)
+ 黃金時段參考實現 {#reference}
   + [如何使用黃金時段參考實現](ref-implementation/how-to-use-ref-player.md)
   + [參考實現結構](ref-implementation/ref-player-structure.md)
   + 如何使用功能管理器 {#feature-managers}
      + [如何使用功能管理器](ref-implementation/using-feature-managers/how-to-use-feature-managers.md)
      + [通過將配置資訊傳遞給MediaPlayer建立功能管理器……](ref-implementation/using-feature-managers/creating-feature-managers.md)
      + [使用ManagerFactory開啟或關閉特徵](ref-implementation/using-feature-managers/turning-features-on-off.md)
      + [處理事件](ref-implementation/using-feature-managers/handling-events.md)
   + 設定開發環境 {#setup-dev}
      + [設定開發環境](set-up-dev-environment/set-up-dev-environment-overview.md)
      + [下載和配置必備軟體](set-up-dev-environment/download-prereqs-android.md)
      + [構建黃金時段參考實現](set-up-dev-environment/install-the-ref-player-project.md)
   + 瀏覽代碼 {#explore-code}
      + [播放器片段](set-up-dev-environment/exploring-code/player-fragment.md)
      + [功能管理器](set-up-dev-environment/exploring-code/about-psdk-feature-managers.md)
      + [配置提供程式](set-up-dev-environment/exploring-code/config-provider.md)
      + [設定活動](set-up-dev-environment/exploring-code/settings-activity.md)
      + [目錄格式](set-up-dev-environment/exploring-code/catalog-format.md)
      + [用於黃金時段廣告的JSON對象](set-up-dev-environment/exploring-code/json-pt-ads.md)
      + [用於直接廣告分段的JSON對象](set-up-dev-environment/exploring-code/json-direct-ad-breaks.md)
      + [自定義廣告標籤的JSON對象](set-up-dev-environment/exploring-code/json-custom-ad-markers.md)
      + [權利資源ID的JSON對象](set-up-dev-environment/exploring-code/json-entitlement-resource-id.md)
      + [示例JSON源格式](set-up-dev-environment/exploring-code/example-json-feed-format.md)
   + 實現視頻播放 {#implement-video}
      + [視頻播放的基本操作](implement-video-playback/video-playback.md)
      + [啟用視頻播放](implement-video-playback/enable-video-playback.md)
      + [DRM內容保護](implement-video-playback/content-protection.md)
   + [多比特率](implement-video-playback/mbr.md)
   + 設定播放器以通過廣告進行DVR回放 {#dvr}
      + [無廣告插入的DVR](implement-video-playback/dvr/dvr-without-ad-insertion.md)
      + [帶廣告插入的DVR](implement-video-playback/dvr/dvr-with-ad-insertion.md)
      + [為DVR選擇自定義起點](implement-video-playback/dvr/dvr-custom-start-point.md)
      + [在引用實現中設定自定義開始時間](implement-video-playback/dvr/set-custom-start-time-dvr.md)
   + [顯示QoS回放和設備統計資訊](implement-video-playback/qos-statistics.md)
   + 插入廣告 {#insert-ads}
      + [廣告插入](insert-ads/ad-insertion.md)
      + [廣告插入類型](insert-ads/ad-insertion-types.md)
      + [添加廣告](insert-ads/add-advertising.md)
      + [相關API文檔](insert-ads/aps-callbacks-ad-insertion.md)
   + 延遲綁定音頻 {#late-binding-audio}
      + [概述](late-binding-audio/late-binding-audio-overview.md)
      + [整合後綁定音頻](late-binding-audio/aa-enable.md)
      + [選擇音頻軌道](late-binding-audio/select-audio-tracks.md)
      + [相關API文檔](late-binding-audio/aa-api-callbacks.md)
   + 黃金時段驗證權限流 {#primetime-authentications}
      + [概述](paytvpass-entitlement/paytvpass-entitlement-overview.md)
      + [權利檔案管理器概述](paytvpass-entitlement/entitlement-overvivew.md)
      + [整合Mighine身份驗證](paytvpass-entitlement/integrate-pass.md)
      + [配置Adobe Analytics報告](paytvpass-entitlement/pass-analytics-setup.md)
      + [相關API文檔](paytvpass-entitlement/pass-apis-callbacks.md)
   + 視頻分析 {#video-analytics}
      + [視頻分析](video-analytics/video-analytics-overview.md)
      + [建立視頻分析管理器](video-analytics/create-video-analytics-manager.md)
      + [配置視頻分析](video-analytics/configure-video-analytics-manager.md)
      + [相關API文檔](video-analytics/va-apis-callbacks.md)
   + [構建自定義用戶介面](build-custom-ui.md)
   + [故障排除](troubleshooting.md)
