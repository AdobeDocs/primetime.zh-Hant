---
title: 設定廣告追蹤
description: 設定廣告追蹤
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# 設定廣告追蹤{#ser-up-ad-tracking}

大部分廣告商都需要有關廣告被檢視的時間、時間長度以及成功程度的資訊。 Primetime廣告插入支援用戶端、伺服器端和混合式廣告追蹤，以提供收集此資訊的彈性。

## 使用VMAP/JSON {#client-side-ad-tracking-vmap-json}進行用戶端廣告追蹤

在用戶端廣告追蹤中，伺服器會傳送JSON、VMAP或資訊清單內結構給用戶端，以指定追蹤事件和URL以及廣告銜接播放清單。

若要啟用用戶端廣告追蹤，請在[引導API](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)中指定下列參數。

* `pttrackingmode=simple`

* `pttrackingversion={format version (vmap,v1,v2,v3)}`

>[!NOTE]
>
>設定`pttrackingmode=simple`會導致初始引導API請求傳回JSON回應，而非HLS或DASH檔案。

有關`pttrackingmode`、`pttrackingversion`格式的詳細資訊，請參閱[API參考：資訊清單伺服器查詢參數](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)。

## 伺服器端廣告追蹤{#server-side-ad-tracking}

使用此方法，廣告追蹤資料會完全在伺服器端計算。 在更新客戶端應用程式不可行時，此功能非常有用。 不過，伺服器端廣告追蹤可能不符合用戶端播放活動。 例如，伺服器會認為廣告會在傳送區段後播放，即使使用者未檢視整個廣告亦然。

若要啟用伺服器端廣告追蹤，請在[引導API](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)中指定下列參數。

`pttrackingmode=sstm`

請參閱[引導API](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)的`pttrackingmode`章節。

所有廣告追蹤信標都會隨下列HTTP請求標題傳送：

* `X-Forwarded-For`
* `User-Agent`
* `X-Device-User-Agent`

這些值包含client/player user-agent和client IP位址。

## 混合廣告追蹤{#hybrid-ad-tracking}

此方法類似伺服器端追蹤，但用戶端應用程式也會要求Primetime廣告插入的附屬資訊，以取得詳細的追蹤資訊。 混合式廣告追蹤可傳送非線性廣告，例如覆蓋和客戶應用程式的伴侶，同時仍依賴「Primetime廣告插入」來傳送個別廣告追蹤URL。
若要啟用混合廣告追蹤，請參閱[引導API](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)中的`pttrackingmode`參數。
