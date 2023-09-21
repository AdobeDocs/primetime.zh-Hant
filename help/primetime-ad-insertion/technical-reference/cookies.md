---
description: Primetime廣告插入將Cookie用於內部用途，並方便處理串流和廣告伺服器。
title: Cookie
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# Cookie {#cookies}

Primetime廣告插入將Cookie用於內部用途，並便於使用串流和廣告伺服器。  建議使用Cookie，並建議在您的使用者端播放器上啟用。

## Cookie清單

Primetime廣告插入會維護下列Cookie：

* `ssaiPub` 協助從需要Cookie驗證的資料流擷取內容URL，以取得 `m3u8` 檔案。
* `ssai3` 會保留需要工作階段Cookie的廣告伺服器。
* `AWSELB` 和 `ssaiSession` 保留工作階段的相關資訊。
