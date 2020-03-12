---
seo-title: 特定於供應商的安全資訊
title: 特定於供應商的安全資訊
uuid: 23186770-c73a-4802-bc30-fa9e4b47d9ba
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 特定於供應商的安全資訊{#vendor-specific-security-information}

本節包含與安全性相關的資訊，這些資訊與您的Adobe Access解決方案整合的作業系統和應用程式伺服器有關。

使用本節中提供的連結，查找作業系統和應用伺服器的特定於供應商的安全資訊。

## 作業系統安全性資訊 {#section-B6D9D6CEA7CC42A8A20346600EFB5E4E}

在確保作業系統安全時，請仔細實施作業系統供應商描述的措施，包括：

* 定義和控制用戶、角色和權限
* 監控日誌和審核記錄
* 移除不必要的服務和應用程式
* 備份檔案

如需Adobe Access支援之作業系統的安全性資訊，請參閱本表中的資源。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-ugl-kjz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">作業系統 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">安全資源 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Microsoft® Windows Server® 2008企業版或標準版 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Windows Server 2008安全指南</i> </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Red Hat® Enterprise Linux® 5.4、5.5和5.6。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Red Hat Enterprise Linux 5安全指南</i> </p> </td> 
  </tr> 
 </tbody> 
</table>

下表說明一些將作業系統中發現的安全性弱點降至最低的潛在方法。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-whl-kjz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">項目 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">安全性修補程式 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果未及時應用供應商安全補丁和升級，未經授權的用戶可能會獲得對應用程式伺服器的訪問，這一風險增加。 在將安全修補程式套用至生產伺服器之前，請先加以測試。 </p> <p class="- topic/p ">此外，建立策略和程式以定期檢查和安裝修補程式。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">病毒防護軟體 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">病毒掃描器可以通過掃描簽名或監視異常行為來識別感染病毒的檔案。 掃描器將其病毒簽名保存在檔案中，該檔案通常儲存在本地硬碟上。 由於新病毒經常被發現，因此您必須頻繁更新此檔案，病毒掃描程式才能識別所有當前病毒。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">網路時間協定(NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">為了進行正確的操作和取證分析，請在Adobe Access伺服器和Adobe Access封裝器上保持準確的時間。 使用NTP的安全版本來同步連接到Internet的所有系統上的時間。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 應用程式伺服器安全性資訊 {#section-EBB4EF371CFF4A848694CC240B23D404}

在保護應用程式伺服器時，必須實施伺服器供應商描述的措施，包括：

* 使用非顯而易見的管理員用戶名
* 禁用不必要的服務
* 保護控制台管理器
* 啟用安全Cookie
* 關閉不需要的埠
* 按IP地址或域限制管理介面
* 使用Java™ Security Manager

