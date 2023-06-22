---
description: Audio Codec 3 (AC-3，也稱為Dolby Digital®) 5.1格式可讓內容提供者壓縮多聲道音訊檔案的大小，而不會影響音質。 AC-3是5.1格式，這表示它提供五個全頻寬通道，以提供更豐富的使用者體驗。
title: AC-3 5.1格式
exl-id: 16647d69-9cb4-4bb8-8ad9-cac8811ea66d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# AC-3 5.1格式 {#ac-format}

Audio Codec 3 (AC-3，也稱為Dolby Digital®) 5.1格式可讓內容提供者壓縮多聲道音訊檔案的大小，而不會影響音質。 AC-3是5.1格式，這表示它提供五個全頻寬通道，以提供更豐富的使用者體驗。

如需詳細資訊，請參閱 [Dolby Digital 5.1](https://www.dolby.com/us/en/technologies/dolby-digital.html).

TVSDK支援下列AC-3 5.1功能：

* AC-3環繞音訊
* 環繞音訊型別的混合/非混合串流
* 能夠查詢裝置，以檢視裝置上是否有環繞音訊轉碼器。

   結果會決定選取哪一種偏好的音訊轉碼器型別。 裝置將不會使用的具有音訊轉碼器型別的資訊清單會遭到捨棄。 例如，如果已選取AC-3格式，則不會考慮具有進階音訊編碼(AAC)格式的設定檔。
* 直通模式

   在直通模式中，不是將媒體從AC-3 5.1格式解碼成多通道脈衝碼調制(PCM)格式，而是由「解碼器」修改或未修改（視裝置而定） Dolby媒體。 此媒體會傳送至音訊裝置（喇叭或接收器），讓音訊裝置可以解碼並播放Dolby環繞串流。

>[!IMPORTANT]
>
>TVSDK僅支援Amazon Fire TV第1代裝置上的AC-3 5.1功能。

不支援下列AC-3 5.1功能：

* 多聲道AAC音訊
* 不同轉碼器的ABR (AAC - AC3)

## 選取支援的媒體 {#section_0D7E717BE18B418D817EE017EF2375D1}

以下是TVSDK找到包含AC-3和AAC媒體的資訊清單時發生的典型工作流程：

1. TVSDK會查詢裝置可支援的轉碼器。
1. 會選取品質較高的轉碼器。

   以下是選取品質的順序：

   1. AC-3
   1. AAC

1. TVSDK會忽略其他音訊轉碼器型別的設定檔。

>[!TIP]
>
>應用程式無法取得已忽略設定檔的相關資訊。

## 決定輸出模式 {#section_D2AFBF33D3904AC2A7C653A60C3A0CD3}

處理AC-3媒體時，如果Android裝置已連線至喇叭系統，則以環繞模式或立體聲模式播放內容的決定取決於裝置的設定方式。

|  | 環繞音效 | 立體聲喇叭 |
|---|---|---|
| 裝置設定Dolby on （或auto） | 裝置設定Dolby on （或auto） | 立體聲模式 |
| 裝置設定Dolby off | 立體聲模式 | 立體聲模式 |
