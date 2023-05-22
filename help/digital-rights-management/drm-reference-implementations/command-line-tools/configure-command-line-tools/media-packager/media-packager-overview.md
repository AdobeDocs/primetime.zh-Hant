---
title: 概述
description: 概述
copied-description: true
exl-id: 866b3147-c28b-41b0-8653-06ba867354c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---

# DRM介質打包器 {#media-packager}

使用介質打包器( [!DNL AdobePackager.jar])以指定要應用於內容的DRM策略，並指定要加密的內容的哪一部分。 例如，可以指定打包器應加密視頻資料，而不是音頻資料。

運行前 [!DNL AdobePackager.jar]，必須在配置檔案的「媒體打包器屬性」部分設定屬性。

>[!NOTE]
>
>也可以從命令行指定所有介質打包器屬性。

## 介質打包器命令行用法 {#media-packager-command-line-usage}

**包一個檔案：**

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

* `source`  — 要加密的檔案的名稱。
* `dest`  — 生成的加密檔案的名稱。

   如果指定目錄，則加密檔案將自動保存在指定的目錄中，其檔案名與指定為源檔案的檔案名相同。 但是，不能指定包含源檔案的目標目錄。

**使用同一密鑰打包多個檔案** （用於多比特率支援）:

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

* `sourcefiles`  — 要加密的檔案的一系列以空格分隔的源條目。
* `dest-directory`  — 要寫入加密內容的目標目錄。 加密的檔案將自動保存在此目錄中，使用與源檔案相同的檔案名。 但是，目標目錄不能包含任何源檔案。

**查看有關加密檔案的資訊：**

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

