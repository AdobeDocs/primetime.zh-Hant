---
description: CRS提供了即時(JIT)和非同步重新打包以及HLS到HLS的轉換。 重新打包的結果是原始廣告創意的HLS格式版本。 CRS將HLS格式化版本放置在內容分發網路(CDN)伺服器上，以便在需要時使用。
title: CRS的主要用途
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# CRS的主要用途 {#main-uses-of-crs}

CRS提供了即時(JIT)和非同步重新打包以及HLS到HLS的轉換。 重新打包的結果是原始廣告創意的HLS格式版本。 CRS將HLS格式化版本放置在內容分發網路(CDN)伺服器上，以便在需要時使用。

在JIT重新打包Adobe Primetime廣告插入時，首次遇到非HLS廣告創意時，將開始重新打包過程。 這通常會導致在重新打包過程中丟失運行廣告的機會。

在非同步重新打包中，廣告創意在需要之前被轉碼並儲存，這可以消除那些丟失的機會。

在HLS到HLS的轉換中，CRS將HLS廣告重新格式化為適當大小的塊，以確保一致的回放。

## 及時重新打包 {#section_1BA344F2300B49F291865A7461EDFEAE}

JIT重新包裝的順序如下：

1. 清單伺服器讀取廣告。
1. 如果廣告格式為HLS，則清單伺服器將廣告插入內容流。
1. 如果格式不是HLS（例如MP4、FLV或WebM），則清單伺服器在CDN伺服器上查找轉碼版本。 如果找到一個，則會將轉碼廣告插入內容流。
1. 如果格式不是HLS，並且CDN伺服器沒有轉碼版本，則清單伺服器將廣告傳遞給CRS,CRS對廣告進行轉碼，並將結果儲存在CDN伺服器上以供以後使用。
1. 清單伺服器返回沒有廣告的內容。

## 非同步重新打包 {#section_ACDFB43FDA4B445CB9F2A107FEB4F2F7}

可以使用中介紹的API [重新打包API](../~old-creative-repackaging-service/api-repackage.md) 對非HLS的創意進行預編碼，以盡量減少印象損失和最大化貨幣化。

## HLS到HLS的轉換 {#section_877A0E7E8FAF4C2DB086A31C24D53435}

為避免緩衝和延遲，客戶端以小塊形式下載視頻。 如果區塊大小不一致，則回放可能會變得亂糟糟。 HLS到HLS的轉換可確保資料塊的持續時間均相同（例如，6秒）。

>[!NOTE]
>
>CRS生成HLS版本3，而不管它接收的是哪個HLS版本。