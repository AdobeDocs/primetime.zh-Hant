---
title: 命令行用法
description: 命令行用法
copied-description: true
exl-id: 241849bb-e818-420e-98b4-c12e306b17b2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# 命令行用法 {#command-line-usage}

要生成許可證，請使用以下語法：

```
    java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

`metadata` 是包含Adobe訪問DRM元資料的.metadata檔案。 可以使用 `-d -m` 選項。

要顯示以前生成的許可證，請使用以下語法：

```
    java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

`license` 是包含許可證生成器生成的Adobe訪問許可證的檔案。

下表介紹了可以指定的命令行選項以及前面提到的語法：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_skr_vry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c配置檔案</span> </td> 
   <td colname="2" class="- topic/entry "> 指定配置檔案的位置。 如果未使用此選項，許可證生成器將在工作目錄中查找flashaccesstools.properties。 在命令行上指定的選項優先於配置檔案中存在的選項。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> 許可檔案</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> 顯示有關已生成的許可證的資訊。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf leaf檔案名</span> </td> 
   <td colname="2" class="- topic/entry "> 生成葉許可證，並將輸出寫入指定檔案。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m元資料檔案名</span> </td> 
   <td colname="2" class="- topic/entry "> 指定要為其生成許可證的內容元資料。 （生成許可證時需要） </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">不要詢問是否應覆蓋目標檔案。 如果目標檔案已存在，並且 <span class="codeph"> -o</span> 未設定，將返回錯誤。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目標檔案已存在，則覆蓋它而不出現提示。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy policy num</span> </td> 
   <td colname="2" class="- topic/entry "> 如果元資料包含多個策略，請指定要用於生成許可證的策略數（從1開始）。 如果未指定，則使用第一個策略。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r收件人證書</span> </td> 
   <td colname="2" class="- topic/entry ">為指定的收件人生成許可證。 可以使用設備或域證書。 多重 <span class="+ topic/ph pr-d/codeph codeph"> -r </span>可以指定選項為多個收件人建立許可證。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root根檔案名</span> </td> 
   <td colname="2" class="- topic/entry "> 生成根許可證，並將輸出寫入指定的檔案。 </td> 
  </tr> 
 </tbody> 
</table>
