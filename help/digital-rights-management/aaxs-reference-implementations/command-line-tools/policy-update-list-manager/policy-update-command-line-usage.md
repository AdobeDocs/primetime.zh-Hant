---
title: 命令列使用
description: 命令列使用
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# 命令行用法{#command-line-usage}

策略更新清單管理器位於DVD的\Reference Implementation\Command Line Tools目錄中。 要建立策略更新清單，請使用以下語法：

```
    java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` 指示將寫入策略更新清單的位置。

要查看現有策略更新清單，請使用以下語法：

```
    java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

下表包含上述語法中所示命令行選項的說明：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c配置檔案  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置檔案的位置。 如果未使用此選項，「策略更新清單管理器」將在工作目錄中查找<span class="filepath"> flashaccessools.properties </span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d檔案名  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">顯示有關策略更新清單的資訊。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e日期  </span> </td> 
   <td colname="2" class="- topic/entry "> （可選）原則更新清單的到期日。 使用格式<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span>或<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>（例如，2009-01-31-14:30:00代表1月31日下午2:30）。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f檔案名[certfile]  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">從現有策略更新清單中添加所有條目。 只能指定一個現有檔案。 </p> <p class="- topic/p ">如果此現有清單的簽署憑證與用來簽署新清單的憑證不同，請指定其憑證檔案，以驗證其簽名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">請勿詢問是否應覆寫目標檔案。 如果目標檔案已存在且未設定<span class="codeph"> -o </span> ，則將返回錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目標檔案已存在，請不提示而覆寫它。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyDATE  </span> <span class="+ topic/ph pr-d/codeph codeph"> date  </span> reasonCode " " "  <span class="+ topic/ph pr-d/codeph codeph"> reasonText  </span>" "reasonURL  <span class="+ topic/ph pr-d/codeph codeph">  </span> <span class="+ topic/ph pr-d/codeph codeph">  </span>ID" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（可選）在指定日期廢止原則ID。 也可能提供可選的原因代碼、原因文字和原因URL。 指定空字串""，以指出未提供任何選用參數的值。 將日期指定為<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span>或<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>（例如2008-12-1或2008-1-00:00:00的午夜，於2001年12月1日8）。 如果未指定日期，則會使用目前日期。 原因代碼必須大於或等於0。 可以指定多個-r選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> date </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">執行與-r標誌相同的操作，但從給定檔案中提取策略標識符。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" " reasonURL"  </span> </td> 
   <td colname="2" class="- topic/entry "> <p>使用指定的原因碼（選用）、原因文字（選用）和原因URL（選用），將授權要求中的任何符合原則取代為此原則。 </p> <p>指定空字串""，以指出未提供任何選用參數的值。 </p> <p>原因代碼必須大於或等於<span class="codeph"> 0 </span>。 可以指定多個<span class="codeph"> -u </span>選項。 </p> </td> 
  </tr> 
 </tbody> 
</table>

