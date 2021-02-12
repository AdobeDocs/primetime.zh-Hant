---
description: 即時轉碼功能可將ID3計時中繼資料注入廣告創意，以利用戶端廣告追蹤。
seo-description: 即時轉碼可將ID3計時中繼資料注入HLS格式廣告創意，以利用戶端廣告追蹤。
seo-title: 使用即時轉碼來插入ID3計時中繼資料標籤
title: 使用即時轉碼來插入ID3計時中繼資料標籤
uuid: 491bbb9e-15de-4871-baa1-f7bb0ea0dde2
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 使用Just-in-Time Codecing來插入ID3 Timed Metadata標籤{#using-crs-to-inject-id-timed-metadata-tags}

CRS可將ID3計時中繼資料插入廣告創意，以利用戶端廣告追蹤。

用戶端播放器會讀取ID3中繼資料，以啟用影格精確的廣告追蹤。

>[!NOTE]
>
>ID3計時中繼資料插入功能僅適用於Safari/iOS。

## ID3植入{#workflow-for-crs-for-id3-injection}的CRS工作流程

如果Primetime廣告插入收到`ptplayer=ios-mobileweb`參數，則會先將ID3封包插入轉碼廣告創意素材，然後再上傳至適當的廣告儲存CDN。