**查看有關元資料檔案的資訊：**

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` 是 [!DNL .metadata] 包含DRM元資料的檔案。

>[!NOTE]
>
>在打包期間，介質打包器無法再生成 [!DNL .header] 檔案。 生成 [!DNL .header] 檔案，使用 `-h` 選項。

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置檔案的名稱和位置。 </p> <p class="- topic/p ">如果未指定名稱或位置，DRM介質包器將搜索 <span class="filepath"> flashaccessols.properties </span> 的子菜單。 </p> <p>注：在命令行上指定的選項優先於在配置檔案中指定的選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph"> 加密檔案 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許您查看有關已打包的檔案的資訊。 </p> <p class="- topic/p ">源檔案和目標檔案不是必需的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> 元資料 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">使您能夠查看有關現有元資料的資訊。 </p> <p class="- topic/p ">源檔案和目標檔案不是必需的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在與 <span class="codeph"> -d </span> 的雙曲餘切值。 </p> <p class="- topic/p ">在加密檔案所在的同一目錄中自動建立檔案，該目錄具有檔案名和DRM策略標識符。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在與 <span class="codeph"> -d </span> 的雙曲餘切值。 </p> <p class="- topic/p ">在加密檔案所在的目錄中自動建立一個檔案，檔案的副檔名為 <span class="filepath"> .header </span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> 內容ID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定此內容段的唯一標識符。 </p> <p class="- topic/p ">如果未指定標識符，則將自動應用目標檔案名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> 鍵 </span>= <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要添加到內容元資料的自定義鍵/值。 </p> <p class="- topic/p ">可以指定多個 <span class="codeph"> -k </span> 頁籤 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">將此選項與 <span class="codeph"> -d </span> 的雙曲餘切值。 </p> <p class="- topic/p ">檔案將自動建立在與加密檔案相同的目錄下，其中包含檔案名和 <span class="codeph"> .元資料 </span> 擴展。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要詢問是否應覆蓋目標檔案。 </p> <p class="- topic/p ">如果目標檔案已存在，並且 <span class="codeph"> -o </span> 未設定，則出現錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">覆蓋目標檔案，但不會提示您，除非它已存在。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> 檔案名[域 — 傳輸 — 證書] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定包含DRM策略的檔案的名稱。 </p> <p class="- topic/p ">如果DRM策略要求向使用傳輸證書而不是在屬性檔案中指定的傳輸證書的伺服器註冊域，則需要提供域傳輸證書。 </p> <p class="- topic/p ">可以指定多個 <span class="codeph"> -p </span> 頁籤 預設情況下，客戶端始終應用第一個選項。 在命令行上指定的值優先於在配置檔案中指定的值。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 配置屬性 {#configuration-properties}

<!--<a id="section_3081C60BE54D47569FD1E3793513A2D9"></a>-->

>[!NOTE]
>
>對於包含* n*的屬性名， *n* 表示以1開頭的整數，並為屬性的每個實例增加。

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
   <td colname="2" class="- topic/entry "> 指示是否加密視頻內容。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.audio</span> </td> 
   <td colname="2" class="- topic/entry "> 指示是否加密音頻。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.script</span> </td> 
   <td colname="2" class="- topic/entry "> <p>指示是否加密mp4中的指令碼資料。 </p> <p><i class="+ topic/ph hi-d/i ">元資料</i> 和 <i class="+ topic/ph hi-d/i ">在XMP上</i> 即使啟用此選項，指令碼資料標籤也不會被加密。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示視頻加密級別。 </p> <p class="- topic/p ">值 <span class="codeph"> 高</span> 用於加密所有視頻內容，而 <span class="codeph"> 介質</span> 和 <span class="codeph"> 低</span> 用於加密包含H.264內容的mp4檔案的視頻內容的部分。 </p> <p class="- topic/p ">值= <span class="codeph"> 高 |中 |低</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.seconds未加密</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果值大於0，則不加密檔案開頭指定的內容秒數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.cerfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用於加密密鑰的許可證伺服器證書檔案。 </p> <p class="- topic/p ">的 <span class="codeph"> encrypt.keys.asymmetric.cerfile</span> 屬性指定僅包含證書的檔案（PEM或DER格式可接受）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">此屬性反複用於建立要應用於內容的DRM策略清單。 <span class="codeph"> n</span> 表示值為1或更大的整數。 預設情況下，客戶端使用第一個實例。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">許可證伺服器URL </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">許可證伺服器的傳輸證書。 </p> <p class="- topic/p ">此屬性指定 <span class="filepath"> .cer</span> 僅包含證書的檔案（PEM或DER格式可接受）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.cerfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">PKCS12檔案，包括用於簽名內容的打包器憑據。 </p> <p class="- topic/p ">的 <span class="codeph"> encrypt.sign.cerfile</span> 需要參考 <span class="filepath"> .pfx</span> 包含證書和私鑰的檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> 加密.sign.cerpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可應用於保護由指定的檔案的密碼 <span class="codeph"> encrypt.sign.cerfile</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">設定為要打包的內容頒發許可證所需的最低伺服器版本。 </p> <p class="- topic/p ">指定x（用於Mogine DRM x.0），其中x表示主發行號。 Adobe Primetime版本3.0之前的任何伺服器版本都不支援此設定。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n .domain.transportcert </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果DRM策略 <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> 需要向支援傳輸證書（您在中指定的證書除外）的伺服器註冊域 <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>，則需要提供域傳輸證書的需要。 </p> <p class="- topic/p ">此屬性指定僅包含證書的檔案（PEM或DER格式可接受）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定許可證密鑰。 </p> <p class="- topic/p ">如果未指定密鑰，則會隨機生成該密鑰。 如果不啟用密鑰輪替，則可以使用此密鑰加密內容。 </p> <p class="- topic/p ">啟用密鑰輪替時，可以使用此密鑰保護旋轉密鑰。 該密鑰的長度必須為16個位元組，並指定為十六進位值。 十六進位值之間的空格是可選的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定是否啟用密鑰輪替。 </p> <p class="- topic/p ">如果設定為false（是預設設定），則禁用密鑰輪替，並使用主CEK對內容中的所有示例進行加密。 </p> <p class="- topic/p ">如果設定為true，則啟用密鑰輪替，並可以使用不同的密鑰來加密任何內容的段。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">啟用密鑰輪替時可指定以加密內容的旋轉密鑰序列。 </p> <p class="- topic/p ">如果未指定任何鍵，則會隨機生成鍵。 密鑰的長度必須為16個位元組，並指定為十六進位值。 </p> <p class="- topic/p ">十六進位值之間的空格是可選的。 <i class="+ topic/ph hi-d/i ">n</i> 必須單調遞增，從1開始。 指定多個鍵時，按您指示的順序循環使用鍵。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定可以應用旋轉密鑰加密內容示例的時間間隔（秒）。 </p> <p class="- topic/p ">在經過已加密內容的時間間隔之後，然後應用下一旋轉密鑰。 如果已啟用密鑰輪替，但未指定任何時間間隔，則每15分鐘自動輪替一次密鑰。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果此選項設定為true，則無法獲得許可證的許可證伺服器。 </p> <p class="- topic/p ">許可證必須嵌入或帶外獲取。 除非您指定其他值，否則預設值將設定為false。 此選項僅在Mogife DRM Professional中受支援。 </p> </td> 
  </tr> 
 </tbody> 
</table>
