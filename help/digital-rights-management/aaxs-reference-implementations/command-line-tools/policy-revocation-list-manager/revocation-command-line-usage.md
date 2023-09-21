---
title: 命令列使用方式
description: 命令列使用方式
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 命令列使用方式 {#command-line-usage}

[撤銷清單管理員]位於DVD的\Reference Implementation\Command Line Tools目錄中。 若要執行此工具，請使用下列其中一種語法：

```
    java -jar AdobeRevocationListManager.jar 
<i class="+ topic ph hi-d="" i "="">
 destfile 
 <i class="+ topic ph hi-d="" i "="">
  crlNumber [
  <i class="+ topic ph hi-d="" i "="">
   options] 
       java -jar AdobeRevocationListManager.jar -d 
   <i class="+ topic ph hi-d="" i "="">
     filename
   </i class="+ topic>
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `destfile` 表示將寫入撤銷清單的位置。
* `crlNumber` 是憑證撤銷清單(CRL)的非負數版本號碼。 每次更新CRL時，此數字都會增加。

下表包含上述語法中所顯示的命令列選項說明：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_a3y_wqy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 命令列選項 </th> 
   <th colname="2" class="- topic/entry entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c設定檔</span> </td> 
   <td colname="2" class="- topic/entry ">指定組態檔的位置。 如果未使用此選項，「撤銷清單管理員」將會尋找 <span class="filepath"> flashaccesstools.properties</span> 於工作目錄中。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d檔案名稱</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">顯示撤銷清單的相關資訊。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e日期</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（選用）撤銷清單的到期日。 使用格式 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> 或 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span> (例如：2009-01-31-14:30:00代表1月31日下午2:30)。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f filename[certfile]</span> </td> 
   <td colname="2" class="- topic/entry ">從現有的撤銷清單新增所有專案。 只能指定一個現有檔案。 <p class="- topic/p ">如果這個現有清單的簽署憑證與用來簽署新清單的憑證不同，請接著指定其憑證檔案，以便驗證其簽章。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要詢問是否應該覆寫目的地檔案。 如果目的地檔案已經存在，但未設定 — o，則會傳回錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目的地檔案已經存在，則覆寫它而不進行提示。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber撤銷日期</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">撤銷由以下識別出的憑證： <span class="codeph"> issuerName</span> 和 <span class="codeph"> 序號</span> 在指定日期。 此 <span class="codeph"> issuerName</span> 必須遵循509名稱格式(例如 <span class="codeph"> CN=12345，O=Adobe Systems Incorporated，C=US</span>)。 以十六進位格式指定序號。 將撤銷日期指定為 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> 或 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span>，例如2008-12-1或2008-12-1-00:00:2008年12月1日午夜00。 如果未指定撤銷日期，則會使用目前的日期。 </p> </td> 
  </tr> 
 </tbody> 
</table>
