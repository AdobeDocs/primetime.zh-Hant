---
description: 音訊轉碼器3（AC-3，又稱為Dolby Digital®）5.1格式可讓內容供應商壓縮多聲道音訊檔案的大小，而不會影響音效品質。 AC-3是5.1格式，這表示它提供5個全頻寬頻道，以提供更豐富的使用體驗。
seo-description: 音訊轉碼器3（AC-3，又稱為Dolby Digital®）5.1格式可讓內容供應商壓縮多聲道音訊檔案的大小，而不會影響音效品質。 AC-3是5.1格式，這表示它提供5個全頻寬頻道，以提供更豐富的使用體驗。
seo-title: AC-3 5.1格式
title: AC-3 5.1格式
uuid: 9d1adf33-4c9b-4d31-8212-ac301f3e44c5
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---


# AC-3 5.1格式{#ac-format}

音訊轉碼器3（AC-3，又稱為Dolby Digital®）5.1格式可讓內容供應商壓縮多聲道音訊檔案的大小，而不會影響音效品質。 AC-3是5.1格式，這表示它提供5個全頻寬頻道，以提供更豐富的使用體驗。

如需詳細資訊，請參閱[Dolby Digital 5.1](https://www.dolby.com/us/en/technologies/dolby-digital.html)。

TVSDK支援下列AC-3 5.1功能：

* AC-3環繞音效
* 用於環繞音效類型的混合／非混合串流
* 能夠查詢裝置，以查看裝置上是否提供環繞音訊codec。

   結果會決定選取的是哪一種偏好的音訊轉碼器類型。 會捨棄具有音訊codec類型且裝置不會使用的資訊清單。 例如，如果已選取AC-3格式，則不會考慮使用進階音訊編碼(AAC)格式的描述檔。
* 直通模式

   在直通模式下，TVSDK不會將媒體從AC-3 5.1格式解碼為多頻道脈衝碼調制(PCM)格式，而是會從解碼器修改或未修改（視裝置而定）杜比媒體。 該媒體被發送到音頻設備（揚聲器或接收器），以便音頻設備能夠解碼並播放杜比環繞串流。

>[!IMPORTANT]
>
>TVSDK僅支援Amazon Fire TV第1代裝置上的AC-3 5.1功能。

不支援下列AC-3 5.1功能：

* 多聲道AAC音訊
* 跨不同轉碼器的ABR(AAC - AC3)

## 選擇支援的介質{#section_0D7E717BE18B418D817EE017EF2375D1}

以下是TVSDK找到包含AC-3和AAC媒體的資訊清單時所發生的典型工作流程：

1. TVSDK會查詢裝置可支援的轉碼器。
1. 選擇了具有較高質量的編解碼器。

   以下是選取品質的順序：

   1. AC-3
   1. AAC

1. TVSDK會忽略其他音訊轉碼器類型的描述檔。

>[!TIP]
>
>應用程式無法取得有關已忽略描述檔的資訊。

## 確定輸出模式{#section_D2AFBF33D3904AC2A7C653A60C3A0CD3}

在處理AC-3媒體時，如果Android裝置已連接至喇叭系統，則決定以環繞模式或立體聲模式播放內容取決於裝置的設定方式。

|  | **環繞音效** | **立體聲揚聲器** |
|---|---|---|
| 裝置設定Dolby on（或自動） | 裝置設定Dolby on（或自動） | 立體聲模式 |
| 設備配置Dolby off | 立體聲模式 | 立體聲模式 |