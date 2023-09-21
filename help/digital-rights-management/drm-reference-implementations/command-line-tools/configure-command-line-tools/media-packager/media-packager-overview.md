---
title: 概觀
description: 概觀
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---

# DRM媒體封裝程式 {#media-packager}

使用Media Packager ( [!DNL AdobePackager.jar])，以指定要套用至內容的DRM原則，並指定要加密的內容部分。 例如，您可以指定封裝程式應加密視訊資料，但不加密音訊資料。

執行之前 [!DNL AdobePackager.jar]，您必須在設定檔案的Media Packager Properties區段中設定屬性。

>[!NOTE]
>
>您也可以從命令列指定所有「媒體封裝程式」屬性。

## Media Packager命令列使用方式 {#media-packager-command-line-usage}

**封裝一個檔案：**

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  source  
 <i class="+ topic ph hi-d="" i "="">
   dest [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `source`  — 您要加密的檔案名稱。
* `dest`  — 產生的加密檔案的名稱。

  如果您指定目錄，則加密的檔案會自動儲存在指定的目錄中，且檔案名稱與您指定的來源檔案相同。 但是，您無法指定包含來源檔案的目標目錄。

**使用相同的索引鍵封裝多個檔案** （支援多位元速率）：

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefiles  
 <i class="+ topic ph hi-d="" i "="">
   dest-directory [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `sourcefiles`  — 一系列以空格分隔的來源專案，用於您想要加密的檔案。
* `dest-directory`  — 您要寫入加密內容的目的地目錄。 加密的檔案會使用與來源檔案相同的檔案名稱，自動儲存在此目錄中。 但是，目的地目錄不能包含任何來源檔案。

**檢視加密檔案的相關資訊：**

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

**檢視中繼資料檔案的相關資訊：**

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` 是 [!DNL .metadata] 包含DRM中繼資料的檔案。

>[!NOTE]
>
>封裝期間，Media Packager無法再產生 [!DNL .header] 預設為檔案。 產生 [!DNL .header] 檔案，使用 `-h` 封裝期間選項。

**表3：選項**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_wgz_spy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令列選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-c <span class="+ topic/ph pr-d/codeph codeph"> configfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定組態檔的名稱和位置。 </p> <p class="- topic/p ">如果您未指定名稱或位置，DRM Media Packager會搜尋 <span class="filepath"> flashaccesstools.properties </span> 於目前工作目錄中。 </p> <p>注意：您在命令列中指定的選項優先於您在組態檔案中指定的選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph"> encryptedfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可讓您檢視已封裝檔案的相關資訊。 </p> <p class="- topic/p ">來源和目的地檔案並非必要檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> 中繼資料檔 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可讓您檢視現有中繼資料的相關資訊。 </p> <p class="- topic/p ">來源和目的地檔案並非必要檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">當您將此選項與套用時，從封裝檔案中擷取DRM原則 <span class="codeph"> -d </span> 選項。 </p> <p class="- topic/p ">系統會在加密檔案所在的同一目錄中自動建立檔案，其中含有檔案名稱和DRM原則識別碼。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">當您將此選項與套用時，從封裝檔案中擷取DRM標頭 <span class="codeph"> -d </span> 選項。 </p> <p class="- topic/p ">系統會自動在加密檔案所在的同一目錄中建立檔案，且檔案名稱和副檔名皆為 <span class="filepath"> .header </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定此內容區段的唯一識別碼。 </p> <p class="- topic/p ">如果您未指定識別碼，則會自動套用destfile檔案名稱。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> key </span>= <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要新增至內容中繼資料的自訂索引鍵/值。 </p> <p class="- topic/p ">您可以指定多個 <span class="codeph"> -k </span> 選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">當您套用此選項和 <span class="codeph"> -d </span> 選項。 </p> <p class="- topic/p ">系統會在與加密檔案相同的目錄中自動建立檔案，且檔案名稱和 <span class="codeph"> .metadata </span> 副檔名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要詢問是否應該覆寫目的地檔案。 </p> <p class="- topic/p ">如果目的地檔案已存在，並且 <span class="codeph"> -o </span> 未設定，則會發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">覆寫目的地檔案，除非檔案已經存在，否則系統不會提示您進行覆寫。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> 檔案名稱[domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定包含DRM原則的檔案名稱。 </p> <p class="- topic/p ">如果DRM原則要求使用傳輸憑證的伺服器登入網域，而不是您在屬性檔案中指定的伺服器，則您必須提供網域傳輸憑證。 </p> <p class="- topic/p ">您可以指定多個 <span class="codeph"> -p </span> 選項。 依預設，使用者端一律會套用第一個選項。 您在命令列中指定的值優先於您在組態檔案中指定的值。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 設定屬性 {#configuration-properties}

<!--<a id="section_3081C60BE54D47569FD1E3793513A2D9"></a>-->

>[!NOTE]
>
>對於包含* n*的屬性名稱， *n* 代表以1開頭的整數，並且會隨著屬性的每個例項而增加。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_dx4_mpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">屬性 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video</span> </td> 
   <td colname="2" class="- topic/entry "> 指示是否要加密視訊內容。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.audio</span> </td> 
   <td colname="2" class="- topic/entry "> 指示是否要加密音訊。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.script</span> </td> 
   <td colname="2" class="- topic/entry "> <p>指示是否加密mp4中的指令碼資料。 </p> <p><i class="+ topic/ph hi-d/i ">onMetaData</i> 和 <i class="+ topic/ph hi-d/i ">onXMP</i> 即使您啟用此選項，指令碼資料標籤也不會加密。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">表示視訊加密等級。 </p> <p class="- topic/p ">值 <span class="codeph"> 高</span> 用於加密所有視訊內容，而值 <span class="codeph"> 中</span> 和 <span class="codeph"> 低</span> 用於加密包含H.264內容的mp4檔案的部分視訊內容。 </p> <p class="- topic/p ">值= <span class="codeph"> 高 |中 |低</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.secondsUnencrypted</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果值大於0，則檔案開頭指定的內容秒數不會加密。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用來加密金鑰的授權伺服器憑證檔案。 </p> <p class="- topic/p ">此 <span class="codeph"> encrypt.keys.asymmetric.certfile</span> 屬性指定僅包含憑證的檔案（可接受PEM或DER格式）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">此屬性會重複用來建立要套用至內容的DRM原則清單。 <span class="codeph"> n</span> 代表值為1或以上的整數。 使用者端預設會使用第一個執行個體。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權伺服器URL </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權伺服器的傳輸憑證。 </p> <p class="- topic/p ">此屬性會指定 <span class="filepath"> .cer</span> 僅包含憑證的檔案（可接受PEM或DER格式）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">包含封裝程式認證的PKCS12檔案，用於簽署內容。 </p> <p class="- topic/p ">此 <span class="codeph"> encrypt.sign.certfile</span> 需要參考 <span class="filepath"> .pfx</span> 包含憑證和私密金鑰的檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">您可以套用的密碼，用來保護由指定的檔案 <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">設定為封裝的內容發行授權所需的最低伺服器版本。 </p> <p class="- topic/p ">指定x （針對Primetime DRM x.0），其中x代表主要發行版本編號。 Adobe Primetime 3.0之前的任何伺服器版本均不支援此設定。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n .domain.transportcert </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果DRM原則 <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> 需要透過支援傳輸憑證的伺服器登入網域，而不是透過您指定的伺服器登入 <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>，則您需要提供網域傳輸憑證需求。 </p> <p class="- topic/p ">此屬性指定僅包含憑證的檔案（可接受PEM或DER格式）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定授權金鑰。 </p> <p class="- topic/p ">如果您未指定金鑰，則會隨機產生金鑰。 如果您未啟用金鑰輪換，則可以使用此金鑰來加密內容。 </p> <p class="- topic/p ">當您啟用金鑰輪換時，可以使用此金鑰來保護輪換金鑰。 金鑰的長度必須是16個位元組，並指定為十六進位值。 十六進位值之間的空白字元為選用。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定是否啟用金鑰輪換。 </p> <p class="- topic/p ">如果設定為false （預設設定），則會停用金鑰輪換，並使用主要CEK來加密內容中的所有範例。 </p> <p class="- topic/p ">若設為true，則會啟用金鑰輪換，而使用不同的金鑰來加密任何內容的區段。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">啟用金鑰輪換時，您可以指定用來加密內容的輪換金鑰順序。 </p> <p class="- topic/p ">如果您未指定任何金鑰，則會隨機產生金鑰。 金鑰的長度必須是16個位元組，並指定為十六進位值。 </p> <p class="- topic/p ">十六進位值之間的空白字元為選用。 <i class="+ topic/ph hi-d/i ">n</i> 必須從1開始單調遞增。 當您指定多個金鑰時，金鑰會依照您指定的順序循環瀏覽。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定可套用旋轉金鑰來加密內容範例的時間間隔（秒）。 </p> <p class="- topic/p ">經過加密內容的時間間隔後，就會套用下一個輪換金鑰。 如果您已啟用金鑰輪換，但尚未指定任何時間間隔，則會每15分鐘自動輪換金鑰。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果此選項設定為true，則無法取得授權的授權伺服器。 </p> <p class="- topic/p ">授權必須內嵌或在頻外取得。 除非您指定不同的值，否則預設值會設為false。 只有Primetime DRM Professional支援此選項。 </p> </td> 
  </tr> 
 </tbody> 
</table>
