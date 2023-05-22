---
title: 設定首選項概述
description: 設定首選項概述
copied-description: true
exl-id: 9618a038-c5b0-4b49-8936-ef8fcacf2105
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# 設定首選項概述 {#setting-preferences-overview}

除Packager Server URL外，下面指定的所有首選項都儲存在 [!DNL flashaccess-refimpl-packager.properties] 檔案。 可以直接在屬性檔案中或通過AIR應用程式修改所有設定。 密碼儲存在伺服器的屬性檔案中時會進行加密。 在UI中鍵入未加密的密碼，並在將其儲存在檔案中之前對其進行加密。

>[!NOTE]
>
>所有目錄和路徑都指Packager伺服器上的目錄，而不是運行AIR應用程式的客戶端上的目錄。

此處所做的任何更改在保存首選項後立即生效。 無需重新啟動伺服器，除非Packager線程因配置問題而終止。

首選項說明使用以下術語：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_tj5_hcz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 首選項 </th> 
   <th colname="2" class="- topic/entry entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 打包伺服器URL </td> 
   <td colname="2" class="- topic/entry "> 運行伺服器的位置 <span class="filepath"> 手提電話打包器.war </span>;比如說， <span class="filepath"> https://localhost:8080 </span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 資源目錄 </td> 
   <td colname="2" class="- topic/entry "> 包含打包伺服器所需的策略、證書、憑據和任何其他資源的目錄 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 許可證伺服器URL </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">客戶端應從其請求許可證的伺服器的URL;比如說， <span class="filepath"> https://mylicenseserver.com:8080 </span> </p> </td> 
  </tr> 
 </tbody> 
</table>
