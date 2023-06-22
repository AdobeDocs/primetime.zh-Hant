---
description: Adobe Primetime DRM解決方案包含作業系統和應用程式伺服器。
title: 廠商特定安全性資訊
exl-id: 4cc39414-cab5-4282-825d-64651d9b03e1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# 廠商特定安全性資訊{#vendor-specific-security-information}

Adobe Primetime DRM解決方案包含作業系統和應用程式伺服器。

若要尋找您作業系統和應用程式伺服器的廠商特定安全性資訊，請參閱使用Adobe Primetime DRM金鑰伺服器。

## 作業系統安全性資訊 {#section_53CAD802FCA54C4D8CE0C4E1B3045E52}

保護作業系統時，您必須實作作業系統供應商所說明的措施。

以下是一些措施：

* 定義和控制使用者、角色和許可權
* 監控日誌和稽核追蹤
* 移除不必要的服務和應用程式
* 備份檔案

以下是Adobe Primetime DRM支援之作業系統的相關資訊：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ugl_kjz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">作業系統 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">安全性資源 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Microsoft® Windows Server® 2008企業版或標準版 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Windows Server 2008安全性指南</i> </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Red Hat® Enterprise Linux® 5.4、5.5和5.6。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Red Hat Enterprise Linux 5安全性指南</i> </p> </td> 
  </tr> 
 </tbody> 
</table>

以下提供作業系統中最大程度降低安全性弱點的方法相關資訊：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_whl_kjz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">專案 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">安全性修補程式 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果未及時套用廠商安全性修補程式和升級，未經授權的使用者可能會取得應用程式伺服器的存取權，此風險會增加。 </p> <p>注意：請確定您在將安全性修補程式套用至生產伺服器之前，先測試這些修補程式。 </p> <p class="- topic/p ">您必須建立原則和程式，以定期檢查並安裝修補程式。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">病毒防護軟體 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">病毒掃描程式可透過掃描特徵碼或異常行為來識別受感染的檔案。 </p> <p>掃描器會將其病毒簽章儲存在檔案中，檔案通常會儲存在本機硬碟中。 新病毒經常被發現，因此您必須確保此檔案定期更新。 如此一來，病毒掃描程式就能夠識別所有目前的病毒。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">網路時間通訊協定(NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">為了正確操作及進行鑑證分析，請保持Primetime DRM伺服器和封裝器的正確時間。 使用安全的NTP版本，同步所有連線至網際網路的系統上的Primetime DRM時間。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 應用程式伺服器安全性資訊 {#section_22986936F1A547CEAB2D97E9E9D4825C}

保護應用程式伺服器時，您必須實作伺服器供應商所述的措施。

以下是其中一些測量：

* 使用不顯眼的管理員使用者名稱
* 停用不必要的服務
* 保護主控台管理員
* 啟用安全Cookie
* 關閉不需要的連線埠
* 依IP位址或網域限制管理介面
* 使用Java™安全管理員
