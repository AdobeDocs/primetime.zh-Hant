---
keywords: 創意選取規則；AdobeTVSDKConfig
title: 套用創意選取規則
description: 套用創意選取規則
copied-description: true
exl-id: 7918e58d-7783-403c-a12c-8982b26a1555
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# 套用創意選取規則 {#apply-creative-selection-rules}

TVSDK會以下列方式套用創意選取規則：

* TVSDK適用於所有 `default` 規則優先，然後是區域特定規則。
* TVSDK會忽略任何未針對目前區域ID定義的規則。
* 一旦TVSDK套用預設規則，區域特定規則即可根據 `host` （網域）相符的內容出自以下使用者選取的創意： `default` 規則。

* 在隨附的範例規則檔案中，一旦TVSDK套用 `default` 規則(如果M3U8創意網域不包含 [!DNL my.domain.com] 或 [!DNL a.bcd.com] 廣告區域為 `1234`，會重新排序創意，並先播放FlashVPAID創意（如果可用）。 否則會播放MP4廣告，依此類推，一直到JavaScript。

* 如果選取廣告創意，TVSDK無法原生播放( [!DNL .mp4]， [!DNL .flv]等)，TVSDK會發出重新封裝要求。

請注意，可由TVSDK處理的廣告型別仍需透過以下方式定義： `validMimeTypes` 設定於 `AuditudeSettings`.
