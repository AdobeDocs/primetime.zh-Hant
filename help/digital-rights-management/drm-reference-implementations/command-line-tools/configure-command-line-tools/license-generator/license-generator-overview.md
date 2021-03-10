---
title: 概觀
description: 概觀
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---


# DRM License Generator {#license-generator}

使用[!DNL AdobeLicenseGenerator.jar]產生授權，而不需要用戶端傳送授權要求至伺服器。 然後，您可以將預先產生的授權內嵌在內容中，或透過其他機制（例如簡單的HTTP網頁伺服器）將授權傳送給用戶端。

## License Generator命令列用法{#license-generator-command-line-usage}

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

* `metadata` -包括Adobe PrimetimeDRM元資料。

   您可以使用Media Packager中的`-d -m`選項，從受保護的內容擷取此檔案。

**顯示先前產生的授權：**

```
java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

* `license` -包含由授權產生器產生的Adobe PrimetimeDRM授權。

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置檔案的名稱和位置。 </p> <p class="- topic/p ">如果您未指定名稱或位置，DRM License Generator會在目前工作目錄中搜尋<span class="filepath"> flashaccessools.properties</span>。 </p> <p>注意： 在命令行上指定的選項優先於在配置檔案中指定的選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph">許可證檔案</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> 顯示已產生之授權的相關資訊。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf-leaf-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 產生葉片授權，並將輸出儲存在指定的檔案中。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m元資料檔案名</span> </td> 
   <td colname="2" class="- topic/entry "> 指定您需要產生授權的內容中繼資料。 產生授權時需要此選項。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">請勿詢問是否應覆寫目標檔案。 如果目標檔案已存在且<span class="codeph"> -o</span>尚未設定，則會發生錯誤。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目標檔案已存在，則無需提示即可覆蓋它。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy-policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> <p>如果元資料包含多個DRM策略，則可以指定用於生成許可證的DRM策略數。 </p> <p>如果未指定DRM策略的數量，則會自動應用第一個DRM策略。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r recipient-cert</span> </td> 
   <td colname="2" class="- topic/entry ">為指定的收件者產生授權。 您可以使用裝置或網域憑證，也可以指定多個<span class="+ topic/ph pr-d/codeph codeph"> -r </span>選項，以建立多個收件者的授權。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root根檔案名</span> </td> 
   <td colname="2" class="- topic/entry "> 產生根授權並將輸出儲存到您指定的檔案。 </td> 
  </tr> 
 </tbody> 
</table>

## 配置檔案屬性{#configuration-file-properties}

在執行授權產生器之前，您必須在設定檔案中指定授權產生器屬性的值。

>[!NOTE]
>
>對於包含&#x200B;*n*&#x200B;的屬性名稱，*n*&#x200B;代表以1開頭的整數，並且會針對屬性的每個例項增加。

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
   <td colname="2" class="- topic/entry "> <p>設定當前支援的最低客戶端版本。 如果您未設定此屬性，預設會自動支援所有版本。 </p> <p>您可以設定此值，以控制較舊的用戶端如何回應他們不支援的授權需求。 指定<span class="codeph"> x</span>(針對Adobe PrimetimeDRM x.0)，其中<span class="codeph"> x</span>代表主要發行版本號碼。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> 金鑰伺服器憑證，此為由金鑰伺服器使用的Adobe授權伺服器憑證。 僅當元資料/DRM策略指示密鑰發送到iOS設備需要密鑰伺服器時，才應用此證書。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> PKCS12檔案，包含用於簽署許可證的許可證伺服器憑據。 此屬性需要參考包含憑證和私密金鑰的。pfx檔案。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">用於保護您使用<span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span>選項指定的檔案的口令。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p>如果您產生網域系結的授權，您必須指定一或多個網域CA憑證，以指出授權發行者可信任的網域授權機構。 </p> <p>如果授權收件者是網域憑證（並非由其中一個指定的網域CA核發），則無法產生授權。 此屬性指定<span class="filepath"> .cer</span>檔案，該檔案包含PEM或DER格式的證書。 <span class="codeph">必</span> 須單調增加，從1開始。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可選的PKCS12檔案，其中包括用於解密元資料和DRM策略中的CEK的附加許可證伺服器憑據。 如果內容之前已封裝為授權伺服器憑證，而非使用<span class="codeph"> licensegen.sign.certfile</span>指定的憑證，則可設定其他憑證。 此屬性需要參考<span class="filepath"> .pfx</span>檔案，其中包含憑證和私密金鑰。 <span class="codeph">必</span> 須單調增加，從1開始。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n.password</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p>此密碼用於保護您使用<span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.ansymetic.licenseServerCredential.n</span>屬性指定的檔案。 </p> </td> 
  </tr> 
 </tbody> 
</table>