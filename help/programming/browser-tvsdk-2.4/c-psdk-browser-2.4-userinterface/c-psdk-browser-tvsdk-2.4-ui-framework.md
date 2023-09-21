---
description: UI架構是瀏覽器TVSDK上方的UI層，可立即提供各種視訊播放器相關UI結構。 您可以透過進行適合您環境的點變更，來建立高度可自訂的播放器。
title: UI架構
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 0%

---

# UI架構 {#the-ui-framework}

UI架構是瀏覽器TVSDK上方的UI層，可立即提供各種視訊播放器相關UI結構。 您可以透過進行適合您環境的點變更，來建立高度可自訂的播放器。

>[!TIP]
>
>視覺（外觀設計）和UI行為是可自訂的。

您可以重寫自己的行為或覆寫某些預設行為的功能。 您也可以從頭開始撰寫行為，以重複使用SDK提供的行為。

## 建立基本播放器 {#section_30E4812C4DDA4B519C9C837930B6AE45}

`primetimevisualapi.min.js` 是UI架構程式庫，其所有功能會透過全域物件ptp公開。 在以下範例中， `videoPlayer` 方法會建立基礎播放器：

```js
<script src="scripts/primetimevisualapi.min.js"></script> 
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
    })(); 
</script>
```

## 設定播放器 {#section_9FC936B983CD40439E6D7675197B226C}

您可以透過下列其中一種方式設定播放器：

* 使用JSON物件
* 使用API

若要產生JSON物件，瀏覽器TVSDK提供UI設定器工具。 在工具中，您可以選取各種設定，按一下 **[!UICONTROL Test Configuration]** 以驗證設定，然後按一下 **[!UICONTROL Download Configuration]** 以下載設定。 下載檔案的內容會用作JSON物件，以傳遞至 `ptp.videoPlayer` API。

**如何執行UI設定器工具**：

1. 託管 `frameworks` 資料夾（可在本機Web伺服器上的瀏覽器TVSDK中使用）。
1. 若要開啟工具，請開啟瀏覽器並導覽至 `< path-to-hosted-frameworks-folder>/ui-framework/ui-configurator/`.

**設定播放器的行為**

您可以透過下列其中一種方式來設定播放器行為：

>[!TIP]
>
>對於某些設定，兩個選項都可用。

* **使用videoBehavior API** `ptp.videoPlayer` 傳回 `ptp.videoBehavior`，可讓您設定基礎的視訊播放器。 如果需要設定某些播放相關設定，您可以使用此選項。

  ```js
  player.setAbrControlParameters ({object})
  ```

* **將設定物件傳遞至videoPlayer函式** 使用此物件時，除了上方討論的播放設定外，還可以設定UI的行為。 呼叫者需要指定必須變更的引數，播放器將繼續使用未指定引數的預設值。

  ```js
  var player = ptp.videoPlayer('#video1', { 
          player: { 
              abrControlParameters : {object} 
      }, 
      controlBar : {object} 
  });
  ```

  在上述範例中，ABR控制引數是使用組態物件來設定的。 也傳遞了物件以設定控制列行為。

  請參閱下方的檢視組態物件結構一節，瞭解組態物件的結構。

* **存取AdobePSDK.MediaPlayer** 您可以使用 `videoPlayer.getMediaPlayer` 在某些進階使用案例中，您需要存取瀏覽器TVSDK的MediaPlayer。

* **設定播放器的外觀設定** 如需建立播放器外觀的詳細資訊，請參閱 [為播放器建立外觀](../../browser-tvsdk-2.4/c-psdk-browser-2.4-userinterface/c-psdk-browser-tvsdk-2.4-skin-the-player.md).

## 修改預設行為 {#section_D5D692638FFF4BEF81F7BE70E438CCE9}

在UI架構術語中，行為是定義特定元件之視覺部分和互動部分的建構。 使用下列物件結構，您可以修改您要變更的行為。

例如，在體積塊滑桿可見後，如果您不想隱藏它，請使用下列範例：

```js
var customVolumeSliderBehavior = function (element, configuration, player) { 
    function neverHide() { 
        // do nothing 
 } 
 
    var api = ptp.volumeSliderBehavior(element, configuration, player) 
        .compose({ 
            hide: neverHide 
 }); 
    return api; 
}; 
var player = ptp.videoPlayer('.videoHolder', { 
    controlBar : { 
        volume: { 
            slider: { 
                behavior: customVolumeSliderBehavior 
 } 
        } 
    } 
}
```

>[!NOTE]
>
>根據您想要的自訂內容，您可以覆寫行為中的特定功能，或撰寫您自己的行為。 如需有關哪些功能可以覆寫的詳細資訊，請參閱 [UI框架](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/index.html) API檔案。

