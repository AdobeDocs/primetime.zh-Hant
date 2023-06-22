---
product: primetime
audience: end-user
user-guide-title: Primetime參考實作說明
user-guide-description: 協助瞭解TVSDK並修改功能管理員，以自訂您的個人播放器。
source-git-commit: 95626ebde981d1996652a67bc9e0cea05f24aa6d
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Android適用的PSDK 1.4參考實作 {#reference-implementation}

+ [Android參考實作概觀](home.md)
+ Primetime參考實作 {#reference}
   + [如何使用Primetime參考實作](ref-implementation/how-to-use-ref-player.md)
   + [參考實作結構](ref-implementation/ref-player-structure.md)
   + 如何使用功能管理員 {#feature-managers}
      + [如何使用功能管理員](ref-implementation/using-feature-managers/how-to-use-feature-managers.md)
      + [將設定資訊傳遞至MediaPlayer以建立功能管理員……](ref-implementation/using-feature-managers/creating-feature-managers.md)
      + [使用ManagerFactory開啟或關閉功能](ref-implementation/using-feature-managers/turning-features-on-off.md)
      + [處理事件](ref-implementation/using-feature-managers/handling-events.md)
   + 設定您的開發環境 {#setup-dev}
      + [設定您的開發環境](set-up-dev-environment/set-up-dev-environment-overview.md)
      + [下載及設定必要軟體](set-up-dev-environment/download-prereqs-android.md)
      + [建立Primetime參考實作](set-up-dev-environment/install-the-ref-player-project.md)
   + 探索程式碼 {#explore-code}
      + [Playerfragment](set-up-dev-environment/exploring-code/player-fragment.md)
      + [功能管理員](set-up-dev-environment/exploring-code/about-psdk-feature-managers.md)
      + [ConfigProvider](set-up-dev-environment/exploring-code/config-provider.md)
      + [設定活動](set-up-dev-environment/exploring-code/settings-activity.md)
      + [目錄格式](set-up-dev-environment/exploring-code/catalog-format.md)
      + [Primetime廣告的JSON物件](set-up-dev-environment/exploring-code/json-pt-ads.md)
      + [直接廣告插播的JSON物件](set-up-dev-environment/exploring-code/json-direct-ad-breaks.md)
      + [自訂廣告標籤的JSON物件](set-up-dev-environment/exploring-code/json-custom-ad-markers.md)
      + [權利資源ID的JSON物件](set-up-dev-environment/exploring-code/json-entitlement-resource-id.md)
      + [範例JSON摘要格式](set-up-dev-environment/exploring-code/example-json-feed-format.md)
   + 實作視訊播放 {#implement-video}
      + [視訊播放的基本作業](implement-video-playback/video-playback.md)
      + [啟用視訊播放](implement-video-playback/enable-video-playback.md)
      + [DRM內容保護](implement-video-playback/content-protection.md)
   + [多位元速率](implement-video-playback/mbr.md)
   + 設定播放器以播放具有廣告的DVR播放 {#dvr}
      + [沒有廣告插入的DVR](implement-video-playback/dvr/dvr-without-ad-insertion.md)
      + [具有廣告插入的DVR](implement-video-playback/dvr/dvr-with-ad-insertion.md)
      + [選擇DVR的自訂起點](implement-video-playback/dvr/dvr-custom-start-point.md)
      + [在參考實作中設定自訂開始時間](implement-video-playback/dvr/set-custom-start-time-dvr.md)
   + [顯示QoS播放和裝置統計資料](implement-video-playback/qos-statistics.md)
   + 插入廣告 {#insert-ads}
      + [廣告插入](insert-ads/ad-insertion.md)
      + [廣告插入型別](insert-ads/ad-insertion-types.md)
      + [新增廣告](insert-ads/add-advertising.md)
      + [相關API檔案](insert-ads/aps-callbacks-ad-insertion.md)
   + 延遲繫結音訊 {#late-binding-audio}
      + [概觀](late-binding-audio/late-binding-audio-overview.md)
      + [整合後期繫結音訊](late-binding-audio/aa-enable.md)
      + [選取音訊曲目](late-binding-audio/select-audio-tracks.md)
      + [相關API檔案](late-binding-audio/aa-api-callbacks.md)
   + Primetime驗證權益流程 {#primetime-authentications}
      + [概觀](paytvpass-entitlement/paytvpass-entitlement-overview.md)
      + [軟體權利檔案管理員概述](paytvpass-entitlement/entitlement-overvivew.md)
      + [整合Primetime驗證](paytvpass-entitlement/integrate-pass.md)
      + [設定Adobe Analytics報表](paytvpass-entitlement/pass-analytics-setup.md)
      + [相關API檔案](paytvpass-entitlement/pass-apis-callbacks.md)
   + 視訊分析 {#video-analytics}
      + [視訊分析](video-analytics/video-analytics-overview.md)
      + [建立Video Analytics管理員](video-analytics/create-video-analytics-manager.md)
      + [設定視訊分析](video-analytics/configure-video-analytics-manager.md)
      + [相關API檔案](video-analytics/va-apis-callbacks.md)
   + [建立自訂使用者介面](build-custom-ui.md)
   + [疑難排除](troubleshooting.md)
