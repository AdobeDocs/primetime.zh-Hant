---
title: 命令列使用方式
description: 命令列使用方式
copied-description: true
exl-id: 4c772010-b7b6-4655-98ee-b52e8022d4af
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 命令列使用方式 {#command-line-usage}

原則更新清單管理員位於DVD上的\Reference Implementation\Command Line Tools目錄中。 若要建立原則更新清單，請使用下列語法：

```
    java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` 指出寫入原則更新清單的位置。

若要檢視現有的原則更新清單，請使用下列語法：

```
    java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

下表包含上述語法中所顯示的命令列選項說明：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令列選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c設定檔 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定組態檔的位置。 如果未使用此選項，原則更新清單管理員將會尋找 <span class="filepath"> flashaccesstools.properties </span> 於工作目錄中。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d檔案名稱 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">顯示原則更新清單的相關資訊。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e日期 </span> </td> 
   <td colname="2" class="- topic/entry "> （選用）原則更新清單的到期日。 使用格式 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span> (例如，2009-01-31-14:30:00代表1月31日下午2:30)。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f檔案名稱[certfile] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">從現有原則更新清單新增所有專案。 只能指定一個現有檔案。 </p> <p class="- topic/p ">如果此現有清單使用與用來簽署新清單的憑證不同的憑證簽名，請指定其憑證檔案，以便可以驗證其簽名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要詢問是否應該覆寫目的地檔案。 如果目的地檔案已存在且 <span class="codeph"> -o </span> 未設定，則會傳回錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目的地檔案已經存在，請覆寫它而不提示。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyID </span> <span class="+ topic/ph pr-d/codeph codeph"> 日期 </span> " <span class="+ topic/ph pr-d/codeph codeph"> 原因代碼 </span>「 」 <span class="+ topic/ph pr-d/codeph codeph"> 原因文字 </span>「 」 <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（選用）在指定的日期撤銷原則ID。 也可以提供選擇性的原因代碼、原因文字和原因URL。 指定空字串「」以表示未提供選擇性引數的值。 指定日期為 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span> (例如2008-12-1或2008-12-1-00:00:00 （2008年12月1日午夜）。 如果未指定日期，則會使用目前的日期。 原因代碼必須大於或等於0。 可以指定多個 — r選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> 日期 </span> " <span class="+ topic/ph pr-d/codeph codeph"> 原因代碼 </span>「 」 <span class="+ topic/ph pr-d/codeph codeph"> 原因文字 </span>「 」 <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">執行與 — r標幟相同的動作，但會從指定的檔案中擷取原則識別碼。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" " reasonURL" </span> </td> 
   <td colname="2" class="- topic/entry "> <p>使用指定的原因代碼（選擇性）、原因文字（選擇性）和原因URL （選擇性），以這個原則取代授權請求中的任何相符原則。 </p> <p>指定空字串「」以表示未提供選擇性引數的值。 </p> <p>原因代碼必須大於或等於 <span class="codeph"> 0 </span>. 多個 <span class="codeph"> -u </span> 可指定選項。 </p> </td> 
  </tr> 
 </tbody> 
</table>
