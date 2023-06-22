---
title: 設定廣告追蹤
description: 設定廣告追蹤
exl-id: b5ebad0f-4e20-456a-892d-4c981ab26e51
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# 設定廣告追蹤 {#ser-up-ad-tracking}

大多數廣告商需要有關何時檢視其廣告、檢視時間長短和檢視成功程度的資訊。 PrimetimeAd Insertion支援使用者端、伺服器端和混合式廣告追蹤，以便在收集此資訊時提供靈活性。

## 使用VMAP/JSON追蹤使用者端廣告 {#client-side-ad-tracking-vmap-json}

在使用者端廣告追蹤中，伺服器會將指定追蹤事件和URL以及廣告拼接播放清單的JSON、VMAP或資訊清單內結構傳送給使用者端。

若要啟用使用者端廣告追蹤，請在 [BOOTSTRAPAPI](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

* `pttrackingmode=simple`

* `pttrackingversion={format version (vmap,v1,v2,v3)}`

>[!NOTE]
>
>設定 `pttrackingmode=simple` 將導致初始啟動程式API請求傳回JSON回應，而不是HLS或DASH檔案。

<!-- **Daniel to check. The specified file in this statement does not exist.** 
More information about `pttrackingmode`, `pttrackingversion` formats, can be found in [API Reference: Manifest server query parameters](manifest-server-query-parameters.md). -->

<!--Show examples of how to request a sidecar] -->

## 伺服器端廣告追蹤 {#server-side-ad-tracking}

使用此方法，廣告追蹤資料完全在伺服器端計算。 這在更新使用者端應用程式不可行時很有用。 不過，伺服器端廣告追蹤可能不符合使用者端播放活動。 例如，即使一般使用者沒有檢視整個廣告，伺服器也會在區段傳送後考慮要播放廣告。

若要啟用伺服器端廣告追蹤，請在 [BOOTSTRAPAPI](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

`pttrackingmode=sstm`

另請參閱 `pttrackingmode` 部分 [BOOTSTRAPAPI](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

所有廣告追蹤信標都會隨下列HTTP要求標題傳送：

* `X-Forwarded-For`
* `User-Agent`
* `X-Device-User-Agent`

這些值包含使用者端/播放器使用者代理程式和使用者端IP位址。

## 混合式廣告追蹤 {#hybrid-ad-tracking}

此方法類似於伺服器端追蹤，但使用者端應用程式也向PrimetimeAd Insertion要求側邊欄，以取得詳細的追蹤資訊。 混合式廣告追蹤可以向使用者端應用程式提供非線性廣告（例如覆蓋和同伴），同時仍仰賴PrimetimeAd Insertion傳送個別廣告追蹤URL。
若要啟用混合式廣告追蹤，請參閱 `pttrackingmode` 中的引數 [BOOTSTRAPAPI](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).
