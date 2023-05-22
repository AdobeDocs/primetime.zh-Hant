---
title: 概述
description: 概述
copied-description: true
exl-id: ba6e8fab-b199-4969-b372-06fa6d7a1e4a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# DRM許可證生成器 {#license-generator}

使用 [!DNL AdobeLicenseGenerator.jar] 生成許可證，而不需要客戶端向伺服器發送許可證請求。 然後，您可以在內容中嵌入預生成的許可證，或通過其他機制（如簡單的HTTP Web伺服器）將許可證交付給客戶端。

## 許可證生成器命令行用法 {#license-generator-command-line-usage}

**生成許可證：**

```
java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

* `metadata`  — 包括Adobe PrimetimeDRM元資料。

   您可以使用 `-d -m` 選項。

**顯示以前生成的許可證：**

```
java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

* `license`  — 包含由許可證生成器生成的Adobe PrimetimeDRM許可證。

**表6:選項**

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置檔案的名稱和位置。 </p> <p class="- topic/p ">如果未指定名稱或位置，DRM許可證生成器將搜索 <span class="filepath"> flashaccessols.properties</span> 的子菜單。 </p> <p>注：在命令行上指定的選項優先於在配置檔案中指定的選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> 許可檔案</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> 顯示有關已生成的許可證的資訊。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf leaf檔案名</span> </td> 
   <td colname="2" class="- topic/entry "> 生成葉許可證，並將輸出保存在指定檔案中。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m元資料檔案名</span> </td> 
   <td colname="2" class="- topic/entry "> 指定需要為其生成許可證的內容元資料。 生成許可證時需要此選項。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">不要詢問是否應覆蓋目標檔案。 如果目標檔案已存在，並且 <span class="codeph"> -o</span> 未設定，發生錯誤。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目標檔案已存在，則無需提示即可覆蓋它。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy policy num</span> </td> 
   <td colname="2" class="- topic/entry "> <p>如果元資料包括多個DRM策略，則可以指定可用於生成許可證的DRM策略數。 </p> <p>如果未指定DRM策略的數量，則會自動應用第一個DRM策略。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r收件人證書</span> </td> 
   <td colname="2" class="- topic/entry ">為指定的收件人生成許可證。 可以使用設備或域證書，並且可以指定多個 <span class="+ topic/ph pr-d/codeph codeph"> -r </span>選項，為多個收件人建立許可證。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root根檔案名</span> </td> 
   <td colname="2" class="- topic/entry "> 生成根許可證，並將輸出保存到您指定的檔案。 </td> 
  </tr> 
 </tbody> 
</table>

## 配置檔案屬性 {#configuration-file-properties}

在運行許可證生成器之前，需要在配置檔案中為許可證生成器屬性指定值。

>[!NOTE]
>
>對於包含的屬性名 *n*。 *n* 表示以1開頭的整數，並為屬性的每個實例增加。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_qk1_rry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 屬性 </th> 
   <th colname="2" class="- topic/entry entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.minClientVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p>設定當前支援的最低客戶端版本。 如果未設定此屬性，則預設情況下將自動支援所有版本。 </p> <p>您可以設定此值以控制較舊客戶端如何響應他們不支援的許可證要求。 指定 <span class="codeph"> x</span> (用於Adobe PrimetimeDRM x.0), <span class="codeph"> x</span> 表示一個主要版本號。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> 密鑰伺服器證書，是密鑰伺服器使用的Adobe頒發的許可證伺服器證書。 僅當元資料/DRM策略指示密鑰伺服器需要用於向iOS設備傳遞密鑰時，才應用此證書。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.cerfile</span> </td> 
   <td colname="2" class="- topic/entry "> PKCS12檔案，其中包含用於簽名許可證的許可證伺服器憑據。 此屬性需要引用包含證書和私鑰的.pfx檔案。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.cerpass</span> </td> 
   <td colname="2" class="- topic/entry ">用於保護您使用 <span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.cerfile</span> 的雙曲餘切值。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p>如果生成域綁定的許可證，則必須指定一個或多個域CA證書以指示許可證頒發者可以信任的域授權。 </p> <p>如果許可證接收者是域證書，而該證書不是由指定的域CA之一頒發的，則無法生成許可證。 此屬性指定 <span class="filepath"> .cer</span> 包含PEM或DER格式的證書的檔案。 <span class="codeph">n</span> 必須單調增加，從1開始。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可選的PKCS12檔案，其中包括用於解密元資料和DRM策略中的CEK的附加許可證伺服器憑據。 如果內容以前已與許可證伺服器證書打包，而不是那些已指定的憑據，則可以配置其他憑據 <span class="codeph"> licensegen.sign.cerfile</span>。 此屬性需要引用 <span class="filepath"> .pfx</span> 包含證書和私鑰的檔案。 <span class="codeph">n</span> 必須單調增加，從1開始。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n.password</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p>密碼用於保護您使用<span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.asymmetric.licenseServerCredential.n</span> 屬性。 </p> </td> 
  </tr> 
 </tbody> 
</table>
