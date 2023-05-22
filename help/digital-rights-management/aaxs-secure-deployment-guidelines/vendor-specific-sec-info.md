---
title: 特定於供應商的安全資訊
description: 特定於供應商的安全資訊
copied-description: true
exl-id: 668321c5-b2c7-4bb3-9f68-2dba622a54de
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 特定於供應商的安全資訊{#vendor-specific-security-information}

本節包含與Adobe訪問解決方案中整合的作業系統和應用程式伺服器相關的安全資訊。

使用本節中提供的連結可以查找作業系統和應用程式伺服器的特定於供應商的安全資訊。

## 作業系統安全資訊 {#section-B6D9D6CEA7CC42A8A20346600EFB5E4E}

在保護作業系統時，請仔細實施作業系統供應商描述的措施，包括：

* 定義和控制用戶、角色和權限
* 監視日誌和審計跟蹤
* 刪除不必要的服務和應用程式
* 備份檔案

有關Adobe訪問支援的作業系統的安全資訊，請參見下表中的資源。

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">《 Red Hat Enterprise Linux 5安全指南》</i> </p> </td> 
  </tr> 
 </tbody> 
</table>

下表介紹了一些可能的方法，以最大限度地減少作業系統中的安全漏洞。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-whl-kjz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">物料 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">安全修補程式 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果供應商安全補丁程式和升級未及時應用，則未經授權的用戶可能獲得對應用程式伺服器的訪問權限的風險增加。 Test安全修補程式，然後將其應用到生產伺服器。 </p> <p class="- topic/p ">此外，建立策略和過程以定期檢查和安裝修補程式。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">病毒防護軟體 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">病毒掃描程式可以通過掃描簽名或監視異常行為來識別受感染的檔案。 掃描程式將其病毒簽名保留在檔案中，該檔案通常儲存在本地硬碟上。 由於經常發現新病毒，因此必須經常更新此檔案，以便病毒掃描程式識別所有當前病毒。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">網路時間協定(NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">為了進行正確的操作和取證分析，請在Adobe訪問伺服器和Adobe訪問包上保持準確的時間。 使用安全版本的NTP來同步連接到Internet的所有系統上的時間。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 應用程式伺服器安全資訊 {#section-EBB4EF371CFF4A848694CC240B23D404}

在保護應用程式伺服器時，必須實施伺服器供應商描述的度量，包括：

* 使用非顯而易見的管理員用戶名
* 禁用不必要的服務
* 保護控制台管理器
* 啟用安全Cookie
* 關閉不需要的埠
* 按IP地址或域限制管理介面
* 使用Java™ Security Manager
