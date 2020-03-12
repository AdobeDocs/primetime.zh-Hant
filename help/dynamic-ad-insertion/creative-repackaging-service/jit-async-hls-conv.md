---
description: CRS提供即時(JIT)和非同步重新封裝以及HLS到HLS的轉換。 重新封裝的結果是原始廣告創意的HLS格式版本。 CRS會視需要將HLS格式化版本放在內容放送網路(CDN)伺服器上使用。
seo-description: CRS提供即時(JIT)和非同步重新封裝以及HLS到HLS的轉換。 重新封裝的結果是原始廣告創意的HLS格式版本。 CRS會視需要將HLS格式化版本放在內容放送網路(CDN)伺服器上使用。
seo-title: CRS的主要用途
title: CRS的主要用途
uuid: df2caa67-bc94-4146-9b93-14edc060c3d5
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# CRS的主要用途 {#main-uses-of-crs}

CRS提供即時(JIT)和非同步重新封裝以及HLS到HLS的轉換。 重新封裝的結果是原始廣告創意的HLS格式版本。 CRS會視需要將HLS格式化版本放在內容放送網路(CDN)伺服器上使用。

在JIT重新封裝中，Adobe Primetime廣告插入會在首次遇到非HLS廣告創意素材時開始重新封裝程式。 這通常會導致在重新封裝程式期間失去執行廣告的機會。

在非同步重新封裝中，廣告創意素材會在需要之前進行轉碼並儲存，以消除這些失去的機會。

在HLS到HLS的轉換中，CRS會將HLS廣告創意重新格式化為適當大小的區塊，以確保一致的播放。

## 即時重新封裝 {#section_1BA344F2300B49F291865A7461EDFEAE}

JIT再包裝順序為：

1. 資訊清單伺服器擷取廣告。
1. 如果廣告格式為HLS，資訊清單伺服器會將廣告插入內容串流。
1. 如果格式不是HLS（例如MP4、FLV或WebM），資訊清單伺服器會在CDN伺服器上尋找轉碼版本。 如果找到一個，則會將轉碼廣告插入內容串流。
1. 如果格式不是HLS，而CDN伺服器沒有轉碼版本，資訊清單伺服器會將廣告傳遞至CRS,CRS會轉碼廣告創意並將結果儲存在CDN伺服器上以供日後使用。
1. 資訊清單伺服器會傳回不含廣告的內容。

## 非同步重新封裝 {#section_ACDFB43FDA4B445CB9F2A107FEB4F2F7}

您可以使用重新封裝API中所述的API [](../creative-repackaging-service/api-repackage.md) ，對非HLS創意素材進行預先轉碼，以減少曝光次數並最大化獲利。

## HLS到HLS的轉換 {#section_877A0E7E8FAF4C2DB086A31C24D53435}

為避免緩衝和延遲，用戶端會以小塊下載視訊。 如果區塊大小不一致，則播放可能會變得不順暢。 HLS到HLS的轉換可確保資料區塊的持續時間都相同（例如，6秒）。

>[!NOTE]
>
>CRS會產生HLS第3版，不論它收到的是哪個HLS版本。