---
description: CRS提供即時(JIT)和非同步重新封裝以及HLS到HLS的轉換。 重新封裝的結果是原始廣告創意的HLS格式化版本。 CRS會將HLS格式版本放置在內容傳遞網路(CDN)伺服器上，以便在需要時使用。
title: CRS的主要用途
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# CRS的主要用途 {#main-uses-of-crs}

CRS提供即時(JIT)和非同步重新封裝以及HLS到HLS的轉換。 重新封裝的結果是原始廣告創意的HLS格式化版本。 CRS會將HLS格式版本放置在內容傳遞網路(CDN)伺服器上，以便在需要時使用。

在JIT重新封裝Adobe Primetime中，當廣告第一次遇到非HLS廣告創意時，廣告插入會開始重新封裝程式。 這通常會導致在重新封裝程式期間失去執行廣告的機會。

在非同步重新封裝中，廣告創意會在需要之前被轉碼和儲存，從而消除這些失去的機會。

在HLS到HLS的轉換中，CRS會將HLS廣告創意重新格式化為適當大小的區塊，以確保一致的播放。

## 即時重新封裝 {#section_1BA344F2300B49F291865A7461EDFEAE}

JIT重新封裝的順序如下：

1. 資訊清單伺服器會擷取廣告。
1. 如果廣告格式為HLS，資訊清單伺服器會將廣告插入內容串流中。
1. 如果格式不是HLS （例如MP4、FLV或WebM），資訊清單伺服器會在CDN伺服器上尋找轉碼版本。 如果找到轉碼廣告，會將轉碼廣告插入內容資料流。
1. 如果格式不是HLS，且CDN伺服器沒有轉碼版本，資訊清單伺服器會將廣告傳遞至CRS，CRS會將廣告創意轉碼，並將結果儲存在CDN伺服器以供稍後使用。
1. 資訊清單伺服器傳回不含廣告的內容。

## 非同步重新封裝 {#section_ACDFB43FDA4B445CB9F2A107FEB4F2F7}

您可以使用中說明的API [重新封裝API](../~old-creative-repackaging-service/api-repackage.md) 將非HLS創意內容預先轉碼，以將曝光次數損失降至最低並最大化營收。

## HLS到HLS的轉換 {#section_877A0E7E8FAF4C2DB086A31C24D53435}

為避免緩衝和延遲，使用者端會下載小片段的影片。 如果區塊大小不一致，則播放可能會不連貫。 HLS到HLS的轉換可確保資料區塊都維持相同的持續時間（例如6秒）。

>[!NOTE]
>
>CRS會產生HLS版本3，無論它收到哪個HLS版本。