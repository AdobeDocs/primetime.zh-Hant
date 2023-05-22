---
title: 設定廣告跟蹤
description: 設定廣告跟蹤
exl-id: b5ebad0f-4e20-456a-892d-4c981ab26e51
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# 設定廣告跟蹤 {#ser-up-ad-tracking}

大多數廣告商都需要有關他們的廣告被瀏覽時間、瀏覽時間以及瀏覽成功程度的資訊。 黃金時段Ad Insertion支援客戶端、伺服器端和混合廣告跟蹤，以提供收集這些資訊的靈活性。

## 使用VMAP/JSON的客戶端廣告跟蹤 {#client-side-ad-tracking-vmap-json}

在客戶端廣告跟蹤中，伺服器向客戶端發送JSON、VMAP或清單內結構，指定跟蹤事件和URL以及廣告縫合播放清單。

要啟用客戶端和跟蹤，請在 [BootstrapAPI](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md)。

* `pttrackingmode=simple`

* `pttrackingversion={format version (vmap,v1,v2,v3)}`

>[!NOTE]
>
>設定 `pttrackingmode=simple` 將導致初始引導API請求返回JSON響應，而不是HLS或DASH文檔。

<!-- **Daniel to check. The specified file in this statement does not exist.** 
More information about `pttrackingmode`, `pttrackingversion` formats, can be found in [API Reference: Manifest server query parameters](manifest-server-query-parameters.md). -->

<!--Show examples of how to request a sidecar] -->

## 伺服器端廣告跟蹤 {#server-side-ad-tracking}

利用該方法，在伺服器端完全計算廣告跟蹤資料。 當更新客戶端應用程式不可行時，此功能非常有用。 但是，伺服器端廣告跟蹤可能與客戶端播放活動不匹配。 例如，伺服器認為在傳遞段之後要播放的廣告，即使最終用戶不查看整個廣告。

要啟用伺服器端和跟蹤，請在 [BootstrapAPI](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md)。

`pttrackingmode=sstm`

請參閱 `pttrackingmode` 部分 [BootstrapAPI](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md)。

所有廣告跟蹤信標都使用以下HTTP請求標頭髮送：

* `X-Forwarded-For`
* `User-Agent`
* `X-Device-User-Agent`

這些值包含客戶機/播放器用戶代理和客戶機IP地址。

## 混合廣告跟蹤 {#hybrid-ad-tracking}

這種方法類似於伺服器端跟蹤，但客戶端應用程式也從MighideAd Insertion請求十進位號，以獲取詳細的跟蹤資訊。 混合廣告跟蹤可以將諸如覆蓋和伴侶等非線性廣告發送到客戶端應用程式，同時仍然依靠黃金時段Ad Insertion發送單個廣告跟蹤URL。
要啟用混合廣告跟蹤，請參閱 `pttrackingmode` 參數 [BootstrapAPI](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md)。
