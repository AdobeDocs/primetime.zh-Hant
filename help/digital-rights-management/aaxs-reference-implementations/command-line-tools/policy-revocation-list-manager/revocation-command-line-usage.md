---
title: 命令行用法
description: 命令行用法
copied-description: true
exl-id: b9e51bab-7bef-459f-bb4d-13ccc4add37a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 命令行用法 {#command-line-usage}

吊銷清單管理器位於DVD的\Reference Implementation\Command Line Tools目錄中。 要運行該工具，請使用以下語法之一：

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

* `destfile` 指示將寫入吊銷清單的位置。
* `crlNumber` 是證書吊銷清單(CRL)的非負版本號。 每次更新CRL時，該數字應遞增。

下表包含上述語法中所示的命令行選項的說明：

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
   <td colname="2" class="- topic/entry ">指定配置檔案的位置。 如果未使用此選項，則吊銷清單管理器將查找 <span class="filepath"> flashaccessols.properties</span> 的子菜單。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d檔案名</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">顯示有關吊銷清單的資訊。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e日期</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（可選）吊銷清單的到期日期。 使用格式 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> 或 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span> (例如，2009-01-31-14:30:00表示1月31日下午2:30)。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f檔案名[certfile]</span> </td> 
   <td colname="2" class="- topic/entry ">添加現有吊銷清單中的所有條目。 只能指定一個現有檔案。 <p class="- topic/p ">如果此現有清單使用與用於簽署新清單的憑據不同的憑據簽名，請指定其下一個證書檔案，以便驗證其簽名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要詢問是否應覆蓋目標檔案。 如果目標檔案已存在且未設定 — o，則將返回錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目標檔案已存在，則覆蓋它而不出現提示。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber revocationDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">撤消由 <span class="codeph"> 頒發者名稱</span> 和 <span class="codeph"> 序列號</span> 在給定日期。 的 <span class="codeph"> 頒發者名稱</span> 必須採用509名稱格式(例如， <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>)。 以十六進位形式指定序列號。 將吊銷日期指定為 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> 或 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span>，例如2008-12-1或2008-12-1-00:00:2008年12月1日午夜0點。 如果未指定吊銷日期，則使用當前日期。 </p> </td> 
  </tr> 
 </tbody> 
</table>
