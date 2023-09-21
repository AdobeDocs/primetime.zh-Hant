---
description: TVSDK可播放具有多個設定檔且位元速率不同的影片，還可切換視訊，根據可用頻寬提供多個品質等級。
title: 多位元速率
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# 多位元速率 {#multiple-bit-rates}

TVSDK可播放具有多個設定檔且位元速率不同的影片，還可切換視訊，根據可用頻寬提供多個品質等級。

您可以為多位元速率(MBR)資料流設定初始、最小和最大位元速率，以及最適化位元速率(ABR)切換原則。 TVSDK會自動切換為位元速率，在指定的設定中提供最佳播放體驗。

參考實作會在中設定下列ABR引數 [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html).

| 引數 | 說明 |
|--- |--- |
| 初始位元速率： getABRIinitialBitRate | 第一個區段的所需播放位元速率（每秒位元數）。 當播放開始時，最接近的輪廓（等於或大於初始位元速率）會用於第一個區段。  如果已定義最低位元速率，且初始位元速率低於最低位元速率，TVSDK會選取最低位元速率高於最低位元速率的設定檔。 同樣地，如果初始速率高於最大速率，TVSDK會選取低於最大速率的最高速率。 如果初始位元速率為零或未定義，則初始位元速率由ABR原則決定。  傳回代表每秒位元組設定檔的整數值。 |
| 最低位元速率： getABRMinBitRate | ABR可切換的最低允許位元速率。 ABR切換會忽略位元速率低於此的設定檔。 傳回代表每秒位元設定檔的整數值。 |
| 最大位元速率： getABRMaxBitRate | ABR可切換的最高允許位元速率。 ABR切換會忽略位元速率高於此的設定檔。 傳回代表每秒位元設定檔的整數值。 |
| ABR切換原則： getABRPolicy | 播放會儘可能逐漸切換至最高位元速率設定檔。 您可以設定ABR切換原則，以決定TVSDK在設定檔之間切換的速度。 預設值為「稽核」。 <ul><li>*保守*：當頻寬比目前的位元速率高50%時，切換至具有更高位元速率的設定檔。 </li><li>*稽核*：當頻寬比目前的位元速率高20%時，切換到下一個較高的位元速率設定檔。</li><li>*積極進取*：當頻寬高於目前的位元速率時，立即切換至最高位元速率設定檔</li></ul><br/>如果初始位元速率為零或未指定，且已指定原則，則播放會從「保守」的最低位元速率設定檔、「中等」最接近可用設定檔的中位元速率的設定檔，以及「積極」的最高位元速率設定檔開始。<br/><br/>原則會在最小和最大位元速率（如果已指定）的限制內運作。  從ABRControlParameters列舉傳回目前設定： <ul><li>ABR_CONSERVATIVE</li><li>ABR_MODERATE </li><li>ABR_AGGRESSIVE</li></ul><br>另請參閱 [ABRPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/ABRControlParameters.ABRPolicy.html). |

>[!NOTE]
>
>* TVSDK容錯移轉機制可能會覆寫這些設定，因為TVSDK偏好持續播放體驗，而非嚴格遵守控制引數。
>* 當位元速率變更時，TVSDK會傳送 `onProfileChanged` 中的事件 `PlaybackEventListener`.

## 在參考實作中啟用自訂ABR控制 {#section_72A6E7263E1441DD8D7E0690285515E6}

TVSDK預設會啟用最適化位元速率(ABR)。 您可以藉由設定自訂ABR控制項，使用Primetime設定使用者介面來覆寫參考實作中的預設TVSDK行為。

若要透過「設定」使用者介面啟用自訂ABR：

* 開啟Primetime設定對話方塊。
* 選取 **[!UICONTROL ABR controls]**.

  ![](assets/abr-configuration.jpg)

* 點選 [!UICONTROL Enable ON] 控制，使其顯示 `OFF`.

此 `PlaybackManager` 僅在下列情況下設定ABR引數 [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) 傳回true （開啟）。 如果傳回false （關閉），則 `PlaybackManager` 使用預設的ABR控制，所以初始、最小和最大位元速率都將為0，而ABR原則將為 `ABR_MODERATE`.

## 針對低位元速率進行設定 {#section_5451691CBBD24542AD54A474D222CD39}

對於某些低位元速率播放速率，TVSDK預設會切換為僅限音訊的資料流，且播放會顯示為凍結狀態。 您可以設定播放器，讓播放器絕不會切換為僅限音訊。

* 實作 [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) 介面：

* 確定 [getABRMinBitrate](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#getABRMinBitRate()) 高於純音訊位元速率(高於64000)。
* 確定 [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#isABRControlEnabled()) 已開啟。
