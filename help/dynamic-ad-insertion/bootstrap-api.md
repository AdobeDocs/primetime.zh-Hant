---
title: 引導API
description: null
translation-type: tm+mt
source-git-commit: aa43834fea161c537c448b7616c9bd8f779d1a74
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---


# 引導API {#bootstrap-api}

所需參數生成引導

## 參數說明 {#parameter-description}

| 參數 | 描述 | 格式 |
|---|---|---|
| pabimode | 啟用 [即時串流的部分廣告插](ad-insertion-live-linear-stream.md#partial-ad-break-support) 入／插入。 可能的值：true to enableimot to disable（預設禁用） | HLS/DASH |
| ptadwindow | 回顧廣告決策視窗的持續時間（以秒為單位）—當DVR使用者加入串流時，「黃金時段廣告插入」會在多長時間內尋找廣告提示。 若值為零，則會停用初始資訊清單中的中段廣告決策，且決策只會在第一次更新後繼續。 此參數對於停用可持續數秒（亦即頻道轉換）的作業的廣告插入很有用。 可能的值：數字字串0-1800（預設值1800） | 僅限HLS |
| ptassetid | 發佈者指派和維護之內容的唯一ID。  與Akamai Ad Scaler搭配使用時需要。 | HLS/DASH |
| ptcdn | 托管已轉碼資產的一或多個CDN清單。 如需詳細資訊，請參 [閱Multi CDN支援](multi-cdn-support.md)。 可能的值：akamai, level3, llnw(limelight networks), comcast依預設會使用Primetime廣告插入CDN | HLS/DASH |
| ptcueformat | 要執行廣告決策的指定標籤格式（例如scte35）。 可能的值：dpisimple, dpiscte35, elemental若需自訂的提示格式，請連絡您的技術帳戶代表，以取得用於使用案例的值 | HLS/DASH |
| ptfailover | 向資訊清單伺服器發出訊號，以識別主播放清單中指定的主要和容錯串流，並將它們視為不相交集。 這有助於故障切換並防止計時錯誤。 （僅適用於Apple HLS裝置）。 如需詳細資訊，請參 [閱促進HLS播放器切換](hls-switching-to-failover.md) | 僅限HLS |
| ptmulticall | 如果啟用，則會針對VOD資產中的每個可用項目提出個別的廣告請求。  依預設，Primetime廣告插入會嘗試收集所有可用資訊，並在單一請求中將其傳送至廣告伺服器。 可能的值：true to enableimot to disable（預設禁用） | HLS/DASH |
| pttagds | 啟用將EXT-X-DINSUCTION-SEQUENCE標籤注入HLS標頭。可能的值：true to enableimot to disable（預設禁用） | 僅限HLS |
| pttimelime | 包含廣告位置和內容所需時間軸的字串，會覆寫內容串流中的廣告分段。 [ 請參閱VOD時間軸格式 ] | HLS/DASH |
| pttoken | 啟用CDN的內容片段／區段授權Token保護方案可能的值：akamai, llnw(limelight), ctl(centurylink)（預設的Token化已停用） | HLS/DASH |
| pttrackingmode | 啟用廣告追蹤方案：可能的值：用於伺服器端廣告追蹤的簡單值用於伺服器端廣告追蹤的簡單值用於混合用戶端／伺服器廣告追蹤的簡單值（依預設，未執行廣告追蹤） | HLS/DASH |
| pttrackingversion |  |  |
| ptadtimeout（如20.9.2） |  |  |
| ptparallelstream（如20.9.3） |  |  |
