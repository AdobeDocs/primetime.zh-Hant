---
title: 概觀
description: 概觀
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# DRM授權產生器 {#license-generator}

使用 [!DNL AdobeLicenseGenerator.jar] 產生授權，而不要求使用者端傳送授權要求至伺服器。 然後，您可以在內容中內嵌預先產生的授權，或透過其他機制（例如簡單的HTTP網頁伺服器）將授權傳送給使用者端。

## 授權產生器命令列使用方式 {#license-generator-command-line-usage}

**產生授權：**

```
java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

* `metadata`  — 包含Adobe Primetime DRM中繼資料。

  您可以使用從受保護的內容擷取此檔案 `-d -m` Media Packager中的選項。

**顯示先前產生的授權：**

```
java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

* `license`  — 包含由授權產生器產生的Adobe Primetime DRM授權。

**表6：選項**

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定組態檔的名稱和位置。 </p> <p class="- topic/p ">如果您未指定名稱或位置，則「DRM許可證產生器」會搜尋 <span class="filepath"> flashaccesstools.properties</span> 於目前工作目錄中。 </p> <p>注意：您在命令列中指定的選項優先於您在組態檔案中指定的選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> licensefile</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> 顯示已產生之授權的相關資訊。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf leaf-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 產生一個Leaf許可證並將輸出儲存在指定的檔案中。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m metadata-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 指定您需要為其產生授權的內容中繼資料。 需要此選項才能產生授權。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">不要詢問是否應該覆寫目的地檔案。 如果目的地檔案已經存在，而且 <span class="codeph"> -o</span> 尚未設定，發生錯誤。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目的地檔案已經存在，您便可以覆寫該檔案，而不需要系統提示。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> <p>如果中繼資料包含多個DRM原則，您可以指定可用於產生許可證的DRM原則數目。 </p> <p>如果您不指定DRM政策的數量，則會自動套用第一個DRM政策。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r recipient-cer</span> </td> 
   <td colname="2" class="- topic/entry ">為指定的收件者產生授權。 您可以使用裝置或網域憑證，也可以指定多個 <span class="+ topic/ph pr-d/codeph codeph"> -r </span>為多個收件者建立授權的選項。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root root-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 產生根許可證並將輸出儲存到您指定的檔案中。 </td> 
  </tr> 
 </tbody> 
</table>

## 組態檔屬性 {#configuration-file-properties}

執行「許可證產生器」之前，您必須在組態檔案中指定「許可證產生器」屬性的值。

>[!NOTE]
>
>針對包含的屬性名稱 *n*， *n* 代表以1開頭的整數，並且會隨著屬性的每個例項而增加。

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
   <td colname="2" class="- topic/entry "> <p>設定目前支援的最低使用者端版本。 如果您未設定此屬性，預設會自動支援所有版本。 </p> <p>您可以設定此值，以控制較舊的使用者端如何回應不支援的授權需求。 指定 <span class="codeph"> x</span> (適用於Adobe Primetime DRM x.0)，其中 <span class="codeph"> x</span> 代表主要發行版本編號。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Key Server憑證，這是Key Server所使用的Adobe核發的License Server憑證。 此憑證僅在中繼資料/DRM政策指出金鑰傳遞至iOS裝置需要金鑰伺服器時套用。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> 包含簽署授權之License Server認證的PKCS12檔案。 此屬性需要參照包含憑證和私密金鑰的.pfx檔案。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">用來保護您指定之檔案的密碼 <span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> 選項。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p>如果您產生網域繫結授權，則必須指定一或多個網域CA憑證，以指出授權簽發者可以信任的網域授權單位。 </p> <p>如果授權收件者是網域憑證（不是由指定的網域CA發行），則無法產生授權。 此屬性會指定 <span class="filepath"> .cer</span> 包含PEM或DER格式憑證的檔案。 <span class="codeph">n</span> 必須從1開始單調增加。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">選用的PKCS12檔案，其中包含用於解密中繼資料和DRM原則中的CEK的其他License Server認證。 如果內容先前已封裝有License Server憑證，而不是那些已透過指定的認證，您可以設定其他認證 <span class="codeph"> licensegen.sign.certfile</span>. 此屬性必須參考 <span class="filepath"> .pfx</span> 包含憑證和私密金鑰的檔案。 <span class="codeph">n</span> 必須從1開始單調增加。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n.password</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p>系統會套用密碼，以保護您透過指定的檔案<span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.asymmetric.licenseServerCredential.n</span> 屬性。 </p> </td> 
  </tr> 
 </tbody> 
</table>
