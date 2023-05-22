---
description: 可以使用不同的廣告信令模式和廣告元資料組合來標籤、刪除和替換VOD流中的時間範圍。 不同的信令模式和元資料組合導致不同的行為。
title: 廣告信令模式和廣告元資料組合對廣告插入和刪除的影響
exl-id: 0b265471-2d5c-432b-b1c9-c850ce99f2f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 廣告信令模式和廣告元資料組合對廣告插入和刪除的影響{#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

可以使用不同的廣告信令模式和廣告元資料組合來標籤、刪除和替換VOD流中的時間範圍。 不同的信令模式和元資料組合導致不同的行為。

>[!NOTE]
>
>當時間範圍和廣告信令模式之間存在衝突時，TVSDK給予時間範圍優先順序。

**表3:信令模式/元資料組合行為**

<table>  
 <thead> 
  <tr> 
   <th class="entry"> 廣告信令模式 </th> 
   <th class="entry"> 廣告元資料 </th> 
   <th class="entry"> 已建立解析器 </th> 
   <th class="entry"><span class="codeph"> 放置資訊</span> 建立 </th> 
   <th class="entry"> 結果行為 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <b>伺服器映射</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> 刪除 </td> 
   <td> 刪除 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 已刪除範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 刪除，審核 </td> 
   <td> 刪除，審核 </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE、Mode.DELETE), </span> </li> 
     <li><span class="codeph"> PlacementInfo(Type.SERVER_MAP、Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> 刪除範圍，插入廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 奧迪 </td> 
   <td> 奧迪 </td> 
   <td><span class="codeph"> PlacementInfo(Type.SERVER_MAP、Mode.INSERT)</span> </td> 
   <td> 插入的廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 替換，審慎 </td> 
   <td> 刪除，審核 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE),PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> 已替換範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤 </td> 
   <td> 自定義廣告 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 標籤的範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 馬克，奧迪 </td> 
   <td> CustomAd、Auditue </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 標籤範圍，未插入廣告 </td> 
  </tr> 
  <tr> 
   <td> <b>清單提示</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 奧迪 </td> 
   <td> 奧迪 </td> 
   <td><span class="codeph"> PlacementInfo(Type.PRE_ROLL、Mode.INSERT)</span> </td> 
   <td> 插入的廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 刪除，審核 </td> 
   <td> 刪除，審核 </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </li> 
     <li><span class="codeph"> PlacementInfo(Type.PRE_ROLL、Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> 刪除範圍，插入廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 馬克，奧迪 </td> 
   <td> 馬克，奧迪 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 標籤範圍，未插入廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 刪除 </td> 
   <td> 刪除 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 已刪除範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤 </td> 
   <td> 自定義廣告 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 標籤的範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 替換，審慎 </td> 
   <td> 刪除，審核 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE),PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> 已替換範圍 </td> 
  </tr> 
  <tr> 
   <td> <b>自定義時間範圍</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 刪除 </td> 
   <td> 刪除 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 已刪除範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 刪除，審核 </td> 
   <td> 刪除，審核 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 已刪除範圍，未插入廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 奧迪 </td> 
   <td> 奧迪 </td> 
   <td> 無 </td> 
   <td> 未插入廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 替換，審慎 </td> 
   <td> 刪除，審核 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE),PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> 用廣告替換的範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤 </td> 
   <td> 自定義廣告 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 標籤的範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 馬克，奧迪 </td> 
   <td> 定制廣告，審美 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 標籤範圍，未插入廣告 </td> 
  </tr> 
  <tr> 
   <td> <b>未設定（預設）</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 刪除 </td> 
   <td> 刪除 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 已刪除範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 刪除，審核 </td> 
   <td> 刪除，審核 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)、PlacementInfo(Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> 刪除範圍，插入廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 奧迪 </td> 
   <td> 奧迪 </td> 
   <td><span class="codeph"> PlacementInfo(Type.SERVER_MAP、Mode.INSERT)</span> </td> 
   <td> 插入的廣告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 替換，審慎 </td> 
   <td> 刪除，審核 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE),PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> 用廣告替換的範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 標籤 </td> 
   <td> 自定義廣告 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 標籤的範圍 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 馬克，奧迪 </td> 
   <td> CustomAd、Auditue </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 標籤的範圍 </td> 
  </tr> 
 </tbody> 
</table>
