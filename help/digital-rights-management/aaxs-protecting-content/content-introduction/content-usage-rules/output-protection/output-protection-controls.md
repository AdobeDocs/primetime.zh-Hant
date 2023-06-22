---
title: 輸出保護控制項
description: 輸出保護控制項
copied-description: true
exl-id: e27e49f9-9bc3-493f-a9ba-efe623694942
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# 輸出保護控制項 {#output-protection-controls}

**控制輸出至外部演算裝置的內容是否受到保護。 分別指定類比與數位輸出。**

控制是否應限制輸出至外部轉譯裝置。 外部裝置定義為未內嵌於電腦中的任何視訊或音訊裝置。 外部裝置清單不包括整合式顯示器，例如筆記型電腦。 可獨立指定類比與數位輸出限制。

可使用下列執行選項/層級：

<table frame="all" colsep="0" rowsep="1" id="adobetable_fvw_5fx_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">支援類比裝置 </p> </th> 
   <th colname="3" class="- topic/entry entry"> <p class="- topic/p ">數位裝置支援 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">必填</b>  — 類比複製保護(ACP)或複製產生管理系統 — 必須啟用類比(CGMS-A)輸出保護，才能播放內容到外部裝置。 Adobe存取使用者端必須使用ACP或CGMS-A啟用輸出保護。在支援兩者的裝置上，AdobeAccess 3.0使用者端會嘗試同時啟用兩者。 不過，僅需啟用一個即可播放內容。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">需要ACP</b>  — 需要ACP輸出保護。 不允許在CGMS-A上播放。Adobe Access 2.0使用者端不支援此選項。 如果設定，Adobe存取2.0使用者端的行為會與已指定「無播放」選項相同。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">需要CGMS-A</b> — CGMS — 需要輸出保護。 ACP上不允許播放。 Adobe Access 2.0使用者端不支援此選項。 如果設定，Adobe存取2.0使用者端的行為會與已指定「無播放」選項相同。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">使用（如果可用）</b>  — 嘗試啟用ACP和CGMS-A輸出保護（如果可用），如果不可用則允許播放。 如果可能，Adobe存取3.0使用者端會嘗試同時啟用ACP和CGMS-A。 Adobe存取2.0使用者端只會嘗試啟用ACP或CGMS-A。例如，Adobe存取使用者端會嘗試啟用ACP或CGMS-A。如果嘗試成功，則不會啟用其他選項。 如果嘗試失敗，將再次嘗試啟用另一個選項。 即使兩次嘗試都失敗，內容仍會播放。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">使用ACP （如果可用）</b>  — 嘗試啟用ACP輸出保護（如果可用），但允許播放（如果不可用）。 CGMS-A上無法使用保護。Adobe Access 2.0使用者端不支援此選項。 如果設定，Adobe存取2.0使用者端的行為會與已指定「無保護」選項相同。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">使用CGMS-A （如果可用） </b> — 嘗試啟用CGMS-A輸出保護（如果可用），但允許播放（如果不可用）。 無法在ACP上提供保護。 Adobe Access 2.0使用者端不支援此選項。 如果設定，Adobe存取2.0使用者端的行為會與已指定「無保護」選項相同。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">無保護</b>  — 模擬和數位輸出不強制啟用輸出保護。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">無播放</b>  — 不允許對外部裝置播放類比與數位輸出。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>雖然這些規則在所有平台上都一定會執行，但目前只能在Windows平台上安全地開啟輸出保護。 其他平台（例如Macintosh和Linux）沒有支援的作業系統功能可供協力廠商應用程式使用。

使用案例範例：某些內容可能會強制執行輸出保護控制項，而保護層級可由內容散發者設定。 如果指定「必要」且嘗試在Macintosh上播放，使用者端不會在外部裝置上播放內容。 不過，內容會在內部顯示器上播放。

如果指定「必要」且嘗試在Linux上播放，使用者端不會在任何裝置上播放內容，因為無法區分內部和外部裝置。

如果您指定「如果可用則使用」，則會儘可能開啟輸出保護。 例如，在支援Certified Output Protection Protocol (COPP)的Windows電腦上，內容會透過輸出保護傳送至外部顯示器。 此範例有時稱為「可選擇的輸出控制」。
