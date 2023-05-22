---
title: 輸出保護控制
description: 輸出保護控制
copied-description: true
exl-id: e27e49f9-9bc3-493f-a9ba-efe623694942
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# 輸出保護控制 {#output-protection-controls}

**控制是否保護輸出到外部呈現設備。 獨立指定模擬和數字輸出。**

控制是否應限制輸出到外部呈現設備。 外部設備定義為未嵌入電腦中的任何視頻或音頻設備。 外部設備清單不包括整合顯示，如在筆記型電腦中。 可以獨立地指定模擬和數字輸出限制。

以下選項/強制級別可用：

<table frame="all" colsep="0" rowsep="1" id="adobetable_fvw_5fx_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">在模擬設備中支援 </p> </th> 
   <th colname="3" class="- topic/entry entry"> <p class="- topic/p ">在數字設備中支援 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">必需</b>  — 模擬複製保護(ACP)或複製生成管理系統 — 必須啟用模擬(CGMS-A)輸出保護，才能向外部設備播放內容。 Adobe訪問客戶端必須使用ACP或CGMS-A啟用輸出保護。在支援兩者的設備上，AdobeAccess 3.0客戶端將嘗試啟用兩者。 但是，只能啟用一個內容才能播放內容。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">需要ACP</b>  — 需要ACP輸出保護。 CGMS-A上不允許播放。AdobeAccess 2.0客戶端不支援此選項。 如果設定，AdobeAccess 2.0客戶端將像指定了「無回放」選項一樣運行。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">需要CGMS-A</b>  — 需要CGMS-A輸出保護。 ACP上不允許播放。 AdobeAccess 2.0客戶端不支援此選項。 如果設定，AdobeAccess 2.0客戶端將像指定了「無回放」選項一樣運行。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">使用（如果可用）</b>  — 嘗試啟用ACP和CGMS-A輸出保護（如果可用），如果不可用則允許播放。 AdobeAccess 3.0客戶端將嘗試啟用ACP和CGMS-A（如果可能）。 AdobeAccess 2.0客戶端將僅嘗試啟用ACP或CGMS-A。例如，Adobe訪問客戶端將嘗試啟用ACP或CGMS-A。如果嘗試成功，則不會啟用其他選項。 如果嘗試失敗，將再次嘗試啟用另一個選項。 即使兩次嘗試都失敗，內容仍將被播放。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">使用ACP（如果可用）</b>  — 嘗試啟用ACP輸出保護（如果可用），但如果不可用則允許播放。 CGMS-A上沒有保護。AdobeAccess 2.0客戶端不支援此選項。 如果設定，AdobeAccess 2.0客戶端將像指定了「無保護」選項一樣運行。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">使用CGMS-A（如果可用） </b> — 嘗試啟用CGMS-A輸出保護（如果可用），但如果不可用則允許播放。 ACP上沒有保護。 AdobeAccess 2.0客戶端不支援此選項。 如果設定，AdobeAccess 2.0客戶端將像指定了「無保護」選項一樣運行。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">無保護</b>  — 對模擬和數字輸出不強制啟用輸出保護。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">無播放</b>  — 不允許對外部設備進行模擬和數字輸出回放。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">是 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>雖然這些規則在所有平台上都得到一致的強制執行，但目前只能在Windows平台上安全地啟用輸出保護。 在其他平台（如Macintosh和Linux）上，第三方應用程式沒有支援的作業系統功能。

示例用例：某些內容可能會強制實施輸出保護控制，而保護級別可由內容分發器設定。 如果指定了「必需」，並且在Macintosh上嘗試播放，則客戶端不會在外部設備上回放內容。 但是，內容將在內部顯示器上回放。

如果指定了「必需」，並且嘗試在Linux上播放，則客戶端不會在任何設備上播放內容，因為無法區分內部和外部設備。

如果指定「如果可用，則在可能的情況下啟用輸出保護。 例如，在支援認證輸出保護協定(COPP)的Windows電腦上，內容會通過輸出保護傳遞到外部顯示器。 此示例有時稱為「可選輸出控制」。
