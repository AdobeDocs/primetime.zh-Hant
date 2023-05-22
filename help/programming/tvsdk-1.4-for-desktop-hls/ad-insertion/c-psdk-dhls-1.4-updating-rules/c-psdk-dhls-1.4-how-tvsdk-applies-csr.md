---
title: 應用創意選擇規則
description: 應用創意選擇規則
copied-description: true
exl-id: 756de2e8-ffd0-46f6-9ebc-27e52c5c7b74
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# 應用創意選擇規則{#applying-creative-selection-rules}

TVSDK通過以下方式應用創意選擇規則：

* TVSDK應用所有 `default` 首先是規則，然後是特定區域的規則。
* TVSDK忽略未為當前區域ID定義的任何規則。
* 一旦TVSDK應用預設規則，特定於區域的規則就可以根據 `host` （域）與 `default` 規則。

* 在包含的示例規則檔案中包含附加區域規則，一旦TVSDK應用 `default` 規則，如果M3U8建立域不包含 [!DNL my.domain.com] 或 [!DNL a.bcd.com] 廣告區是 `1234`創意人員被重新排序，FlashVPAID創意首先播放。 否則，將播放MP4廣告，依此類推，直至JavaScript。

* 如果選擇了廣告創意，TVSDK無法以本機方式播放( [!DNL .mp4]。 [!DNL .flv]等),TVSDK發出重新打包請求。

請注意，TVSDK可以處理的廣告類型仍通過 `validMimeTypes` 設定 `AuditudeSettings`。
