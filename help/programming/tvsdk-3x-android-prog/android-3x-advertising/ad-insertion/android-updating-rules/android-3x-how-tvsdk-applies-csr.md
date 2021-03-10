---
keywords: 創意選擇規則；AdobeTVSDKonfig
title: 套用創意選擇規則
description: 套用創意選擇規則
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# 套用創意選擇規則{#apply-creative-selection-rules}

TVSDK以下列方式套用創意選擇規則：

* TVSDK會先套用所有`default`規則，接著是區域特定規則。
* TVSDK會忽略未為目前區域ID定義的任何規則。
* 一旦TVSDK套用預設規則，區域特定規則就可以根據`default`規則所選取之創作符合的`host`（網域），進一步變更創意優先順序。

* 在內含的範例規則檔案中，當TVSDK套用`default`規則後，如果M3U8創意網域不包含`my.domain.com`或`a.bcd.com`且廣告區域為`1234`，則會重新排序創意素材，而FlashVPAID創意素材會先播放（如果有的話）。 否則會播放MP4廣告，依此類推。

* 如果選取TVSDK無法原生播放的廣告創意素材（[!DNL .mp4]、[!DNL .flv]等）,TVSDK會發出重新封裝請求。

請注意，TVSDK可處理的廣告類型仍透過`AuditudeSettings`中的`validMimeTypes`設定來定義。

<!-- 

In Android 2.5 API docs, I see a 
<span class="codeph"> setValidMimeTypes</span> but not a 
<span class="codeph"> getValidMimeTypes</span>.

 -->

