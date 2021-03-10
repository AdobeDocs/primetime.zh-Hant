---
title: 輸出保護控制
description: 輸出保護控制
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---


# 輸出保護控制{#output-protection-controls}

**控制輸出至外部轉換裝置是否受到保護。獨立指定模擬和數字輸出。**

控制輸出至外部轉換裝置的限制。 外部設備定義為未嵌入電腦中的任何視頻或音頻設備。 外部設備清單不包括整合顯示器，例如筆記型電腦。 模擬和數字輸出限制可以單獨指定。

可使用下列選項／強制級別：

<table frame="all" colsep="0" rowsep="1" id="adobetable_fvw_5fx_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">在模擬設備中支援 </p> </th> 
   <th colname="3" class="- topic/entry entry"> <p class="- topic/p ">數位裝置支援 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">必要</b> — 模擬複製保護(ACP)或複製生成管理系統——必須啟用模擬(CGMS-A)輸出保護，以便向外部設備播放內容。Adobe訪問客戶端必須使用ACP或CGMS-A啟用輸出保護。在同時支援這兩者的設備上，AdobeAccess 3.0客戶端將嘗試同時啟用這兩者。 但是，只有一個必須啟用才能播放內容。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">需要ACP</b> — 需要ACP輸出保護。CGMS-A不允許播放。AdobeAccess 2.0客戶端不支援此選項。 如果設定，AdobeAccess 2.0客戶端將像指定了「無回放」選項一樣運行。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">CGMS-A必要</b> — 需要CGMS-A輸出保護。不允許在ACP上播放。 AdobeAccess 2.0客戶端不支援此選項。 如果設定，AdobeAccess 2.0客戶端將像指定了「無回放」選項一樣運行。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">使用(如果可用</b> )— 嘗試啟用ACP和CGMS-A輸出保護（如果可用），如果不可用則允許播放。AdobeAccess 3.0客戶端將嘗試啟用ACP和CGMS-A（如果可能）。 AdobeAccess 2.0客戶端將僅嘗試啟用ACP或CGMS-A。例如，Adobe訪問客戶端將嘗試啟用ACP或CGMS-A。如果嘗試成功，則不會啟用其他選項。 如果嘗試失敗，則會再次嘗試啟用另一個選項。 即使兩次嘗試都失敗，內容仍會播放。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">使用ACP(如果可用</b> )— 嘗試啟用ACP輸出保護（如果可用），但如果不可用則允許播放。CGMS-A上不提供保護。AdobeAccess 2.0客戶端不支援此選項。 如果設定，AdobeAccess 2.0客戶端將像指定了「無保護」選項一樣運行。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">使用CGMS-A（如果可用） </b>— 嘗試啟用CGMS-A輸出保護（如果可用），但如果不可用則允許播放。ACP上不提供保護。 AdobeAccess 2.0客戶端不支援此選項。 如果設定，AdobeAccess 2.0客戶端將像指定了「無保護」選項一樣運行。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">沒有保護</b> — 模擬和數字輸出不啟用輸出保護。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">無播放</b> -不允許對模擬和數字輸出的外部設備進行播放。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>雖然這些規則在所有平台上都一致地執行，但目前只有在Windows平台上安全地開啟輸出保護功能。 在其他平台（例如Macintosh和Linux）上，協力廠商應用程式沒有支援的作業系統功能。

範例使用案例：某些內容可能會強制執行輸出保護控制，而保護等級可由內容配銷商設定。 如果指定「必要」，並嘗試在Macintosh上播放，則用戶端不會在外部裝置上播放內容。 不過，內容會在內部顯示器上播放。

如果指定「必要」並嘗試在Linux上播放，則客戶端不會在任何裝置上播放內容，因為無法區分內部和外部裝置。

如果您指定「Use if available」（使用可用時），則會在可能的情況下開啟輸出保護。 例如，在支援認證輸出保護通訊協定(COPP)的Windows電腦上，內容會隨輸出保護傳遞至外部顯示器。 此範例有時稱為「可選輸出控制」。
