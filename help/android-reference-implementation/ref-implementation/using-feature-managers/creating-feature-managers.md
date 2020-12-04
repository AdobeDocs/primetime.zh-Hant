---
description: TVSDK功能由設定驅動，並透過MediaPlayer實作。
seo-description: TVSDK功能由設定驅動，並透過MediaPlayer實作。
seo-title: 將設定資訊傳遞至MediaPlayer以建立功能管理員
title: 將設定資訊傳遞至MediaPlayer以建立功能管理員
uuid: 106ececd-a670-4360-b000-a31fec65233c
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# 將設定資訊傳遞至MediaPlayer {#creating-feature-managers-by-passing-configuration-information-to-the-mediaplayer}以建立功能管理員

TVSDK功能由設定驅動，並透過MediaPlayer實作。

* 設定是特定功能設定的清單，例如ABR控制項的初始位元速率和預設的隱藏字幕可見度。

   功能管理員需要取得設定，才能判斷功能行為。

   在Primetime參考實作中，設定會儲存在共用偏好設定中，但您可以以適合您環境的方式儲存設定。

* `MediaPlayer` 是包含視訊資源的TVSDK媒體播放器物件。

   功能管理員將TVSDK事件偵聽器註冊至此播放器物件、從播放工作階段擷取資料，並觸發TVSDK功能至播放工作階段。

每個特徵都具有相應的配置介面。 例如，`CCManager`使用`ICCConfig`來檢索配置。 `ICCConfig` 包含僅獲取與隱藏字幕相關的配置資訊的方法。

下列範例顯示[!DNL ICCConfig.java]檔案，其設定是從`MediaPlayer`接收有關隱藏字幕可見性、字型樣式和字型邊緣的資訊：

```java
// Constructor of CCManager 
 
<b>public CCManager(ICCConfig ccConfig, MediaPlayer mediaPlayer) {...}</b> 
  
// ICCConfig methods 
 
<b>public interface ICCConfig {</b> 
  
    /** 
     * Get the closed captioning visibility config 
     * 
     * @return true if visibility is set to true, false otherwise 
     */ 
    
<b> public boolean getCCVisibility();</b> 
  
    /** 
     * Get the closed captioning font style 
     * 
     * @return TextFormat.Font object represents font style 
     */ 
     
<b>public TextFormat.Font getCCFont();</b>

    /** 
     * Get the closed captioning font edge 
     * 
     * @return TextFormat.FontEdge represents of font edge 
     */ 
     
<b>public TextFormat.FontEdge getCCFontEdge();</b> 
... 
}
```

使用TVSDK功能的應用程式可建立其功能管理員，其中包含組態提供者和`MediaPlayer`物件。 例如：

```java
// This application needs to use the advertising workflow feature 
AdsManager adsManager = new AdsManagerOn();
```

功能管理器配置API檔案：[Javadoc](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html)