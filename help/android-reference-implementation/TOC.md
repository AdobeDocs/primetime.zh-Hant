---
product: primetime
audience: end-user
user-guide-title: Primetime 參考實作說明
user-guide-description: 協助了解 TVSDK 並修改功能管理員，以自訂您的個人播放器。
translation-type: tm+mt
source-git-commit: 95626ebde981d1996652a67bc9e0cea05f24aa6d
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 7%

---


# PSDK 1.4 for Android參考實作{#reference-implementation}

+ [Android參考實作概觀](home.md)
+ Primetime參考實作{#reference}
   + [如何使用Primetime參考實作](ref-implementation/how-to-use-ref-player.md)
   + [參考實作結構](ref-implementation/ref-player-structure.md)
   + 如何使用功能管理器{#feature-managers}
      + [如何使用功能管理員](ref-implementation/using-feature-managers/how-to-use-feature-managers.md)
      + [將設定資訊傳遞至MediaPlayer，以建立功能管理員……](ref-implementation/using-feature-managers/creating-feature-managers.md)
      + [使用ManagerFactory開啟或關閉功能](ref-implementation/using-feature-managers/turning-features-on-off.md)
      + [處理事件](ref-implementation/using-feature-managers/handling-events.md)
   + 設定您的開發環境{#setup-dev}
      + [設定您的開發環境](set-up-dev-environment/set-up-dev-environment-overview.md)
      + [下載並設定先決條件軟體](set-up-dev-environment/download-prereqs-android.md)
      + [建立Primetime參考實作](set-up-dev-environment/install-the-ref-player-project.md)
   + 探索程式碼{#explore-code}
      + [播放器片段](set-up-dev-environment/exploring-code/player-fragment.md)
      + [功能管理員](set-up-dev-environment/exploring-code/about-psdk-feature-managers.md)
      + [ConfigProvider](set-up-dev-environment/exploring-code/config-provider.md)
      + [SettingsActivity](set-up-dev-environment/exploring-code/settings-activity.md)
      + [目錄格式](set-up-dev-environment/exploring-code/catalog-format.md)
      + [Primetime廣告的JSON物件](set-up-dev-environment/exploring-code/json-pt-ads.md)
      + [直接廣告插播的JSON物件](set-up-dev-environment/exploring-code/json-direct-ad-breaks.md)
      + [自訂廣告標籤的JSON物件](set-up-dev-environment/exploring-code/json-custom-ad-markers.md)
      + [權益資源ID的JSON物件](set-up-dev-environment/exploring-code/json-entitlement-resource-id.md)
      + [範例JSON摘要格式](set-up-dev-environment/exploring-code/example-json-feed-format.md)
   + 實作視訊播放{#implement-video}
      + [視訊播放的基本操作](implement-video-playback/video-playback.md)
      + [啟用視訊播放](implement-video-playback/enable-video-playback.md)
      + [DRM內容保護](implement-video-playback/content-protection.md)
   + [多位元速率](implement-video-playback/mbr.md)
   + 設定DVR播放的播放器，其中包含廣告{#dvr}
      + [DVR，不需插入廣告](implement-video-playback/dvr/dvr-without-ad-insertion.md)
      + [具有廣告插入功能的DVR](implement-video-playback/dvr/dvr-with-ad-insertion.md)
      + [選擇DVR的自訂起點](implement-video-playback/dvr/dvr-custom-start-point.md)
      + [在參考實作中設定自訂開始時間](implement-video-playback/dvr/set-custom-start-time-dvr.md)
   + [顯示QoS播放和裝置統計資料](implement-video-playback/qos-statistics.md)
   + 插入廣告{#insert-ads}
      + [廣告插入](insert-ads/ad-insertion.md)
      + [廣告插入類型](insert-ads/ad-insertion-types.md)
      + [新增廣告](insert-ads/add-advertising.md)
      + [相關API檔案](insert-ads/aps-callbacks-ad-insertion.md)
   + 延遲裝訂音訊{#late-binding-audio}
      + [概觀](late-binding-audio/late-binding-audio-overview.md)
      + [整合後期系結音訊](late-binding-audio/aa-enable.md)
      + [選取音軌](late-binding-audio/select-audio-tracks.md)
      + [相關API檔案](late-binding-audio/aa-api-callbacks.md)
   + Primetime驗證權益流{#primetime-authentications}
      + [概觀](paytvpass-entitlement/paytvpass-entitlement-overview.md)
      + [權益管理員概述](paytvpass-entitlement/entitlement-overvivew.md)
      + [整合Primetime驗證](paytvpass-entitlement/integrate-pass.md)
      + [配置Adobe Analytics報告](paytvpass-entitlement/pass-analytics-setup.md)
      + [相關API檔案](paytvpass-entitlement/pass-apis-callbacks.md)
   + 視訊分析{#video-analytics}
      + [視訊分析](video-analytics/video-analytics-overview.md)
      + [建立視訊分析管理員](video-analytics/create-video-analytics-manager.md)
      + [設定視訊分析](video-analytics/configure-video-analytics-manager.md)
      + [相關API檔案](video-analytics/va-apis-callbacks.md)
   + [建立自訂使用者介面](build-custom-ui.md)
   + [疑難排解](troubleshooting.md)
