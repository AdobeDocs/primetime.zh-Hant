---
description: 用戶端視訊播放器或資訊清單伺服器可與CRS互動，以達成JIT重新封裝。 兩者都使用相同的廣告選擇邏輯。
title: JIT重新封裝的詳細工作流程
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# JIT重新封裝的詳細工作流程{#detailed-workflows-for-jit-repackaging}

用戶端視訊播放器或資訊清單伺服器可與CRS互動，以達成JIT重新封裝。 兩者都使用相同的廣告選擇邏輯。

## JIT重新打包由Manifest Server {#section_1F1C1B7DD146403890C2B43E24FEF0EB}啟動

![](assets/ssai_JIT-workflow_web.png)

資訊清單伺服器端的JIT重新封裝工作流程如下：

1. 資訊清單伺服器向廣告伺服器提出要求。
1. 資訊清單伺服器會收到非HLS格式的廣告創意。
1. 資訊清單伺服器傳送對廣告創意之先前轉碼的HLS版本的要求至CDN伺服器。

   >[!NOTE]
   >
   >在多CDN設定中，資訊清單伺服器使用引導URL中的`ptcdn`參數來識別CDN伺服器。

1. 資訊清單伺服器會檢查回應：

   1. 如果請求成功，manifest伺服器會將廣告創意的先前轉碼HLS版本插入內容串流。
   1. 如果請求失敗，資訊清單伺服器會產生記錄項目並從CRS要求轉碼版本。

1. CRS會轉碼廣告創意內容，並將HLS版本上傳至CDN伺服器以供日後使用。

對於該創意素材的所有後續要求，資訊清單伺服器會從CDN擷取HLS版本，並將其插入內容串流。

## 由客戶{#section_FBC97D40043F4FDD98247A08BB6195B0}啟動的JIT重新打包

<!--<a id="fig_hkn_ndt_3z"></a>-->

![](assets/ssai_JIT-workflow_client_web.png)

基於TVSDK或具備類似功能的用戶端可與CRS互動，以達成JIT重新封裝，如下所示：

1. 用戶端會向廣告伺服器要求廣告。
1. 廣告伺服器會將廣告傳回至用戶端。
1. 用戶端會從廣告伺服器檢查廣告格式：

   1. 如果廣告創意素材是HLS格式，客戶會將它插入（接線）內容，然後完成。
   1. 如果廣告創意不是HLS格式，則用戶端會向CDN伺服器要求一個。

      >[!NOTE]
      >
      >在多CDN設定中，資訊清單伺服器使用引導URL中的`ptcdn`參數來識別CDN伺服器。

1. 用戶端會檢查來自CDN伺服器的回應。

   1. 如果CDN提供HLS版本，用戶端會將它插入（接線）內容，並完成。
   1. 如果CDN伺服器未提供HLS版本，用戶端會要求廣告伺服器向CRS請求。 用戶端不會將廣告插入內容。

1. 廣告伺服器要求將非HLS廣告轉碼至HLS。
1. CRS會建立HLS版本，並將它上傳至CDN伺服器以供日後使用。

## 廣告格式優先順序和時間表{#section_A74DE37A57BF45D7B6D09E3DE40F8E61}

資訊清單伺服器和用戶端使用相同的選擇邏輯來決定播放可用廣告的優先順序。 HLS格式化廣告優先，其次是MP4、FLV和WebM。

CRS通常需要2-4分鐘來處理非HLS廣告創意素材，通常不到3分鐘。

CRS產生不同的HLS位元速率，因此廣告可以以適合可用連線速度和頻寬的速度播放。 如果有多個可用比特率，CRS選擇可用的最高比特率。 如果CRS收到非HLS廣告創意，則會以可用的最高解析度產生HLS版本。