---
description: 您的Adobe PrimetimeDRM解決方案中包含作業系統和應用程式伺服器。
title: 特定於供應商的安全資訊
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# 特定於供應商的安全資訊{#vendor-specific-security-information}

您的Adobe PrimetimeDRM解決方案中包含作業系統和應用程式伺服器。

要查找特定於供應商的作業系統和應用程式伺服器的安全資訊，請參閱使用Adobe PrimetimeDRM密鑰伺服器。

## 作業系統安全資訊{#section_53CAD802FCA54C4D8CE0C4E1B3045E52}

在確保作業系統安全時，必須實施作業系統供應商描述的措施。

以下是一些措施：

* 定義和控制用戶、角色和權限
* 監控日誌和審核記錄
* 移除不必要的服務和應用程式
* 備份檔案

以下是Adobe PrimetimeDRM支援的作業系統相關資訊：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ugl_kjz_n4"> 
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

以下提供一些有關將作業系統中的安全性弱點降至最低的方法：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_whl_kjz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">項目 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">安全性修補程式 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果供應商未及時應用安全補丁和升級，未經授權的用戶可能會獲得對應用程式伺服器的訪問，這一風險增加。 </p> <p>注意： 請務必先測試安全性修補程式，然後再將它們套用至生產伺服器。 </p> <p class="- topic/p ">您必須建立策略和程式，以定期檢查和安裝修補程式。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">病毒防護軟體 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">病毒掃描器可以通過掃描簽名或異常行為來識別感染病毒的檔案。 </p> <p>掃描器將其病毒簽名保存在檔案中，該檔案通常儲存在本地硬碟上。 新病毒經常被發現，因此您必須確保定期更新此檔案。 這樣，病毒掃描器就可以隨時識別所有當前病毒。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">網路時間協定(NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">為獲得正確的操作和取證分析，請在Primetime DRM伺服器和封裝器上保持準確的時間。 使用安全版NTP來同步所有連接到Internet的系統上的Primetime DRM時間。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 應用程式伺服器安全資訊{#section_22986936F1A547CEAB2D97E9E9D4825C}

在保護應用程式伺服器時，必須實施伺服器供應商描述的措施。

以下是一些措施：

* 使用非顯而易見的管理員用戶名
* 禁用不必要的服務
* 保護控制台管理器
* 啟用安全Cookie
* 關閉不需要的埠
* 按IP地址或域限制管理介面
* 使用Java™ Security Manager

