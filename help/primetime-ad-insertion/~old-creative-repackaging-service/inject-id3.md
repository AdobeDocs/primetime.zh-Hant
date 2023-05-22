---
description: CRS可以將ID3定時元資料注入HLS格式和創意中，以便於客戶端和跟蹤。
title: 使用CRS插入ID3定時元資料標籤
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# 使用CRS插入ID3定時元資料標籤 {#using-crs-to-inject-id-timed-metadata-tags}

CRS可以將ID3定時元資料注入HLS格式和創意中，以便於客戶端和跟蹤。

客戶端播放器讀取ID3元資料以啟用幀精確和跟蹤。

>[!NOTE]
>
>ID3定時元資料注入僅在iOS的Safari上工作。

## ID3注入的CRS工作流 {#workflow-for-crs-for-id3-injection}

ID3注入的工作流與中相同 [JIT重新打包的詳細工作流。](../~old-creative-repackaging-service/jit-repackage.md) 如果清單伺服器收到 `ptplayer=ios-mobileweb` 參數，在將ID3資料包上傳到CDN伺服器之前，通知CRS將ID3資料包注入轉碼和創作。

>[!NOTE]
>
>在多CDN設定中，清單伺服器使用 `ptcdn` 引導URL中的參數，以標識要上載廣告的CDN伺服器。