---
description: CRS可將ID3計時中繼資料注入HLS格式廣告創意，以利用戶端廣告追蹤。
seo-description: CRS可將ID3計時中繼資料注入HLS格式廣告創意，以利用戶端廣告追蹤。
seo-title: 使用CRS插入ID3計時中繼資料標籤
title: 使用CRS插入ID3計時中繼資料標籤
uuid: 491bbb9e-15de-4871-baa1-f7bb0ea0dde2
translation-type: tm+mt
source-git-commit: c2216a5089d23ca1fcbb77c87b4a01a6fa1807ff
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# 使用CRS插入ID3計時中繼資料標籤{#using-crs-to-inject-id-timed-metadata-tags}

CRS可將ID3計時中繼資料注入HLS格式廣告創意，以利用戶端廣告追蹤。

用戶端播放器會讀取ID3中繼資料，以啟用影格精確的廣告追蹤。

>[!NOTE]
>
>ID3計時中繼資料插入僅適用於iOS上的Safari。

## ID3植入{#workflow-for-crs-for-id3-injection}的CRS工作流程

ID3植入的工作流程與[JIT重新封裝的詳細工作流程相同。](../creative-repackaging-service/jit-repackage.md) 如果資訊清單伺服器收 `ptplayer=ios-mobileweb` 到參數，它會告訴CRS在將ID3封包上傳至CDN伺服器之前，先將ID3封包注入轉碼廣告創意。

>[!NOTE]
>
>在多CDN設定中，資訊清單伺服器使用引導URL中的`ptcdn`參數來識別CDN伺服器以上傳廣告創意。