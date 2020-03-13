---
seo-title: 命令列使用
title: 命令列使用
uuid: b3a995de-653e-491a-9262-86dc56b9ce31
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 命令列使用 {#command-line-usage}

若要產生授權，請使用下列語法：

```
    java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

`metadata` 是包含Adobe Access DRM中繼資料的。metadata檔案。 此檔案可使用Media Packager選項從受保護的 `-d -m` 內容取得。

若要顯示先前產生的授權，請使用下列語法：

```
    java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

`license` 是包含授權產生器產生之Adobe Access授權的檔案。

下表說明了可以指定的命令行選項以及前面提到的語法：

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
   <td colname="2" class="- topic/entry "> 指定配置檔案的位置。 如果未使用此選項，License Generator會在工作目錄中尋找flashaccessools.properties。 命令行上指定的選項優先於配置檔案中顯示的選項。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d許 <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> 可檔案</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> 顯示已產生之授權的相關資訊。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf-leaf-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 產生葉片授權，並將輸出寫入指定的檔案。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m元資料檔案名</span> </td> 
   <td colname="2" class="- topic/entry "> 指定要產生授權的內容中繼資料。 （需要產生授權） </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">請勿詢問是否應覆寫目標檔案。 如果目標檔案已存在且 <span class="codeph"> 未設定</span> -o，則將返回錯誤。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目標檔案已存在，請不提示而覆寫它。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy-policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> 如果中繼資料包含多個原則，請指定要使用的原則數目（從1開始）以產生授權。 如果未指定，則使用第一個策略。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r recipient-cert</span> </td> 
   <td colname="2" class="- topic/entry ">為指定的收件者產生授權。 可以使用設備或域證書。 可以 <span class="+ topic/ph pr-d/codeph codeph"> 指定多 </span>個-r選項，為多個收件者建立許可證。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root根檔案名</span> </td> 
   <td colname="2" class="- topic/entry "> 產生根授權，並將輸出寫入指定的檔案。 </td> 
  </tr> 
 </tbody> 
</table>