## 引用 {#section_0A76A3F44D8A49B09FE4C83F3FACCB76}

以下是其他參考資訊：

* **檢視組態物件結構** 這是完整的物件結構，會以階層方式提及所有預設行為，以及行為的預設元素。 在範例設定中，使用UI工廠來建立元素。 您可以使用相同的或您偏好的方法來建構元素。

  您只需要指定想要變更的零件，其餘的功能將從預設值中選取。 若要開始，視使用案例而定，您必須提供 `SingleViewConfigurationObject` 或 `MultiViewConfigurationObject` 結構。

  ```js
  var DEFAULT_CONTROL_BAR_CONFIG = { 
      behavior: ptp.controlBarBehavior, 
      element: ptp.factories.simpleDivFactory(null, ptp.elementGetter(selector), 'ptp-control-bar'), 
      audioTrack: { 
          behavior: ptp.audioTrackButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('audioTrackBtn', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-audio-track ptp-control-bar-btn') 
      }, 
      closedCaption: { 
          behavior: ptp.closedCaptionButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('cc', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ' + 
              'ptp-btn-closed-caption ptp-control-bar-btn hidden', 
              'CC') 
      }, 
      displayTime: { 
          behavior: ptp.timeRemainingBehavior, 
          element: ptp.factories.simpleDivFactory('displayTime', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-txt-control ptp-txt-display-time') 
      }, 
      fastForward: { 
          behavior: ptp.fastForwardButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('fastForward', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-fastforward ptp-control-bar-btn', 
              'Fast Forward') 
      }, 
      fastRewind: { 
          behavior: ptp.fastRewindButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('fastRewind', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-fastrewind ptp-control-bar-btn', 
              'Fast Rewind') 
      }, 
      fullScreen: { 
          behavior: ptp.fullScreenButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('fullScreen', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-fullscreen ptp-control-bar-btn', 
              'Full Screen') 
      }, 
      moreOptions: { 
          behavior: ptp.moreOptionsButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('moreOptions', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-more-options ptp-control-bar-btn', 
              'More Options') 
      }, 
      multiView: { 
          behavior: ptp.multiViewButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('multiView', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-multiview ptp-control-bar-btn', 
              'Multi View') 
      }, 
      socialButton: { 
          behavior: ptp.shareVideoButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('shareVideo', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-share-video ptp-control-bar-btn', 
              'Share Video') 
      }, 
      volume: { 
          behavior: ptp.volumeBehavior, 
          element: ptp.factories.simpleDivFactory('volume', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-volume-control ptp-control-bar-btn'), 
          mute: { 
              behavior: ptp.muteButtonBehavior, 
              element: ptp.factories.simpleButtonFactory('mute', ptp.elementGetter('.ptp-volume-control'), 
                  'ptp-control ptp-button-background ptp-btn-volume', 'Mute') 
          }, 
          slider: { 
              behavior: ptp.volumeSliderBehavior, 
              element: ptp.factories.simpleSliderFactory('volumeSlider', ptp.elementGetter('.ptp-volume-control'), 
                  'ptp-control ptp-volume-slider ptp-volume-hidden', 'Volume') 
          } 
      }, 
      pip: { 
          behavior: ptp.pipButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('pip', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-pip ptp-control-bar-btn', 'PIP') 
      }, 
      playPause: { 
          behavior: ptp.playPauseButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('play', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-playpause ptp-control-bar-btn', 
              'Play') 
      }, 
      rewind: { 
          behavior: ptp.rewindButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('rewind', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-rewind ptp-control-bar-btn', 
              'Rewind') 
      }, 
      scrubBar: { 
          element: ptp.factories.simpleDivFactory('scrubBar', ptp.elementGetter('.ptp-control-bar'), 'ptp-scrub-bar'), 
          behavior: ptp.scrubBarBehavior, 
   }, 
    bufferProgressBar: { 
              element: ptp.factories.simpleDivFactory('bufferProgressBar', ptp.elementGetter('.ptp-scrub-bar'), 
                  'ptp-buffer-progress-bar'), 
              behavior: ptp.bufferProgressBarBehavior 
    }, 
      seekToBar: { 
              element: ptp.factories.simpleDivFactory('seekToBar', ptp.elementGetter('.ptp-scrub-bar'), 'ptp-seek-to-bar'), 
              behavior: ptp.seekToBarBehavior 
    }, 
      playbackProgressBar: { 
              element: ptp.factories.simpleDivFactory('playbackProgressBar', ptp.elementGetter('.ptp-scrub-bar'), 
                  'ptp-playback-progress-bar'), 
              behavior: ptp.playProgressBarBehavior 
    }, 
      playHead: { 
              element: ptp.factories.simpleDivFactory('playHead', ptp.elementGetter('.ptp-scrub-bar'), 'ptp-progress-bar-play-head'), 
              behavior: ptp.playHeadBehavior 
    } 
      }, 
      slowRewind: { 
          behavior: ptp.slowRewindButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('slowRewind', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-slowrewind ptp-control-bar-btn', 
              'Slow Rewind'), 
          enabled: true 
   }, 
      slowForward: { 
          behavior: ptp.slowForwardButtonBehavior, 
          element: ptp.factories.simpleButtonFactory('slowForward', ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-button-background ptp-btn-slowforward ptp-control-bar-btn', 
              'Slow Forward') 
      }, 
      spacer: { 
          element: ptp.factories.simpleDivFactory('spacer', ptp.elementGetter('.ptp-control-bar'), 'ptp-fill-spacer') 
      }, 
      trickPlayRateDisplay: { 
          behavior: ptp.trickPlayRateDisplayBehavior, 
          element: ptp.factories.simpleDivFactory('trickPlayDisplay', 
              ptp.elementGetter('.ptp-control-bar'), 
              'ptp-control ptp-btn-control ptp-control-bar-trick-play-rate hidden') 
      } 
  }; 
  var DEFAULT_LOCALIZATION_CONFIG = { 
      locale: 'en-US', 
      behavior: mapLocalizer, 
      localizationMap: { 
          'en-US': { 
              OK: 'Okay', 
              CANCEL: 'Cancel', 
              DEFAULT: 'Default', 
              NONE: 'None', 
              FONT_MONO_W_SERIF: 'Monospaced With Serifs', 
              FONT_PROP_W_SERIF: 'Proportional with Serifs', 
              FONT_MONO_WO_SERIF: 'Monospaced without Serifs', 
              FONT_CASUAL: 'Casual', 
              FONT_CURSIVE: 'Cursive', 
              FONT_SMALL_CAPS: 'Small Capitals', 
              FONT_EDGE_DEFAULT: 'Default', 
              FONT_EDGE_NONE: 'None', 
              FONT_EDGE_RAISED: 'Raised', 
              FONT_EDGE_DEPRESSED: 'Depressed', 
              FONT_EDGE_UNIFORM: 'Uniform', 
              FONT_EDGE_DROP_SHADOW_LEFT: 'Drop Shadow Left', 
              FONT_EDGE_DROP_SHADOW_RIGHT: 'Drop Shadow Right', 
              SIZE_SMALL: 'Small', 
              SIZE_MEDIUM: 'Medium', 
              SIZE_LARGE: 'Large', 
              COLOR_BLACK: 'Black', 
              COLOR_GREY: 'Grey', 
              COLOR_WHITE: 'White', 
              COLOR_BRIGHT_WHITE: 'Bright White', 
              COLOR_DARK_RED: 'Dark Red', 
              COLOR_RED: 'Red', 
              COLOR_BRIGHT_RED: 'Bright Red', 
              COLOR_DARK_GREEN: 'Dark Green', 
              COLOR_GREEN: 'Green', 
              COLOR_BRIGHT_GREEN: 'Bright Green', 
              COLOR_DARK_BLUE: 'Dark Blue', 
              COLOR_BLUE: 'Blue', 
              COLOR_BRIGHT_BLUE: 'Bright Blue', 
              COLOR_DARK_YELLOW: 'Dark Yellow', 
              COLOR_YELLOW: 'Yellow', 
              COLOR_BRIGHT_YELLOW: 'Bright Yellow', 
              COLOR_DARK_MAGENTA: 'Dark Magenta', 
              COLOR_MAGENTA: 'Magenta', 
              COLOR_BRIGHT_MAGENTA: 'Bright Magenta', 
              COLOR_DARK_CYAN: 'Dark Cyan', 
              COLOR_CYAN: 'Cyan', 
              COLOR_BRIGHT_CYAN: 'Bright Cyan', 
              REPLAY: 'Replay', 
              PLAY: 'Play', 
              PAUSE: 'Pause', 
              STOP: 'Stop' 
    } 
      } 
  }; 
  var DEFAULT_AUDIO_TRACK_SELECTION_CONFIG = { 
      behavior: ptp.audioTrackSelectionPanelBehavior, 
      element: ptp.factories.simpleDivFactory('audioTrackSelectionPanel', ptp.elementGetter(selector), 
          'ptp-audio-track-selection-panel hidden'), 
      audioTrackSelectionPanelHeader: { 
          behavior: ptp.audioTrackSelectionPanelHeader, 
          element: ptp.factories.simpleDivFactory('header', ptp.elementGetter('.ptp-audio-track-selection-panel'), 
              'ptp-panel-header ptp-audio-track-selection-header'), 
          audioTrackSelectionPanelCloseButton: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('closeButton', ptp.elementGetter('.ptp-audio-track-selection-header'), 
                  'ptp-control ptp-btn-control ptp-panel-close-btn', 'X') 
          }, 
          audioTrackSelectionPanelTitle: { 
              element: ptp.factories.simpleDivFactory('title', ptp.elementGetter('.ptp-audio-track-selection-header'), 
                  'ptp-panel-title', 'Audio Track') 
          } 
      }, 
      audioTrackSelectionPanelSeparator: { 
          element: ptp.factories.simpleHRFactory('audioTrackSelectionPanelSeparator', 
              ptp.elementGetter('.ptp-audio-track-selection-panel'), 'ptp-hr-separator') 
      }, 
      audioTrackSelectionMenu: { 
          behavior: ptp.audioTrackSelectionMenu, 
          element: ptp.factories.simpleDivFactory('audioTrackSelectionMenu', ptp.elementGetter('.ptp-audio-track-selection-panel'), 
              'ptp-audio-track-selection-menu', 'Menu TBD') 
      } 
  }; 
  
  var DEFAULT_CLOSED_CAPTION_LANGUAGE_PANEL_CONFIG = { 
      behavior: ptp.closedCaptionLanguagePanelBehavior, 
      element: ptp.factories.simpleDivFactory('closedCaptionLanguagePanel', ptp.elementGetter(selector), 
          'ptp-closed-caption-panel hidden ptp-closed-caption-language-panel'), 
      closedCaptionLanguagePanelHeader: { 
          behavior: ptp.closedCaptionLanguagePanelHeader, 
          element: ptp.factories.simpleDivFactory('header', ptp.elementGetter('.ptp-closed-caption-language-panel'), 
              'ptp-panel-header ptp-closed-caption-language-header'), 
          closedCaptionLanguageCloseButton: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('closeButton', ptp.elementGetter('.ptp-closed-caption-language-header'), 
                  'ptp-control ptp-btn-control ptp-panel-close-btn', 'X') 
          }, 
          closedCaptionLanguageTitle: { 
              element: ptp.factories.simpleDivFactory('title', ptp.elementGetter('.ptp-closed-caption-language-header'), 
                  'ptp-panel-title', 'Closed Captions') 
          }, 
          closedCaptionLanguageOptionsButton: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('title', ptp.elementGetter('.ptp-closed-caption-language-header'), 
                  'ptp-closed-caption-options-btn', 'Options') 
          } 
      }, 
      closedCaptionLanguageSeparator: { 
          element: ptp.factories.simpleHRFactory('closedCaptionLanguageSeparator', ptp.elementGetter('.ptp-closed-caption-panel'), 
              'ptp-hr-separator') 
      }, 
      closedCaptionOptions: { 
          behavior: ptp.closedCaptionLanguageMenu, 
          element: ptp.factories.simpleDivFactory('captionLanguageMenu', ptp.elementGetter('.ptp-closed-caption-panel'), 
              'ptp-scroll-bar ptp-closed-caption-language-menu') 
      } 
  }; 
  
  var DEFAULT_CLOSED_CAPTION_OPTIONS_PANEL_CONFIG = { 
      behavior: ptp.closedCaptionOptionsPanelBehavior, 
      element: ptp.factories.simpleDivFactory('closedCaptionOptionsPanel', ptp.elementGetter(selector), 
          'ptp-closed-caption-panel hidden ptp-closed-caption-options-panel'), 
      closedCaptionOptionsHeader: { 
          behavior: ptp.closedCaptionOptionsPanelHeader, 
          element: ptp.factories.simpleDivFactory('closedCaptionOptionsHeader', ptp.elementGetter('.ptp-closed-caption-options-panel'), 
              'ptp-panel-header ptp-closed-caption-options-header'), 
          closedCaptionOptionsCloseButton: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('closedCaptionOptionsCloseButton', 
                  ptp.elementGetter('.ptp-closed-caption-options-header'), 
                  'ptp-control ptp-btn-control ptp-panel-close-btn', '<') 
          }, 
          closedCaptionOptionsTitle: { 
              element: ptp.factories.simpleDivFactory('closedCaptionOptionsTitle', 
                  ptp.elementGetter('.ptp-closed-caption-options-header'), 'ptp-panel-title', 'Closed Captions') 
          }, 
          closedCaptionLanguageDoneButton: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('closedCaptionLanguageDoneButton', 
                  ptp.elementGetter('.ptp-closed-caption-options-header'), 'ptp-closed-caption-done-btn', 'Done') 
          } 
      }, 
      closedCaptionOptionsHeaderSeparator: { 
          element: ptp.factories.simpleHRFactory('closedCaptionOptionsHeaderSeparator', 
              ptp.elementGetter('.ptp-closed-caption-options-panel'), 'ptp-hr-separator') 
      }, 
      closedCaptionOptionsMenu: { 
          behavior: ptp.closedCaptionOptionsMenu, 
          element: ptp.factories.simpleDivFactory('closedCaptionOptionsMenu', ptp.elementGetter('.ptp-closed-caption-options-panel'), 
              'ptp-closed-caption-options-menu'), 
          closedCaptionOptionsMainMenu: { 
              behavior: ptp.closedCaptionOptionsMainMenu, 
              element: ptp.factories.simpleDivFactory('closedCaptionOptionsMainMenu', 
                  ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                  'ptp-scroll-bar ptp-closed-caption-options-main-menu'), 
              closedCaptionOptionsFontStyle: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontStyle', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Font Style') 
              }, 
              closedCaptionOptionsFontSize: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontSize', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Font Size') 
              }, 
              closedCaptionOptionsFontColor: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontColor', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Font Color') 
              }, 
              closedCaptionOptionsFontOpacity: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontOpacity', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Font Opacity') 
              }, 
              closedCaptionOptionsBackgroundColor: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsBackgroundColor', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Background Color') 
              }, 
              closedCaptionOptionsBackgroundOpacity: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsBackgroundOpacity', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Background Opacity') 
              }, 
              closedCaptionOptionsFillColor: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFillColor', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Fill Color') 
              }, 
              closedCaptionOptionsFillOpacity: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFillOpacity', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Fill Opacity') 
              }, 
              closedCaptionOptionsFontEdge: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontEdge', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Stroke Weight') 
              }, 
              closedCaptionOptionsFontEdgeColor: { 
                  behavior: ptp.buttonBehavior, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontEdgeColor', 
                      ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                      'ptp-closed-caption-options-menu-item', 'Stroke Color') 
              } 
          }, 
          closedCaptionOptionsMenuSeparator: { 
              element: ptp.factories.simpleHRFactory('closedCaptionOptionsMenuSeparator', 
                  ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                  'ptp-closed-caption-options-menu-separator') 
          }, 
          closedCaptionOptionsSubMenu: { 
              behavior: ptp.closedCaptionOptionsSubMenu, 
              closedCaptionOptionsFontStyleSubMenu: { 
                  behavior: ptp.verticalListMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontStyleSubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
              }, 
              closedCaptionOptionsFontEdgeSubMenu: { 
                  behavior: ptp.verticalListMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontEdgeSubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
              }, 
              closedCaptionOptionsFontEdgeColorSubMenu: { 
                  behavior: ptp.verticalListMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontEdgeColorSubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
              }, 
              closedCaptionOptionsFontSizeSubMenu: { 
                  behavior: ptp.verticalListMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontSizeSubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
              }, 
              closedCaptionOptionsFontColorSubMenu: { 
                  behavior: ptp.verticalListMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontColorSubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
              }, 
              closedCaptionOptionsFontOpacitySubMenu: { 
                  behavior: ptp.sliderMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontOpacitySubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-closed-caption-options-sub-menu ptp-closed-caption-options-opacity-slider hidden') 
              }, 
              closedCaptionOptionsBackgroundColorSubMenu: { 
                  behavior: ptp.verticalListMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsBackgroundColorSubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
              }, 
              closedCaptionOptionsBackgroundOpacitySubMenu: { 
                  behavior: ptp.sliderMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsBackgroundOpacitySubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-closed-caption-options-sub-menu ptp-closed-caption-options-opacity-slider hidden') 
              }, 
              closedCaptionOptionsFillColorSubMenu: { 
                  behavior: ptp.verticalListMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFillColorSubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
              }, 
              closedCaptionOptionsFillOpacitySubMenu: { 
                  behavior: ptp.sliderMenu, 
                  element: ptp.factories.simpleDivFactory('closedCaptionOptionsFillOpacitySubMenu', 
                      ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                      'ptp-closed-caption-options-sub-menu ptp-closed-caption-options-opacity-slider hidden') 
              } 
          } 
      }, 
      closedCaptionOptionsPreviewSeparator: { 
          element: ptp.factories.simpleHRFactory('closedCaptionOptionsPreviewSeparator', 
              ptp.elementGetter('.ptp-closed-caption-options-panel'), 'ptp-hr-separator') 
      }, 
      closedCaptionPreviewPanel: { 
          behavior: ptp.closedCaptionPreviewPanel, 
          text: 'Sample Captions', 
          element: ptp.factories.simpleDivFactory('closedCaptionPreviewPanel', 
              ptp.elementGetter('.ptp-closed-caption-options-panel'), 
              'ptp-closed-caption-preview-panel', 'Sample Captions') 
      }, 
      closedCaptionOptionsFooterSeparator: { 
          element: ptp.factories.simpleHRFactory('closedCaptionOptionsFooterSeparator', 
              ptp.elementGetter('.ptp-closed-caption-options-panel'), 'ptp-hr-separator') 
      }, 
      closedCaptionOptionsFooter: { 
          behavior: ptp.closedCaptionOptionsFooter, 
          element: ptp.factories.simpleDivFactory('closedCaptionOptionsFooter', 
              ptp.elementGetter('.ptp-closed-caption-options-panel'), 'ptp-closed-caption-options-footer'), 
          closedCaptionOptionsResetButton: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('closedCaptionOptionsResetButton', 
                  ptp.elementGetter('.ptp-closed-caption-options-footer'), 
                  'ptp-closed-caption-options-reset-button', 'Reset to Default') 
          }, 
          closedCaptionOptionsApplyButton: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('closedCaptionOptionsApplyButton', 
                  ptp.elementGetter('.ptp-closed-caption-options-footer'), 
                  'ptp-closed-caption-options-apply-button', 'Apply') 
          } 
      } 
  }; 
  
  var DEFAULT_SHARE_VIDEO_PANEL_CONFIG = { 
      behavior: ptp.shareVideoPanelBehavior, 
      element: ptp.factories.simpleDivFactory('shareVideoPanel', ptp.elementGetter(selector), 'ptp-share-video-panel hidden'), 
      shareVideoPanelHeader: { 
          behavior: ptp.shareVideoPanelHeader, 
          element: ptp.factories.simpleDivFactory('shareVideoPanelHeader', ptp.elementGetter('.ptp-share-video-panel'), 
              'ptp-panel-header ptp-share-video-panel-header'), 
          shareVideoPanelCloseButton: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('shareVideoPanelCloseButton', ptp.elementGetter('.ptp-share-video-panel-header'), 
                  'ptp-control ptp-btn-control ptp-panel-close-btn', 'X') 
          }, 
          shareVideoPanelTitle: { 
              element: ptp.factories.simpleDivFactory('shareVideoPanelTitle', ptp.elementGetter('.ptp-share-video-panel-header'), 
                  'ptp-panel-title', 'Social Share') 
          } 
      }, 
      shareVideoPanelHeaderSeparator: { 
          element: ptp.factories.simpleHRFactory('shareVideoPanelHeaderSeparator', ptp.elementGetter('.ptp-share-video-panel'), 
              'ptp-hr-separator') 
      }, 
      shareVideoPanelMenu: { 
          element: ptp.factories.simpleDivFactory('shareVideoPanelMenu', ptp.elementGetter('.ptp-share-video-panel'), 
              'share-video-panel-menu'), 
          behavior: ptp.shareVideoPanelMenu, 
          shareVideoPanelFacebookBtn: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('shareVideoPanelFacebookBtn', ptp.elementGetter('.share-video-panel-menu'), 
                  'ptp-btn-control ptp-button-background ptp-share-video-panel-menu-item ' + 
                  'ptp-btn-share-video-facebook') 
          }, 
          shareVideoPanelTwitterBtn: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('shareVideoPanelTwitterBtn', ptp.elementGetter('.share-video-panel-menu'), 
                  'ptp-btn-control ptp-button-background ptp-share-video-panel-menu-item ' + 
                  'ptp-btn-share-video-twitter') 
          }, 
          shareVideoPanelGoogleBtn: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('shareVideoPanelGoogleBtn', ptp.elementGetter('.share-video-panel-menu'), 
                  'ptp-btn-control ptp-button-background ptp-share-video-panel-menu-item ' + 
                  'ptp-btn-share-video-google-plus') 
          }, 
          shareVideoPanelLinkedinBtn: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('shareVideoPanelLinkedinBtn', ptp.elementGetter('.share-video-panel-menu'), 
                  'ptp-btn-control ptp-button-background ptp-share-video-panel-menu-item ' + 
                  'ptp-btn-share-video-linkedin') 
          } 
      } 
  }; 
  
  var DEFAULT_MORE_OPTIONS_CONTROL_PANEL_CONFIG = { 
      behavior: ptp.moreOptionsControlPanel, 
      element: ptp.factories.simpleDivFactory('moreOptionsControlPanel', ptp.elementGetter(selector), 
          'ptp-more-options-control-panel hidden'), 
      moreOptionsControlPanelHeader: { 
          behavior: ptp.moreOptionsControlPanelHeader, 
          element: ptp.factories.simpleDivFactory('moreOptionsControlPanelHeader', 
              ptp.elementGetter('.ptp-more-options-control-panel'), 
              'ptp-panel-header ptp-more-options-control-panel-header'), 
          moreOptionsControlPanelCloseButton: { 
              behavior: ptp.buttonBehavior, 
              element: ptp.factories.simpleDivFactory('moreOptionsControlPanelCloseButton', 
                  ptp.elementGetter('.ptp-more-options-control-panel-header'), 
                  'ptp-control ptp-btn-control ptp-panel-close-btn', 'X') 
          }, 
          moreOptionsControlPanelTitle: { 
              element: ptp.factories.simpleDivFactory('moreOptionsPanelTitle', 
                  ptp.elementGetter('.ptp-more-options-control-panel-header'), 
                  'ptp-panel-title', 'Options') 
          } 
      }, 
      moreOptionsPanelHeaderSeparator: { 
          element: ptp.factories.simpleHRFactory('moreOptionsPanelHeaderSeparator', 
              ptp.elementGetter('.ptp-more-options-control-panel'), 
              'ptp-hr-separator') 
      }, 
      moreOptionsPanelMenu: { 
          element: ptp.factories.simpleDivFactory('moreOptionsPanelMenu', 
              ptp.elementGetter('.ptp-more-options-control-panel'), 
              'ptp-more-options-control-panel-menu'), 
          behavior: ptp.moreOptionsControlPanelMenu, 
          audioTrackButton: { 
              behavior: ptp.audioTrackButtonBehavior, 
              element: ptp.factories.simpleButtonFactory('audioTrackBtn', ptp.elementGetter('.ptp-more-options-control-panel-menu'), 
                  'ptp-control ptp-btn-control ptp-button-background ptp-btn-audio-track ' + 
                  'ptp-more-options-control-panel-menu-item ' + 
                  'ptp-more-options-menu-btn', 
                  'Audio Track') 
          }, 
          multiViewButton: { 
              behavior: ptp.multiViewButtonBehavior, 
              element: ptp.factories.simpleButtonFactory('multiView', ptp.elementGetter('.ptp-more-options-control-panel-menu'), 
                  'ptp-control ptp-btn-control ptp-button-background ptp-btn-multiview ' + 
                  'ptp-more-options-control-panel-menu-item ' + 
                  'ptp-more-options-menu-btn', 
                  'Multi View') 
          }, 
          pipButton: { 
              behavior: ptp.pipButtonBehavior, 
              element: ptp.factories.simpleButtonFactory('pip', ptp.elementGetter('.ptp-more-options-control-panel-menu'), 
                  'ptp-control ptp-btn-control ptp-button-background ptp-btn-pip ' + 
                  'ptp-more-options-control-panel-menu-item ' + 
                  'ptp-more-options-menu-btn', 'PIP') 
          }, 
          socialButton: { 
              behavior: ptp.shareVideoButtonBehavior, 
              element: ptp.factories.simpleButtonFactory('shareVideo', ptp.elementGetter('.ptp-more-options-control-panel-menu'), 
                  'ptp-control ptp-btn-control ptp-button-background ptp-btn-share-video ' + 
                  'ptp-more-options-control-panel-menu-item ' + 
                  'ptp-more-options-menu-btn', 
                  'Share Video') 
          } 
      } 
  }; 
  
  SingleViewConfigurationObject = { 
      element: ptp.elementGetter(selector), 
      classNames: 'ptp-root-element', 
      behavior: ptp.singleViewBehavior, 
      logLevel: 0, 
      logOutput: null, 
      player: { 
          element: ptp.factories.simpleDivFactory('videoPlayer', ptp.elementGetter(selector), 
              'ptp-main-video-div-style ptp-background-style'), 
          behavior: ptp.videoBehavior, 
          autoPlay: true, 
          bufferingOverlay: { 
              behavior: ptp.bufferingOverlayBehavior, 
              element: ptp.createDiv('bufferingOverlay', ptp.elementGetter('.ptp-main-video-div-style'), 'ptp-buffering-overlay') 
          }, 
          errorMessagePanel: { 
              behavior: ptp.errorMessagePanelBehavior, 
              element: ptp.createDiv('errorMessagePanel', ptp.elementGetter('.ptp-main-video-div-style'), 'ptp-error-message-panel hidden') 
          }, 
          controlsDisabledInAd: //same as ptp.videoBehavior.setControlsDisabledInAd  
   mediaPlayerItemConfig: //same as ptp.videoBehavior.setMediaPlayerItemConfig  
     abrControlParameters: //same as ptp.videoBehavior.setAbrControlParameters  
    bufferControlParameters: //same as ptp.videoBehavior.setBufferControlParameters  
    ccVisibility: //same as ptp.videoBehavior.setCCVisibility  
     ccStyle: //same as ptp.videoBehavior.setCCStyle  
    mediaResource: //same as ptp.videoBehavior.setMediaResource  
    volume: //same as ptp.videoBehavior.setVolume 
    }, 
  
      pip: { 
          element: ptp.factories.simpleDivFactory('pip', ptp.elementGetter(selector), 'ptp-pip-video-div'), 
              behavior: ptp.videoBehavior, 
              bufferingOverlay: { 
              behavior: ptp.bufferingOverlayBehavior, 
                  element: ptp.createDiv('bufferingOverlay', ptp.elementGetter('.ptp-pip-video-div'), 'ptp-buffering-overlay') 
          }, 
          errorMessagePanel: { 
              behavior: ptp.errorMessagePanelBehavior, 
                  element: ptp.createDiv('errorMessagePanel', ptp.elementGetter('.ptp-pip-video-div'), 'ptp-error-message-panel hidden') 
          }, 
          autoPlay: false 
    }, 
      localization: DEFAULT_LOCALIZATION_CONFIG, 
      controlBar: DEFAULT_CONTROL_BAR_CONFIG, 
      audioTrackSelectionPanel: DEFAULT_AUDIO_TRACK_SELECTION_CONFIG, 
      closedCaptionLanguagePanel: DEFAULT_CLOSED_CAPTION_LANGUAGE_PANEL_CONFIG, 
      closedCaptionOptionsPanel: DEFAULT_CLOSED_CAPTION_OPTIONS_PANEL_CONFIG, 
      moreOptionsControlPanel: DEFAULT_MORE_OPTIONS_CONTROL_PANEL_CONFIG, 
      shareVideoPanel: DEFAULT_SHARE_VIDEO_PANEL_CONFIG 
  }; 
  
  MultiViewConfigurationObject = { 
      element: ptp.elementGetter(selector), 
      classNames: 'ptp-root-element', 
      behavior: ptp.multiViewBehavior, 
      logLevel: 0, 
      logOutput: null, 
      multiVideoHolder: { 
          element: ptp.factories.simpleDivFactory('multiViewPlayer', ptp.elementGetter(selector), 'ptp-multi-view-container') 
      }, 
      views: [ 
          { 
              player: {} // see in SingleViewConfigurationObject above 
    } 
      ], 
      localization: DEFAULT_LOCALIZATION_CONFIG, 
      controlBar: DEFAULT_CONTROL_BAR_CONFIG, 
      audioTrackSelectionPanel: DEFAULT_AUDIO_TRACK_SELECTION_CONFIG, 
      closedCaptionLanguagePanel: DEFAULT_CLOSED_CAPTION_LANGUAGE_PANEL_CONFIG, 
      closedCaptionOptionsPanel: DEFAULT_CLOSED_CAPTION_OPTIONS_PANEL_CONFIG, 
      moreOptionsControlPanel: DEFAULT_MORE_OPTIONS_CONTROL_PANEL_CONFIG, 
      shareVideoPanel: DEFAULT_SHARE_VIDEO_PANEL_CONFIG 
  };
  ```

