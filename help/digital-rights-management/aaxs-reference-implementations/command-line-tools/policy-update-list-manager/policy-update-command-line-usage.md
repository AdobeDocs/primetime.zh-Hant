---
title: 命令行用法
description: 命令行用法
copied-description: true
exl-id: 4c772010-b7b6-4655-98ee-b52e8022d4af
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 命令行用法 {#command-line-usage}

策略更新清單管理器位於DVD的\Reference Implementation\Command Line Tools（\Reference實現\命令行工具）目錄中。 要建立策略更新清單，請使用以下語法：

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

下表包含上述語法中所示的命令行選項的說明：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c配置檔案 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置檔案的位置。 如果未使用此選項，則策略更新清單管理器將查找 <span class="filepath"> flashaccessols.properties </span> 的子菜單。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d檔案名 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">顯示有關策略更新清單的資訊。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e日期 </span> </td> 
   <td colname="2" class="- topic/entry "> （可選）策略更新清單的到期日期。 使用格式 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span> (例如，2009-01-31-14:30:00表示1月31日下午2:30)。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f檔案名[certfile] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">添加現有策略更新清單中的所有條目。 只能指定一個現有檔案。 </p> <p class="- topic/p ">如果此現有清單使用與用於對新清單進行簽名的憑據不同的憑據進行簽名，請指定其證書檔案，以便驗證其簽名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要詢問是否應覆蓋目標檔案。 如果目標檔案已存在，並且 <span class="codeph"> -o </span> 未設定，將返回錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目標檔案已存在，則覆蓋它而不出現提示。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r策略ID </span> <span class="+ topic/ph pr-d/codeph codeph"> 日期 </span> " <span class="+ topic/ph pr-d/codeph codeph"> 原因代碼 </span>" <span class="+ topic/ph pr-d/codeph codeph"> 原因文本 </span>" <span class="+ topic/ph pr-d/codeph codeph"> 原因URL </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（可選）撤消指定日期的策略ID。 還可以提供可選的原因代碼、原因文本和原因URL。 指定空字串「」，以指示未為可選參數提供值。 指定日期為 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span> (例如2008-12-1或2008-12-1-00:00:2008年12月1日午夜)。 如果未指定日期，則使用當前日期。 原因代碼必須大於或等於0。 可以指定多個 — r選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> 策略檔案名 </span> <span class="+ topic/ph pr-d/codeph codeph"> 日期 </span> " <span class="+ topic/ph pr-d/codeph codeph"> 原因代碼 </span>" <span class="+ topic/ph pr-d/codeph codeph"> 原因文本 </span>" <span class="+ topic/ph pr-d/codeph codeph"> 原因URL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">執行與 — r標誌相同的操作，但從給定檔案中提取策略標識符。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" "reasonText" "reasonURL" </span> </td> 
   <td colname="2" class="- topic/entry "> <p>使用給定原因代碼（可選）、原因文本（可選）和原因URL（可選）將許可證請求中的任何匹配策略替換為此策略。 </p> <p>指定空字串「」，以指示未為可選參數提供值。 </p> <p>原因代碼必須大於或等於 <span class="codeph"> 0 </span>。 多重 <span class="codeph"> -u </span> 可以指定選項。 </p> </td> 
  </tr> 
 </tbody> 
</table>
