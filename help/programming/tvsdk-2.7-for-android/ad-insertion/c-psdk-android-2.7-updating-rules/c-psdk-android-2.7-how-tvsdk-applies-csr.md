---
description: 'null'
keywords: creative selection rules;AdobeTVSDKConfig
seo-description: 'null'
seo-title: 套用創意選擇規則
title: 套用創意選擇規則
uuid: 75109483-ea60-43a8-92e7-4bcba48986bc
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 套用創意選擇規則 {#apply-creative-selection-rules}

TVSDK以下列方式套用創意選擇規則：

* TVSDK會先套 `default` 用所有規則，接著是區域特定規則。
* TVSDK會忽略未為目前區域ID定義的任何規則。
* 一旦TVSDK套用預設規則，區域特定規則就可以根據規則所選取的創意素材，進一步變更創意優先 `host``default` 順序。

* 在內含的範例規則檔案中，當TVSDK套用規則後，如果M3U8創意網域不包含 `default`[!DNL my.domain.com] 或廣告區域為 [!DNL a.bcd.com]`1234`，則會重新排序創意素材，而Flash VPAID創意素材會先播放（如果有的話）。 否則會播放MP4廣告，依此類推。

* 如果選取TVSDK無法原生播放的廣告創 [!DNL .mp4]意 [!DNL .flv]素材（、等）,TVSDK會發出重新封裝請求。

請注意，TVSDK可處理的廣告類型仍會透過中的設定 `validMimeTypes` 定義 `AuditudeSettings`。

<!-- 

In Android 2.5 API docs, I see a 
<span class="codeph"> setValidMimeTypes</span> but not a 
<span class="codeph"> getValidMimeTypes</span>.

 -->

