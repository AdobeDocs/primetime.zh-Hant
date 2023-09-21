---
title: 命令列使用方式
description: 命令列使用方式
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# 命令列使用方式 {#command-line-usage}

若要產生許可證，請使用下列語法：

```
    java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

`metadata` 是包含Adobe存取DRM中繼資料的.metadata檔案。 您可以使用從受保護內容取得此檔案 `-d -m` Media Packager選項。

若要顯示先前產生的許可證，請使用下列語法：

```
    java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

`license` 是包含「許可證產生器」產生的「Adobe存取」許可證的檔案。

下表說明可連同先前提到的語法一起指定的命令列選項：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_skr_vry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令列選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c設定檔</span> </td> 
   <td colname="2" class="- topic/entry "> 指定組態檔的位置。 如果未使用此選項，License Generator會在工作目錄中尋找flashaccesstools.properties。 命令列上指定的選項優先於組態檔案中的選項。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> licensefile</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> 顯示已產生之授權的相關資訊。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf leaf-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 產生Leaf授權並將輸出寫入指定的檔案。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m metadata-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 指定要為其產生授權的內容中繼資料。 （產生授權所需） </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">不要詢問是否應該覆寫目的地檔案。 如果目的地檔案已存在，並且 <span class="codeph"> -o</span> 未設定，則會傳回錯誤。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目的地檔案已經存在，則覆寫它而不進行提示。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> 如果中繼資料包含多個原則，請指定用來產生授權的原則編號（從1開始）。 如果未指定，則使用第一個原則。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r recipient-cer</span> </td> 
   <td colname="2" class="- topic/entry ">為指定的收件者產生授權。 可以使用裝置或網域憑證。 多個 <span class="+ topic/ph pr-d/codeph codeph"> -r </span>可以指定選項來建立多個收件者的授權。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root root-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 產生根授權並將輸出寫入指定的檔案。 </td> 
  </tr> 
 </tbody> 
</table>
