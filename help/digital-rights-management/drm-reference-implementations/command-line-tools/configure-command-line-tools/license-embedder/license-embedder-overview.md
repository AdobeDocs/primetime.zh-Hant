---
seo-title: 概觀
title: 概觀
uuid: 5487d1d3-7eb8-410d-a4b1-cde3e94c00a1
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# DRM授權嵌入程式 {#license-embedder}

使用 [!DNL AdobeLicenseEmbedder.jar] 將預先產生的授權內嵌至Media Packager保護的內容。

## 授權嵌入器命令列使用 {#license-embedder-command-line-usage}

```
java -jar AdobeLicenseEmbedder.jar sourcefile destfile [options]
```

* `sourcefile` 代表加密的檔案。
* `destfile` 指定保存具有嵌入式許可證的加密內容的檔案的名稱。

   如果指定目錄，則檔案將保存在目標目錄中。 源檔案的名稱也將成為保存在目標目錄中的檔案的名稱。

下表說明了可指定的命令行選項：

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
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l license-filename </span> </td> 
   <td colname="2" class="- topic/entry "> 包含您要嵌入之授權的檔案名稱。 您可以指定多個 <span class="codeph"> -l選 </span> 項來內嵌多個授權。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m元資料檔案名 </span> </td> 
   <td colname="2" class="- topic/entry "> 指定可產生授權的內容中繼資料。 產生授權時需要此選項。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> 請勿詢問是否應覆寫目標檔案。 如果目標檔案已存在且 <span class="codeph"> -o </span> 尚未應用，則會發生錯誤。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> 如果目標檔案已存在，則無需提示即可覆蓋它。 </td> 
  </tr> 
 </tbody> 
</table>