* **協助程式建構** 此建構包含下列專案：

   * **工廠** 若要建立視覺元素，您可以使用 `ptp.factories.simpleButtonFactory`， `ptp.factories.simpleDivFactory`， `ptp.factories.simpleHRFactory`、和 `ptp.factories.simpleSliderFactory`. 如需詳細資訊，請參閱 [UI框架](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/index.html) API檔案。

   * **Mixin** Mixin是可撰寫的模組，可以在行為中撰寫以使用通用建構。 例如，許多元件希望瞭解可能影響其行為的變更，例如播放廣告時的變更。 所有這些元素都會新增 `adBreak` 類別。

     以下是如何實作內建mixin的範例 `adBreakStyling`：

     ```js
     adBreakStyling = function (element, player) { 
         ... 
         ... 
         return composable().compose({ 
             init: init, 
             manageAdBreakStyle: manageAdBreakStyle 
      }); 
     }
     ```

     以下為行為如何使用此Mixin：

     ```js
     customBehavior = function (element, configuration, player) { 
         var api = 
             component(element, configuration, player, clickHandler).compose( 
                 adBreakStyling(element, player).compose({ 
                     init: init, 
                 })); 
         return api; 
     }
     ```

     現在 `customBehavior` 可以使用以下程式所公開的所有方法： `adBreakStyling`，在此範例中為 `manageAdBreakStyle`. 另一個使用案例是當mixin可以新增事件接聽程式時，而在處理常式中，mixin可以以某種方式修改元素。 隨後，使用此mixin的元件將自動擁有此功能。

   * **Utils** 某些公用程式，例如 `ptp.elementGetter`，用於設定區段和 `ptp.deepmerge`，可協助您撰寫或擴充行為指令。 如需詳細資訊，請參閱 [UI框架](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/index.html) API檔案。
