---
description: TVSDK可以播放具有多個具有不同比特率的配置檔案的視頻，在它們之間切換以基於可用頻寬提供多個質量級別。
title: 多比特率
exl-id: 5f71d69e-993a-4985-accd-7ce2104f837e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# 多比特率 {#multiple-bit-rates}

TVSDK可以播放具有多個具有不同比特率的配置檔案的視頻，在它們之間切換以基於可用頻寬提供多個質量級別。

可以設定初始、最小和最大比特率，以及多比特率(MBR)流的自適應比特率(ABR)切換策略。 TVSDK自動切換到在指定配置內提供最佳回放體驗的比特率。

參考實現在中配置以下ABR參數 [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html)。

| 參數 | 說明 |
|--- |--- |
| 初始比特率：getABRInitialBitRate | 第一段的所需重放比特率（以位/秒為單位）。 當播放開始時，最接近的輪廓（等於或大於初始比特率）用於第一段。  如果定義了最小比特率並且初始比特率低於最小比特率，則TVSDK選擇具有高於最小比特率的最低比特率的簡檔。 同樣，如果初始速率高於最大速率，TVSDK將選擇低於最大速率的最高速率。 如果初始比特率為零或未定義，則初始比特率由ABR策略確定。  返回表示每秒位元組配置檔案的整數值。 |
| 最小比特率：getABRMinBitRate | ABR可切換到的最低允許比特率。 ABR切換忽略比此速率低的配置檔案。 返回表示每秒位配置檔案的整數值。 |
| 最大比特率：getABRMaxBitRate | ABR可切換到的最高允許比特率。 ABR切換忽略比此速率更高的配置檔案。 返回表示每秒位配置檔案的整數值。 |
| ABR切換策略：getABRPolicy | 如果可能，回放將逐漸切換到最高比特率簡檔。 您可以設定ABR切換策略，該策略確定TVSDK在配置檔案之間切換的速度。 預設值為「中等」。 <ul><li>*保守*:當頻寬比當前比特率高50%時，切換到具有下一個更高比特率的配置式。 </li><li>*中等*:當頻寬比當前比特率高20%時，切換到下一個更高的比特率配置檔案。</li><li>*攻擊性*:當頻寬高於當前比特率時，立即切換到最高比特率配置檔案</li></ul><br/>如果初始比特率為零或未指定，並且指定了策略，則回放從Conserval的最低比特率配置檔案開始，該配置檔案最接近中等可用配置檔案的中位數比特率，以及Accive的最高比特率配置檔案。<br/><br/>策略在最小和最大比特率的約束範圍內工作（如果已指定）。  從ABRControlParameters枚舉返回當前設定： <ul><li>ABR_CONSERVAL</li><li>ABR(_M) </li><li>ABR_ACCIVE</li></ul><br>另請參閱 [ABRP策略](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/ABRControlParameters.ABRPolicy.html)。 |

>[!NOTE]
>
>* TVSDK故障轉移機制可能會覆蓋這些設定，因為TVSDK傾向於持續的回放體驗，而不是嚴格遵守控制參數。
>* 當比特率更改時，TVSDK派單 `onProfileChanged` 事件 `PlaybackEventListener`。


## 在參考實現中啟用自定義ABR控制 {#section_72A6E7263E1441DD8D7E0690285515E6}

預設情況下，TVSDK中啟用了自適應比特率(ABR)。 通過配置自定義ABR控制項，可以使用黃金時段設定用戶介面覆蓋引用實現中的預設TVSDK行為。

要通過「設定」用戶介面啟用自定義ABR:

* 開啟「黃金時段設定」對話框。
* 選擇 **[!UICONTROL ABR controls]**。

   ![](assets/abr-configuration.jpg)

* 點擊 [!UICONTROL Enable ON] 控制，以便顯示 `OFF`。

的 `PlaybackManager` 僅在 [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) 返回true(ON)。 如果返回false(OFF)，則 `PlaybackManager` 使用預設ABR控制項，使初始、最小和最大比特率都為0,ABR策略為 `ABR_MODERATE`。

## 配置低比特率 {#section_5451691CBBD24542AD54A474D222CD39}

對於某些低比特率的播放速率，TVSDK預設情況下會切換到僅音頻流，並且播放會顯示為凍結。 您可以配置播放器，使其永遠不會遇到切換為僅音頻的情況。

* 實施 [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) 介面：

* 確保 [getABRMinBitRate](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#getABRMinBitRate()) 高於僅音頻比特率（高於64000）。
* 確保 [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#isABRControlEnabled()) 開啟。
