---
title: 設定偏好設定概觀
description: 設定偏好設定概觀
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# 設定首選項概述{#setting-preferences-overview}

除了Packager Server URL之外，下面指定的所有首選項都儲存在伺服器的[!DNL flashaccess-refimpl-packager.properties]檔案中。 您可以直接在屬性檔案或透過AIR應用程式修改所有設定。 密碼儲存在伺服器的屬性檔案中時會進行加密。 在UI中輸入未加密的密碼，並在密碼儲存在檔案中之前加密。

>[!NOTE]
>
>所有目錄和路徑都指封裝伺服器上的目錄，而非執行AIR應用程式的用戶端上的目錄。

此處所做的任何變更，在儲存偏好設定後，都會立即生效。 除非Packager線程因配置問題而終止，否則無需重新啟動伺服器。

偏好設定說明使用下列詞語：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_tj5_hcz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 偏好設定 </th> 
   <th colname="2" class="- topic/entry entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> Packager Server URL </td> 
   <td colname="2" class="- topic/entry "> 運行<span class="filepath"> flashaccess-packager.war </span>的伺服器位置；例如<span class="filepath"> https://localhost:8080 </span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 資源目錄 </td> 
   <td colname="2" class="- topic/entry "> 包含策略、證書、憑據以及打包伺服器所需的任何其他資源的目錄 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 授權伺服器URL </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用戶端應向其請求授權之伺服器的URL;例如，<span class="filepath"> https://mylicenseserver.com:8080 </span> </p> </td> 
  </tr> 
 </tbody> 
</table>

