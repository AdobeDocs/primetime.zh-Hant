---
title: 命令列使用方式
description: 命令列使用方式
copied-description: true
exl-id: 2142cb76-e71c-4443-8b5d-348e45587331
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 0%

---

# 命令列使用方式 {#command-line-usage}

在使用Policy Manager之前，請確定您符合需求中列出的需求。

原則管理員位於 [!DNL \Reference Implementation\Command Line Tools] 目錄。 若要執行工具，請使用下列語法：

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

下表包含上述語法中所顯示的命令列動作說明：

| 命令列動作 | 說明 |
|---|---|
| `new` | 建立新原則。 |
| `detail` | 說明現有的原則。 |
| `update` | 更新現有原則。 |

下表說明可與上述語法一起指定的命令列選項：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令列選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c設定檔 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定組態檔的位置。 如果未使用此選項，原則管理員將會尋找 <span class="filepath"> flashaccesstools.properties </span> 於工作目錄中。 命令列上指定的選項優先於組態檔案中的選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目的地檔案已經存在，請覆寫它而不提示。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要詢問是否應該覆寫目的地檔案。 如果目的地檔案已存在且 <span class="codeph"> -o </span> 未設定，則會傳回錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">表示原則具有根授權。 不允許更新。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權有效之前的日期。 指定為 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span>. 例如，2008-12-1或2008-12-1-00:00:00 （2008年12月1日午夜）。 值必須大於下列專案的值： <span class="codeph"> -s </span>，如果有的話。 此選項無法搭配 <span class="codeph"> -r </span>. 若要在更新原則時移除結束日期，請使用 <span class="codeph"> -e </span> 而不指定日期。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r分鐘 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">受此原則保護的內容有效期（分鐘），從內容受封裝程式保護時開始。 值必須為非負數。 此選項無法搭配 <span class="codeph"> -e </span>. 若要移除更新原則時的持續時間，請使用 <span class="codeph"> -r </span> 而不指定分鐘數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權有效期的截止日期。 指定為 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span>. 例如，2008-12-1或2008-12-1-00:00:00 （2008年12月1日午夜）。 值必須小於的值 <span class="codeph"> -e </span>，如果有的話。 此選項無法搭配 <span class="codeph"> -r </span>. 若要在更新原則時移除開始日期，請使用 <span class="codeph"> -s </span> 而不指定日期。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w分鐘 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">播放視窗（從第一次播放開始可檢視內容的分鐘數）。 如果未指定此選項，或 <span class="codeph"> -w </span> 使用，而不指定分鐘數，沒有播放視窗限制。 值必須為非負數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l分鐘 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權快取持續時間（以分鐘為單位），即伺服器簽發授權後，允許在使用者端的授權存放區中快取授權的時間。 值必須為非負數。 指定 <span class="codeph"> -l 0 </span> 表示不允許授權快取。 使用 <span class="codeph"> -l </span> 而不指定無限制授權快取的分鐘數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -ldate日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權快取結束日期（伺服器發出授權後，使用者端的「授權存放區」中不可快取授權的日期）。 指定為 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span><i class="+ topic/ph hi-d/i "> </i>或<i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span>. 例如，2008-12-1或2008-12-1-00:00:00 （2008年12月1日午夜）。 使用 <span class="codeph"> -l </span> 而不指定無限制授權快取的分鐘數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">驗證名稱空間。 若指定，使用者端應使用指定授權單位所簽發的使用者名稱和密碼進行驗證。 此選項無法搭配 <span class="codeph"> -x </span>. 不允許更新。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許匿名存取。 此選項無法搭配 <span class="codeph"> -authNS </span>. 不允許更新。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId </span>[： <span class="+ topic/ph pr-d/codeph codeph"> appId </span>[：[ <span class="+ topic/ph pr-d/codeph codeph"> 分鐘 </span>]：[ <span class="+ topic/ph pr-d/codeph codeph"> max </span>]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許播放受保護內容的AIR應用程式允許清單。 使用此選項來限制哪些發行者、應用程式和版本可以存取受此原則保護的內容。 </p> <p class="- topic/p ">若 <i class="+ topic/ph hi-d/i ">appId</i> 未指定，發行者的所有應用程式 <i class="+ topic/ph hi-d/i ">pubId</i> 允許。 </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">分鐘</i> 和 <i class="+ topic/ph hi-d/i ">max</i> 版本編號為選用。 </p> <p class="- topic/p ">多個 <span class="codeph"> -air </span> 可以指定選項以允許多個應用程式。 如果未指定AIR或SWF應用程式，則所有應用程式都可以存取此內容。 在更新期間，使用 — air （不含其餘引數）從清單中移除所有專案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drm黑名單名稱 </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 配對 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM使用者端無法存取受保護的內容。 值包含逗號分隔的名稱：值配對，格式如下： </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> 作業系統 |版本= stringValue </span> </p> <p class="- topic/p ">例如， <span class="codeph"> os=Win，release=2.0.1 </span>. 在更新期間，使用 <span class="codeph"> -drm黑名單 </span> 不含其餘引數，即可從清單中移除所有專案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指出DRM使用者端必須具有指定的最低安全性層級，才能存取受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog無保護 | USE_IF_AVAILABLE |必填 |無播放(_P) | ACP_REQUIRED | CGMS-A_REQUIRED | USE_ACP_IF_AVAILABLE | USE_CGMS-A_IF_AVAILABLE </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">類比輸出保護限制。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECT | USE_IF_AVAILABLE |必填 |無播放(_P) </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">數位輸出保護限制。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist名稱 </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 配對 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">應用程式執行階段無法存取受保護的內容。 值包含逗號分隔的名稱：值配對，格式如下： </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> 作業系統 |應用程式 |版本= stringValue </span> </p> <p class="- topic/p ">例如， <span class="codeph"> os=Win，release=2.0.1，application=AIR </span>. 在更新期間，使用 <span class="codeph"> -runtimeBlacklist </span> 不含其餘引數，即可從清單中移除所有專案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指出應用程式執行階段必須具備指定的最低安全性層級，才能存取受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf檔案= swf檔案 </span>， <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許播放受保護內容的SWF應用程式允許清單。 可以指定多個 — swf選項以允許多個應用程式。 如果未指定AIR或SWF應用程式，則所有應用程式都可以存取此內容。 在更新期間，使用 — swf （不含其餘引數）從清單中移除所有專案。 若要透過雜湊值來識別SWF，請指定要計算雜湊的SWF檔案，以及允許SWF驗證完成的最長時間（以秒為單位）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name= value </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要新增到原則的自訂索引鍵/值。 多個 <span class="codeph"> -k </span> 可指定選項。 在更新期間，使用 <span class="codeph"> -k </span> 不保留引數，以移除所有屬性。 此資料的解譯或處理完全取決於Adobe存取授權伺服器的實作。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p name= value </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">新增自訂屬性，該屬性將顯示在每個使用者端產生的授權中。 多個 <span class="codeph"> -p </span> 可以指定選項以新增多個屬性。 在更新期間，使用 <span class="codeph"> -p </span> 不保留引數，以移除所有屬性。 此資料的解譯或處理完全取決於使用者端應用程式的實作。 </p> </td> 
  </tr> 
 </tbody> 
</table>
