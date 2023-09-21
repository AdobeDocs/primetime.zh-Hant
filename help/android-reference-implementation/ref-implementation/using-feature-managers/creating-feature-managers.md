---
description: TVSDK功能由設定驅動，並透過MediaPlayer實作。
title: 將設定資訊傳遞至MediaPlayer以建立功能管理員
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# 將設定資訊傳遞至MediaPlayer以建立功能管理員 {#creating-feature-managers-by-passing-configuration-information-to-the-mediaplayer}

TVSDK功能由設定驅動，並透過MediaPlayer實作。

* 組態是功能的特定設定清單，例如ABR控制項的初始位元速率和預設隱藏式字幕可見度。

  功能管理員需要取得設定才能判斷功能行為。

  在Primetime參考實作中，設定會儲存在共用的偏好設定中，但您可以對環境採用任何合適的方式儲存設定。

* `MediaPlayer` 是包含視訊資源的TVSDK媒體播放器物件。

  功能管理員會將TVSDK事件接聽程式註冊至此播放器物件、從播放工作階段擷取資料，並觸發播放工作階段的TVSDK功能。

每個功能都有對應的設定介面。 例如， `CCManager` 使用 `ICCConfig` 以擷取組態。 `ICCConfig` 包含僅取得隱藏式字幕相關設定資訊的方法。

下列範例顯示 [!DNL ICCConfig.java] 檔案，設定為接收隱藏式字幕可見度、字型樣式和字型邊緣的相關資訊。 `MediaPlayer`：

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

使用TVSDK功能的應用程式可透過設定提供者和 `MediaPlayer` 物件。 例如：

```java
// This application needs to use the advertising workflow feature 
AdsManager adsManager = new AdsManagerOn();
```

功能管理員設定API檔案： [Javadoc](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html)
