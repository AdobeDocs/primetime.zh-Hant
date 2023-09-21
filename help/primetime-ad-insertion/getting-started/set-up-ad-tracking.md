---
title: 設定廣告追蹤
description: 設定廣告追蹤
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# 設定廣告追蹤 {#ser-up-ad-tracking}

大多數廣告商都要求提供何時檢視、檢視時間長短，以及成功檢視廣告的相關資訊。 PrimetimeAd Insertion支援使用者端、伺服器端和混合式廣告追蹤，以便在收集此資訊時提供彈性。

## 使用VMAP/JSON追蹤使用者端廣告 {#client-side-ad-tracking-vmap-json}

在使用者端廣告追蹤中，伺服器會將指定追蹤事件和URL以及廣告拼接播放清單的JSON、VMAP或資訊清單內結構傳送給使用者端。

若要啟用使用者端廣告追蹤，請在 [BOOTSTRAP API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

* `pttrackingmode=simple`

* `pttrackingversion={format version (vmap,v1,v2,v3)}`

>[!NOTE]
>
>設定 `pttrackingmode=simple` 將會導致初始啟動程式API要求傳回JSON回應，而非HLS或DASH檔案。

<!-- **Daniel to check. The specified file in this statement does not exist.** 
More information about `pttrackingmode`, `pttrackingversion` formats, can be found in [API Reference: Manifest server query parameters](manifest-server-query-parameters.md). -->

<!--Show examples of how to request a sidecar] -->

## 伺服器端廣告追蹤 {#server-side-ad-tracking}

使用此方法時，廣告追蹤資料會在伺服器端完全計算。 這在更新使用者端應用程式不可行時很有用。 不過，伺服器端廣告追蹤可能不符合使用者端播放活動。 例如，伺服器會在傳送區段後考慮要播放廣告，即使一般使用者沒有檢視整個廣告亦然。

若要啟用伺服器端廣告追蹤，請在 [BOOTSTRAP API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

`pttrackingmode=sstm`

另請參閱 `pttrackingmode` 「 」的部分 [BOOTSTRAP API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

所有廣告追蹤信標都會與下列HTTP要求標題一併傳送：

* `X-Forwarded-For`
* `User-Agent`
* `X-Device-User-Agent`

這些值包含使用者端/播放器使用者代理程式和使用者端IP位址。

## 混合式廣告追蹤 {#hybrid-ad-tracking}

此方法類似於伺服器端追蹤，但使用者端應用程式也會向PrimetimeAd Insertion要求側碼，以取得詳細的追蹤資訊。 混合式廣告追蹤可以向使用者端應用程式提供非線性廣告，例如覆蓋和同伴，同時仍仰賴PrimetimeAd Insertion傳送個別廣告追蹤URL。
若要啟用混合式廣告追蹤，請參閱 `pttrackingmode` 中的引數 [BOOTSTRAP API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).
