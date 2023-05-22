---
description: TVSDK功能由配置驅動，並通過MediaPlayer實現。
title: 通過將配置資訊傳遞給MediaPlayer建立功能管理器
exl-id: 47377ceb-ed3e-4dca-9b55-82e4fe6b0194
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# 通過將配置資訊傳遞給MediaPlayer建立功能管理器 {#creating-feature-managers-by-passing-configuration-information-to-the-mediaplayer}

TVSDK功能由配置驅動，並通過MediaPlayer實現。

* 配置是功能的特定設定清單，如ABR控制項的初始比特率和預設的隱藏字幕可見性。

   功能管理器需要獲取配置以確定功能行為。

   在黃金時段參考實現中，配置儲存在共用首選項中，但您可以以任何對您的環境有意義的方式儲存配置。

* `MediaPlayer` 是包含視頻資源的TVSDK媒體播放器對象。

   功能管理器將TVSDK事件偵聽器註冊到此播放器對象，從回放會話中檢索資料並將TVSDK功能觸發到回放會話。

每個特徵都具有相應的配置介面。 比如說， `CCManager` 使用 `ICCConfig` 來獲取配置。 `ICCConfig` 包含僅獲取與關閉字幕相關的配置資訊的方法。

以下示例顯示 [!DNL ICCConfig.java] 檔案，配置為從中接收有關隱藏標題可見性、字型樣式和字型邊緣的資訊 `MediaPlayer`:

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

使用TVSDK功能的應用程式可以使用配置提供程式和 `MediaPlayer` 的雙曲餘切值。 例如：

```java
// This application needs to use the advertising workflow feature 
AdsManager adsManager = new AdsManagerOn();
```

功能管理器配置API文檔： [Javadoc](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html)
