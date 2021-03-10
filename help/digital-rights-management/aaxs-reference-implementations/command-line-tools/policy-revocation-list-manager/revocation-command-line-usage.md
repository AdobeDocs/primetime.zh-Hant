---
title: 命令列使用
description: 命令列使用
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# 命令行用法{#command-line-usage}

「撤銷清單管理器」位於DVD的\Reference Implementation\Command Line Tools目錄中。 若要執行工具，請使用下列其中一種語法：

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

* `destfile` 指出將寫入撤銷清單的位置。
* `crlNumber` 是「證書撤銷清單」(CRL)的非負版本號。每次更新CRL時，此數字應遞增。

下表包含上述語法中所示命令行選項的說明：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_a3y_wqy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 命令行選項 </th> 
   <th colname="2" class="- topic/entry entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c配置檔案</span> </td> 
   <td colname="2" class="- topic/entry ">指定配置檔案的位置。 如果未使用此選項，「撤銷清單管理員」將在工作目錄中尋找<span class="filepath"> flashaccessools.properties</span>。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d檔案名</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">顯示關於撤銷清單的資訊。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e日期</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（選擇性）撤銷清單的到期日。 使用格式<span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span>或<span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span>（例如，2009-01-31-14:30:00代表1月31日2:30 PM）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f檔案名[certfile]</span> </td> 
   <td colname="2" class="- topic/entry ">從現有撤銷清單新增所有項目。 只能指定一個現有檔案。 <p class="- topic/p ">如果此現有清單的簽署憑證與用來簽署新清單的憑證不同，請指定其下一個憑證檔案，以驗證其簽名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">請勿詢問是否應覆寫目標檔案。 如果目標檔案已存在且未設定-o，則將返回錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目標檔案已存在，請不提示而覆寫它。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber revocationDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在指定日期廢止<span class="codeph"> issuberName</span>和<span class="codeph"> serialNumber</span>所識別的憑證。 <span class="codeph"> issuberName</span>必須遵循509名稱格式(例如，<span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>)。 以十六進位形式指定序列號。 將撤銷日期指定為<span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span>或<span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span>，例如2008-12-1或2008-12-1-00:00:00的午夜。08. 如果未指定撤銷日期，則會使用目前日期。 </p> </td> 
  </tr> 
 </tbody> 
</table>

