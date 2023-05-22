---
title: 概述
description: 概述
copied-description: true
exl-id: 9aebdbd0-a6f0-4c9d-be2f-a8789cadf287
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# DRM許可證嵌入程式 {#license-embedder}

使用 [!DNL AdobeLicenseEmbedder.jar] 將預生成的許可證嵌入到Media Packager保護的內容中。

## 許可證嵌入器命令行用法 {#license-embedder-command-line-usage}

```
java -jar AdobeLicenseEmbedder.jar sourcefile destfile [options]
```

* `sourcefile` 表示加密檔案。
* `destfile` 指定保存帶有嵌入許可證的加密內容的檔案的名稱。

   如果指定目錄，則檔案將保存在目標目錄中。 源檔案的名稱也成為保存在目標目錄中的檔案的名稱。

下表介紹了可指定的命令行選項：

**表7:選項**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_hnl_2sy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l許可證檔案名 </span> </td> 
   <td colname="2" class="- topic/entry "> 包含要嵌入的許可證的檔案的名稱。 可以指定多個 <span class="codeph"> -l </span> 可嵌入多個許可證的選項。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m元資料檔案名 </span> </td> 
   <td colname="2" class="- topic/entry "> 指定可為其生成許可證的內容元資料。 生成許可證時需要此選項。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> 不要詢問是否應覆蓋目標檔案。 如果目標檔案已存在，並且 <span class="codeph"> -o </span> 未應用，出現錯誤。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> 如果目標檔案已存在，則無需提示即可覆蓋它。 </td> 
  </tr> 
 </tbody> 
</table>
