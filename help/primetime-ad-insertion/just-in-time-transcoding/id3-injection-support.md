---
description: 即時轉碼可將ID3計時中繼資料插入廣告創意中，以促進使用者端廣告追蹤。
title: 使用即時轉碼來插入ID3計時中繼資料標籤
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# 使用即時轉碼來插入ID3計時中繼資料標籤 {#using-crs-to-inject-id-timed-metadata-tags}

CRS可以將ID3定時中繼資料插入廣告創意內容，以便利使用者端廣告追蹤。

使用者端播放器會讀取ID3中繼資料，以啟用精確影格的廣告追蹤。

>[!NOTE]
>
>ID3定時中繼資料插入功能僅適用於Safari/iOS。

## ID3插入的CRS工作流程 {#workflow-for-crs-for-id3-injection}

如果PrimetimeAd Insertion收到 `ptplayer=ios-mobileweb` 引數，它會先將ID3封包插入轉碼廣告創意，再上傳至適當的廣告儲存CDN。
