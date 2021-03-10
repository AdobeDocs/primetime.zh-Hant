---
description: TVSDK可播放具有不同位元速率之多個描述檔的視訊，並根據可用頻寬在視訊間切換，以提供多個品質等級。
title: 多位元速率
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---


# 多位元速率{#multiple-bit-rates}

TVSDK可播放具有不同位元速率之多個描述檔的視訊，並根據可用頻寬在視訊間切換，以提供多個品質等級。

您可以為多位速率(MBR)串流設定初始、最小和最大位速率，以及自適應位速率(ABR)切換策略。 TVSDK會自動切換至位元速率，以在指定組態內提供最佳播放體驗。

參考實現在[IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html)中配置以下ABR參數。

| 參數 | 說明 |
|--- |--- |
| 初始位元速率： getABRInitialBitRate | 第一段的所需播放位速率（以位／秒為單位）。 當播放開始時，第一個區段會使用最接近的描述檔（等於或大於初始位元速率）。  如果定義了最小位元速率且初始位元速率低於最小位元速率，則TVSDK會選擇位元速率低於最小位元速率的描述檔。 同樣地，如果初始速率高於最大速率，TVSDK會選取最高速率低於最大速率。 如果初始比特率為零或未定義，則初始比特率由ABR策略確定。  傳回代表每秒位元組描述檔的整數值。 |
| 最低位元速率： getABRMinBitRate | ABR可切換至的最低允許位速率。 ABR切換會忽略位元速率低於此速率的描述檔。 傳回代表每秒位元描述檔的整數值。 |
| 最大位速率： getABRMaxBitRate | ABR可切換的最高允許位速率。 ABR切換會忽略位元速率高於此速率的描述檔。 傳回代表每秒位元描述檔的整數值。 |
| ABR交換策略： getABRPolicy | 如果可能，回放會逐漸切換到最高比特率配置檔案。 您可以設定ABR切換的原則，此原則會決定TVSDK在設定檔之間切換的速度。 預設值為「協調」。 <ul><li>*保守*:當頻寬比當前位速率高50%時，切換到具有下一個較高位速率的配置檔案。 </li><li>*協調*:當頻寬比當前位速率高20%時，切換到下一個較高的位速率配置檔案。</li><li>*咄咄逼人*:當頻寬高於當前位速率時，立即切換到最高位速率配置檔案</li></ul><br/>如果初始位元速率為零或未指定並指定原則，則播放會從Consurative的最低位元速率描述檔、Moderate的最接近可用描述檔中位數位元速率的描述檔，以及Accorsive的最高位元速率描述檔開始。<br/><br/>如果指定了最小和最大比特率，則該策略在這些速率的限制內工作。從ABRControlParameters列舉傳回目前設定： <ul><li>ABR_CONSERVACY</li><li>ABR_MODERATE </li><li>ABR_ACCORPISE</li></ul><br>另請參 [閱ABRPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/ABRControlParameters.ABRPolicy.html)。 |

>[!NOTE]
>
>* TVSDK容錯機制可能會覆寫這些設定，因為TVSDK偏好持續播放體驗，而非嚴格遵循控制參數。
>* 當位速率改變時，TVSDK會在`PlaybackEventListener`中調度`onProfileChanged`事件。


## 在參考實施{#section_72A6E7263E1441DD8D7E0690285515E6}中啟用自訂ABR控制

預設會在TVSDK中啟用最適化位元速率(ABR)。 您可以使用「Primetime設定」使用者介面，設定自訂ABR控制項，以覆寫參考實作中的預設TVSDK行為。

若要透過「設定」使用者介面啟用自訂ABR:

* 開啟「Primetime設定」對話方塊。
* 選擇&#x200B;**[!UICONTROL ABR controls]**。

   ![](assets/abr-configuration.jpg)

* 點選[!UICONTROL Enable ON]控制項，以顯示`OFF`。

`PlaybackManager`僅在[isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html)返回true(ON)時設定ABR參數。 如果返回false(OFF),`PlaybackManager`使用預設的ABR控制，因此初始、最小和最大位速率都將為0，而ABR策略將為`ABR_MODERATE`。

## 配置低位速率{#section_5451691CBBD24542AD54A474D222CD39}

對於某些低位元速率的播放速率，依預設，TVSDK會切換至僅限音訊的串流，而播放會顯示為凍結。 您可以設定播放器，使它不會遇到切換為僅限音訊的情況。

* 實作[IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html)介面：

* 請確定[getABRMinBitRate](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#getABRMinBitRate())高於僅音訊位元速率（高於64000）。
* 確保[isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#isABRControlEnabled())已開啟。