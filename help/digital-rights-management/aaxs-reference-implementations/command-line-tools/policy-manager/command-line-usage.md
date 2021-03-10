---
title: 命令列使用
description: 命令列使用
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 0%

---


# 命令行用法{#command-line-usage}

在使用策略管理器之前，請確保您滿足「要求」中列出的要求。

策略管理器位於DVD上的[!DNL \Reference Implementation\Command Line Tools]目錄中。 若要執行工具，請使用下列語法：

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

下表包含上述語法中所示命令行操作的說明：

| 命令行操作 | 說明 |
|---|---|
| `new` | 建立新策略。 |
| `detail` | 說明現有原則。 |
| `update` | 更新現有原則。 |

下表說明了可以指定的命令行選項以及上述語法：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c配置檔案  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置檔案的位置。 如果未使用此選項，策略管理器將在工作目錄中查找<span class="filepath"> flashaccessools.properties </span>。 命令行上指定的選項優先於配置檔案中顯示的選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目標檔案已存在，請不提示而覆寫它。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">請勿詢問是否應覆寫目標檔案。 如果目標檔案已存在且未設定<span class="codeph"> -o </span> ，則將返回錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">表示策略具有根許可證。 不允許更新。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e日期  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權生效的日期。 指定為<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span>或<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>。 例如，2008年12月1日午夜的2008-12-1或2008-12-1-00:00:00。 值必須大於<span class="codeph"> -s </span>的值（如果存在）。 此選項不能與<span class="codeph"> -r </span>一起使用。 要在更新策略時刪除結束日期，請使用<span class="codeph"> -e </span>而不指定日期。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r分鐘  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">使用此原則保護的內容的有效期間（分鐘），從使用封裝程式保護內容時開始。 值必須是非負值。 此選項不能與<span class="codeph"> -e </span>一起使用。 要在更新策略時刪除持續時間，請使用<span class="codeph"> -r </span> ，但不指定分鐘數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s日期  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權的有效日期。 指定為<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span>或<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>。 例如，2008年12月1日午夜的2008-12-1或2008-12-1-00:00:00。 值必須小於<span class="codeph"> -e </span>的值（如果存在）。 此選項不能與<span class="codeph"> -r </span>一起使用。 要在更新策略時刪除開始日期，請使用<span class="codeph"> -s </span>而不指定日期。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w分鐘  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">播放視窗（從第一次播放開始，可檢視內容的分鐘數）。 如果未指定此選項，或如果使用<span class="codeph"> -w </span>而未指定分鐘數，則沒有播放窗口限制。 值必須是非負值。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l分鐘  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權快取持續時間（以分鐘為單位），即在伺服器核發授權後，授權可在用戶端的授權商店中快取的時間。 值必須是非負值。 指定<span class="codeph"> -l 0 </span>以表示不允許授權快取。 使用<span class="codeph"> -l </span>，但不需為無限制的授權快取指定分鐘數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -ldate  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權快取結束日期（在伺服器核發授權後，授權不得快取至用戶端的License Store的日期）。 指定為<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span><i class="+ topic/ph hi-d/i "> </i>或<i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> &lt;yyyy-mm-dd-h24:min:sec </span>。 例如，2008年12月1日午夜的2008-12-1或2008-12-1-00:00:00。 使用<span class="codeph"> -l </span>，但不需為無限制的授權快取指定分鐘數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">驗證命名空間。 如果指定，則客戶端應使用由指定授權機構發出的用戶名和密碼進行身份驗證。 此選項不能與<span class="codeph"> -x </span>一起使用。 不允許更新。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許匿名存取。 此選項不能與<span class="codeph"> -authNS </span>一起使用。 不允許更新。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId  </span>[: <span class="+ topic/ph pr-d/codeph codeph"> appId  </span>[:[ <span class="+ topic/ph pr-d/codeph codeph"> 最 </span>小]:[最大 <span class="+ topic/ph pr-d/codeph codeph">  </span>值]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許播放受保護內容的AIR應用程式清單。 使用此功能來限制哪些發佈者、應用程式和版本可存取使用此原則保護的內容。 </p> <p class="- topic/p ">如果未指定<i class="+ topic/ph hi-d/i ">appId</i>，則允許發佈者<i class="+ topic/ph hi-d/i ">pubId</i>的所有應用程式。 </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">min和</i>  <i class="+ topic/ph hi-d/i "></i> maxversion編號是可選的。 </p> <p class="- topic/p ">可以指定多個<span class="codeph"> -air </span>選項以允許多個應用程式。 如果未指定AIR或SWF應用程式，所有應用程式都可存取此內容。 在更新期間，請使用-air（不含其餘引數）來移除清單中的所有項目。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmBlacklist名稱 </span> <i class="+ topic/ph hi-d/i ">/值</i> <span class="+ topic/ph pr-d/codeph codeph"> 對 </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 數  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM客戶端被限制訪問受保護的內容。 值由逗號分隔的名稱：值對組成，格式如下： </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | release= stringValue  </span> </p> <p class="- topic/p ">例如，<span class="codeph"> os=Win,release=2.0.1 </span>。 在更新期間，使用<span class="codeph"> -drmBlacklist </span>（不含其餘引數）從清單中刪除所有條目。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指出DRM用戶端必須具備指定的最低安全等級才能存取受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog NO_PROTECTION | USE_IF_AVAILABLE |必要 | NO_PLAYBACK | ACP_REQUIRED | CGMS-A_REQUIRED | USE_ACP_IF_AVAILABLE | USE_CGMS-A_IF_AVAILABLE  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">模擬輸出保護限制。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE |必要 | NO_PLAYBACK  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">數位輸出保護限制。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist名稱 </span> <i class="+ topic/ph hi-d/i ">/值</i> <span class="+ topic/ph pr-d/codeph codeph"> 對的 </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 名  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">應用程式執行時期無法存取受保護的內容。 值由逗號分隔的名稱：值對組成，格式如下： </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os |應用程式 | release= stringValue  </span> </p> <p class="- topic/p ">例如，<span class="codeph"> os=Win,release=2.0.1,application=AIR </span>。 在更新期間，使用<span class="codeph"> -runtimeBlacklist </span>（不含其餘引數）來從清單中刪除所有條目。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指出應用程式執行時期必須具備指定的最低安全等級才能存取受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url  </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf file= swf_file </span>,  <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許播放受保護內容的SWF應用程式清單。 可以指定多個-swf選項以允許多個應用程式。 如果未指定AIR或SWF應用程式，所有應用程式都可存取此內容。 在更新期間，請使用-swf（不含其餘引數）來移除清單中的所有項目。 若要依其雜湊值來識別SWF，請指定要計算雜湊的SWF檔案，以及允許完成SWF驗證的最長時間（以秒為單位）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k名稱=值  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要添加到策略的自定義密鑰／值。 可以指定多個<span class="codeph"> -k </span>選項。 在更新期間，使用<span class="codeph"> -k </span>（不含其餘參數）來刪除所有屬性。 此資料的解譯或處理完全取決於Adobe存取授權伺服器的實作。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p名稱=值  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">新增自訂屬性，該屬性會顯示在為每個用戶端產生的授權中。 可以指定多個<span class="codeph"> -p </span>選項來添加多個屬性。 在更新期間，請使用<span class="codeph"> -p </span>而不使用其餘參數來刪除所有屬性。 此資料的解讀或處理完全由用戶端應用程式的實作決定。 </p> </td> 
  </tr> 
 </tbody> 
</table>

