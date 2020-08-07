---
description: 'null'
seo-description: 'null'
seo-title: 概觀
title: 概觀
uuid: f4474837-9460-479d-89c2-dd697e0fb997
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '1317'
ht-degree: 0%

---


# DRM Media Packager {#media-packager}

使用Media Packager( [!DNL AdobePackager.jar])指定要套用至您內容的DRM原則，並指定要加密的內容的哪一部分。 例如，您可以指定封裝程式應加密視訊資料，但不加密音訊資料。

在運行之 [!DNL AdobePackager.jar]前，必須在配置檔案的「Media Packager屬性」部分中設定屬性。

>[!NOTE]
>
>您也可以從命令行中指定所有Media Packager屬性。

## Media Packager命令列使用 {#media-packager-command-line-usage}

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

* `source` -要加密的檔案的名稱。
* `dest` -產生的加密檔案的名稱。

   如果指定目錄，則加密的檔案將自動保存在指定的目錄中，其檔案名與指定的源檔案相同。 但是，您不能指定包含源檔案的目標目錄。

**使用相同的金鑰封裝多個檔案** （針對多位元速率支援）:

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

* `sourcefiles` -要加密的檔案的一系列以空格分隔的源項。
* `dest-directory` -要寫入加密內容的目標目錄。 加密的檔案會使用與源檔案相同的檔案名自動保存到此目錄中。 但是，目標目錄不能包含任何源檔案。

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

* `metadatafile` 是包含 [!DNL .metadata] DRM元資料的檔案。

>[!NOTE]
>
>在封裝期間，Media Packager依預設無法再產 [!DNL .header] 生檔案。 若要產生 [!DNL .header] 檔案，請在封裝期 `-h` 間使用選項。

**表3:選項**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_wgz_spy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-c <span class="+ topic/ph pr-d/codeph codeph"> configfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置檔案的名稱和位置。 </p> <p class="- topic/p ">如果您未指定名稱或位置，DRM Media Packager會在目前工作目錄中搜 <span class="filepath"> 尋flashaccessools. </span> properties。 </p> <p>注意： 在命令行上指定的選項優先於在配置檔案中指定的選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d加 <span class="+ topic/ph pr-d/codeph codeph"> 密檔案 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可讓您檢視已封裝檔案的相關資訊。 </p> <p class="- topic/p ">源檔案和目標檔案不是必需的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> metadatafile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可讓您檢視現有中繼資料的相關資訊。 </p> <p class="- topic/p ">源檔案和目標檔案不是必需的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">將此選項與 <span class="codeph"> -d選項一起應用時，從打包的檔案中提取DRM </span> 策略。 </p> <p class="- topic/p ">在加密檔案所在的同一目錄中自動建立檔案，該檔案具有檔案名和DRM策略標識符。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">將此選項與 <span class="codeph"> -d選項一起應用時，從打包的檔案中提取DRM </span> 標頭。 </p> <p class="- topic/p ">系統會自動在加密檔案所在的相同目錄中建立檔案，其檔案名稱和副檔名為 <span class="filepath"> .header </span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定此內容區段的唯一識別碼。 </p> <p class="- topic/p ">如果您未指定識別碼，則會自動套用目標檔案名稱。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> 鍵 </span>= <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要新增至內容中繼資料的自訂索引鍵／值。 </p> <p class="- topic/p ">您可以指定多 <span class="codeph"> 個-k </span> 選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">當您結合-d選項套用此選項時，從封裝的檔案擷取 <span class="codeph"> 中繼 </span> 資料。 </p> <p class="- topic/p ">檔案會自動建立在與加密檔案相同的目錄中，該檔案具有檔案名和 <span class="codeph"> .metadata副 </span> 名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">請勿詢問是否應覆寫目標檔案。 </p> <p class="- topic/p ">如果目標檔案已存在且 <span class="codeph"> 未設 </span> 置-o，則發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">覆寫目標檔案，但不會收到提示，除非該檔案已存在。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p文 <span class="+ topic/ph pr-d/codeph codeph"> 件名[domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定包含DRM策略的檔案名。 </p> <p class="- topic/p ">如果DRM策略要求向使用傳輸證書（而不是在屬性檔案中指定的傳輸證書）的伺服器進行域註冊，則需要提供域傳輸證書。 </p> <p class="- topic/p ">您可以指定多 <span class="codeph"> 個-p </span> 選項。 依預設，用戶端一律會套用第一個選項。 您在命令行中指定的值優先於在配置檔案中指定的值。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 配置屬性 {#configuration-properties}

<!--<a id="section_3081C60BE54D47569FD1E3793513A2D9"></a>-->

