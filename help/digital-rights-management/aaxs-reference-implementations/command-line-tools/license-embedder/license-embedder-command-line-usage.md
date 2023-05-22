---
title: 命令行用法
description: 命令行用法
copied-description: true
exl-id: 51b11ef8-438e-4747-be3e-e1774dc9f31a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 命令行用法 {#command-line-usage}

要嵌入許可證，請使用以下語法：

```
    java -jar AdobeLicenseEmbedder.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefile destfile [options] 
</i class="+ topic>
```

* `sourcefile` 是加密的FLV或F4V檔案。
* `destfile` 指定將寫入嵌入許可證的加密內容的位置。 如果指定了目錄，則檔案將使用與源檔案相同的檔案名保存到此目錄中，但該目錄不能是包含源檔案的目錄。

下表介紹了可以指定的命令行選項以及前面提到的語法：

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
   <td colname="2" class="- topic/entry "> 包含要嵌入的許可證的檔案的名稱。 多重 <span class="codeph"> -l </span> 可以指定選項來嵌入多個許可證。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m元資料檔案名 </span> </td> 
   <td colname="2" class="- topic/entry "> 指定要為其生成許可證的內容元資料。 （生成許可證時需要） </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> 不要詢問是否應覆蓋目標檔案。 如果目標檔案已存在，並且 <span class="codeph"> -o </span> 未設定，將返回錯誤。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> 如果目標檔案已存在，則覆蓋它而不出現提示。 </td> 
  </tr> 
 </tbody> 
</table>
