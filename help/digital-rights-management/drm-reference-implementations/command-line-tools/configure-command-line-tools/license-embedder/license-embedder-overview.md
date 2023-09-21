---
title: 概觀
description: 概觀
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# DRM授權內嵌程式 {#license-embedder}

使用 [!DNL AdobeLicenseEmbedder.jar] 將預先產生的授權內嵌到Media Packager保護的內容中。

## 授權內嵌程式命令列使用方式 {#license-embedder-command-line-usage}

```
java -jar AdobeLicenseEmbedder.jar sourcefile destfile [options]
```

* `sourcefile` 代表加密的檔案。
* `destfile` 指定儲存含內嵌授權之加密內容的檔案名稱。

  如果您指定目錄，檔案會儲存在目的地目錄中。 來源檔案的名稱也會變成儲存在目的地目錄中的檔案名稱。

下表說明您可以指定的命令列選項：

**表7：選項**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_hnl_2sy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令列選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l license-filename </span> </td> 
   <td colname="2" class="- topic/entry "> 包含您要內嵌之授權的檔案名稱。 您可以指定多個 <span class="codeph"> -l </span> 嵌入多個授權的選項。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m metadata-filename </span> </td> 
   <td colname="2" class="- topic/entry "> 指定您可以為其產生授權的內容中繼資料。 需要此選項才能產生授權。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> 不要詢問是否應該覆寫目的地檔案。 如果目的地檔案已經存在，而且 <span class="codeph"> -o </span> 尚未套用，發生錯誤。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> 如果目的地檔案已經存在，您便可以覆寫該檔案，而不需要系統提示。 </td> 
  </tr> 
 </tbody> 
</table>
