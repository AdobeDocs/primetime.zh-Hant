---
title: 廠商特定的安全性資訊
description: 廠商特定的安全性資訊
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 廠商特定的安全性資訊{#vendor-specific-security-information}

本節包含整合至Adobe存取解決方案之作業系統和應用程式伺服器的安全性相關資訊。

使用本節提供的連結，尋找您作業系統和應用程式伺服器的特定廠商安全性資訊。

## 作業系統安全性資訊 {#section-B6D9D6CEA7CC42A8A20346600EFB5E4E}

保護作業系統的安全時，請謹慎執行作業系統供應商所說明的措施，包括：

* 定義和控制使用者、角色和許可權
* 監控日誌和稽核軌跡
* 移除不必要的服務和應用程式
* 備份檔案

如需「Adobe存取」支援之作業系統的安全性資訊，請參閱此表格中的資源。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-ugl-kjz-n4"> 
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

下表說明將作業系統中發現的安全性弱點降到最低的一些可能方法。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-whl-kjz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">專案 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">安全性修補程式 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果未及時套用廠商安全性修補程式和升級，未經授權的使用者可能會取得應用程式伺服器的存取權，此風險會增加。 請先測試安全性修補程式，再將其套用至生產伺服器。 </p> <p class="- topic/p ">此外，建立原則和程式，以定期檢查並安裝修補程式。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">病毒防護軟體 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">病毒掃描程式可透過掃描簽名或監視異常行為來識別受感染的檔案。 掃描器會將病毒簽章儲存在檔案中，檔案通常儲存在本機硬碟上。 因為經常發現新病毒，您必須經常更新這個檔案，病毒掃描程式才能識別所有目前的病毒。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">網路時間通訊協定(NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">為了進行正確的作業和鑑證分析，請務必在Adobe存取伺服器和Adobe存取封裝上保持準確的時間。 使用安全的NTP版本，同步所有連線至網際網路的系統上的時間。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 應用程式伺服器安全性資訊 {#section-EBB4EF371CFF4A848694CC240B23D404}

保護應用程式伺服器的安全時，您必須實作伺服器供應商所說明的措施，包括：

* 使用不明顯的管理員使用者名稱
* 停用不必要的服務
* 保護主控台管理員
* 啟用安全Cookie
* 關閉不需要的連線埠
* 依IP位址或網域限制管理介面
* 使用Java™安全管理員
