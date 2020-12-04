---
seo-title: 命令列使用
title: 命令列使用
uuid: 72117619-a723-49d3-9aa9-5eefcf5b0916
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# 命令行用法{#command-line-usage}

若要嵌入授權，請使用下列語法：

```
    java -jar AdobeLicenseEmbedder.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefile destfile [options] 
</i class="+ topic>
```

* `sourcefile` 是加密的FLV或F4V檔案。
* `destfile` 指定將寫入嵌入許可證的加密內容的位置。如果指定了目錄，則檔案將使用與源檔案相同的檔案名保存到此目錄中，但該目錄不能是包含源檔案的目錄。

下表說明了可以指定的命令行選項以及前面提到的語法：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_hnl_2sy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l license-filename  </span> </td> 
   <td colname="2" class="- topic/entry "> 包含要嵌入之授權的檔案名稱。 可以指定多個<span class="codeph"> -l </span>選項來嵌入多個許可證。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m元資料檔案名  </span> </td> 
   <td colname="2" class="- topic/entry "> 指定要產生授權的內容中繼資料。 （需要產生授權） </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> 請勿詢問是否應覆寫目標檔案。 如果目標檔案已存在且未設定<span class="codeph"> -o </span> ，則將返回錯誤。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> 如果目標檔案已存在，請不提示而覆寫它。 </td> 
  </tr> 
 </tbody> 
</table>

