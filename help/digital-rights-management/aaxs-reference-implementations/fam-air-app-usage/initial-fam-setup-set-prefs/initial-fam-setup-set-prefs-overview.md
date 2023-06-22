---
title: 設定偏好設定概述
description: 設定偏好設定概述
copied-description: true
exl-id: 9618a038-c5b0-4b49-8936-ef8fcacf2105
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# 設定偏好設定概述 {#setting-preferences-overview}

除了Packager伺服器URL之外，以下指定的所有偏好設定都會儲存在 [!DNL flashaccess-refimpl-packager.properties] 檔案時。 您可以直接在屬性檔案中或透過AIR應用程式修改所有設定。 當密碼儲存在伺服器上的屬性檔案中時，就會加以加密。 在UI中鍵入未加密的密碼，該密碼將在儲存到檔案之前加密。

>[!NOTE]
>
>所有目錄和路徑都參照封裝程式伺服器上的目錄，而不是執行AIR應用程式的使用者端上的目錄。

這裡所做的任何變更會在儲存偏好設定後立即生效。 除非封裝器執行緒因組態問題而終止，否則不需要重新啟動伺服器。

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
   <td colname="1" class="- topic/entry "> 封裝程式伺服器URL </td> 
   <td colname="2" class="- topic/entry "> 伺服器執行中的位置 <span class="filepath"> flashaccess-packager.war </span>；例如， <span class="filepath"> https://localhost:8080 </span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 資源目錄 </td> 
   <td colname="2" class="- topic/entry "> 包含封裝程式伺服器所需之原則、憑證、認證和任何其他資源的目錄 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 授權伺服器URL </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">使用者端應要求授權的伺服器URL；例如， <span class="filepath"> https://mylicenseserver.com:8080 </span> </p> </td> 
  </tr> 
 </tbody> 
</table>
