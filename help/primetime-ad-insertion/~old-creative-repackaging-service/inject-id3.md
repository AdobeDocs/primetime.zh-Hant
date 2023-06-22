---
description: CRS可以將ID3定時中繼資料插入HLS格式廣告創意，以促進使用者端廣告追蹤。
title: 使用CRS插入ID3計時中繼資料標籤
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# 使用CRS插入ID3計時中繼資料標籤 {#using-crs-to-inject-id-timed-metadata-tags}

CRS可以將ID3定時中繼資料插入HLS格式廣告創意，以促進使用者端廣告追蹤。

使用者端播放器會讀取ID3中繼資料，以啟用精確影格的廣告追蹤。

>[!NOTE]
>
>ID3定時中繼資料插入僅適用於iOS上的Safari。

## ID3注入的CRS工作流程 {#workflow-for-crs-for-id3-injection}

ID3插入的工作流程與中的相同 [JIT重新封裝的詳細工作流程。](../~old-creative-repackaging-service/jit-repackage.md) 如果資訊清單伺服器收到 `ptplayer=ios-mobileweb` 引數，它會告知CRS先將ID3封包插入CRS轉碼廣告創意，然後再上傳至CDN伺服器。

>[!NOTE]
>
>在多CDN設定中，資訊清單伺服器會使用 `ptcdn` 啟動程式URL中的引數，用於識別要上傳廣告創意的CDN伺服器。