>[!NOTE]
>
>對於包含* n*的屬性名稱， *n* 表示以1開頭的整數，並且會為屬性的每個實例增加。

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
   <td colname="2" class="- topic/entry "> 指出是否加密視訊內容。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.audio</span> </td> 
   <td colname="2" class="- topic/entry "> 指示是否加密音頻。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.script</span> </td> 
   <td colname="2" class="- topic/entry "> <p>指示是否加密mp4中的指令碼資料。 </p> <p><i class="+ topic/ph hi-d/i ">onMetaData</i> 和 <i class="+ topic/ph hi-d/i ">onXMP</i> script資料標籤即使您啟用此選項，也不會加密。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示視頻加密級別。 </p> <p class="- topic/p ">高值 <span class="codeph"> 用於加密所有視頻內容</span><span class="codeph"></span><span class="codeph"></span> ，而中值和低值用於加密包含H.264內容的mp4檔案的視頻內容的部分。 </p> <p class="- topic/p ">值=高 <span class="codeph"> |中級 |低</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.secondsUnencrypted</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果值大於0，則不會加密檔案開頭處指定的內容秒數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.ansymmet.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用於加密密鑰的許可證伺服器證書檔案。 </p> <p class="- topic/p ">encrypt.keys. <span class="codeph"> ansymetric.certfile</span> 屬性指定僅包含證書的檔案（可接受PEM或DER格式）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">此屬性會重複用於建立要應用於內容的DRM策略清單。 <span class="codeph"> n</span> 表示值為1或更大的整數。 預設情況下，客戶端使用第一個實例。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權伺服器URL </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">許可證伺服器的傳輸證書。 </p> <p class="- topic/p ">此屬性指定僅包 <span class="filepath"> 含證書的。cer</span> 檔案（可接受PEM或DER格式）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">PKCS12檔案，包含用於簽署內容的封裝憑證。 </p> <p class="- topic/p ">encrypt. <span class="codeph"> sign.certfile</span> ，需要參照包含憑證和 <span class="filepath"> 私密金鑰的。pfx</span> 檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">您可以套用的密碼，以保護由 <span class="codeph"> encrypt.sign.certfile指定的檔案</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">設定為要封裝的內容發行授權所需的最低伺服器版本。 </p> <p class="- topic/p ">指定x（適用於Primetime DRM x.0），其中x代表主要發行號。 任何Adobe Primetime 3.0版之前的伺服器版本都不支援此設定。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n .domain.transportcert </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果DRM策 <span class="+ topic/ph pr-d/codeph codeph"> 略encrypt.keys.policyFile.n</span> 要求在支援傳輸證書(在 <span class="+ topic/ph pr-d/codeph codeph"></span>encrypt.license.servercert中指定的傳輸證書除外)的伺服器上註冊域，則需要提供域傳輸證書需要。 </p> <p class="- topic/p ">此屬性指定僅包含證書的檔案（PEM或DER格式是可接受的）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定許可證密鑰。 </p> <p class="- topic/p ">如果您未指定索引鍵，則會隨機產生索引鍵。 當您未啟用金鑰旋轉時，就可以使用此金鑰來加密內容。 </p> <p class="- topic/p ">啟用密鑰旋轉時，可以使用此密鑰保護旋轉密鑰。 索引鍵長度必須為16個位元組，並指定為十六進位值。 十六進位值之間的空格是可選的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定是否啟用密鑰旋轉。 </p> <p class="- topic/p ">如果設定為false（這是預設設定），則禁用密鑰旋轉，並使用主CEK加密內容中的所有樣本。 </p> <p class="- topic/p ">如果設為true，則會啟用金鑰旋轉，並可使用不同的金鑰來加密任何內容的區段。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">已旋轉的金鑰序列，您可以指定在啟用金鑰旋轉時加密內容。 </p> <p class="- topic/p ">如果您未指定任何按鍵，則會隨機產生按鍵。 密鑰長度必須為16個位元組，並指定為十六進位值。 </p> <p class="- topic/p ">十六進位值之間的空格是可選的。 <i class="+ topic/ph hi-d/i ">n必</i> 須單調增加，從1開始。 當您指定多個按鍵時，按您所指示的順序來循環使用按鍵。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定可套用旋轉金鑰來加密內容範例的時間間隔（以秒為單位）。 </p> <p class="- topic/p ">在經過已加密內容的時間間隔之後，接著套用下一個旋轉密鑰。 如果您已啟用金鑰旋轉，但未指定任何時間間隔，則每15分鐘自動旋轉一次金鑰。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果此選項設為true，則無法使用可從中取得授權的授權伺服器。 </p> <p class="- topic/p ">授權必須內嵌或取得帶外授權。 除非您指定其他值，否則預設值會設為false。 此選項僅在Primetime DRM Professional中受支援。 </p> </td> 
  </tr> 
 </tbody> 
</table>