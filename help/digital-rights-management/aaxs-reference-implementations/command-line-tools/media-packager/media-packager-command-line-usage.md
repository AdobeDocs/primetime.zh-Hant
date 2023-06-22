---
title: 命令列使用方式
description: 命令列使用方式
copied-description: true
exl-id: 55b18fee-b7d8-4a5a-91a7-a08cd23e7866
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 命令列使用方式 {#command-line-usage}

使用Media Packager之前，請確定您符合需求中所列的要求，而且組態檔包含必要的資訊(請參閱 *使用Adobe存取參考實作*.

Media Packager位於 [!DNL \Reference Implementation\Command Line tools] 目錄。 若要加密單一檔案，請使用下列語法：

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

* `source` 是要加密的檔案。
* `dest` 指定將寫入加密內容的位置。 如果指定目錄，加密的檔案將會使用與來源檔案相同的檔案名稱儲存在此資料夾中，但目錄不能是包含來源檔案的目錄。

若要使用相同的金鑰加密多個檔案（支援多位元速率），請使用下列語法：

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

* `sourcefiles` 是以空格分隔的一系列來源專案，代表要加密的檔案。
* `dest-directory` 指定將寫入加密內容的位置。 加密的檔案會使用與來源檔案相同的檔案名稱儲存在此資料夾中，但目錄不能是包含來源檔案的目錄。

若要檢視加密檔案的相關資訊，請使用下列語法：

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

* `encryptedfile` 是加密的檔案。

若要檢視中繼資料檔案的相關資訊，請使用下列語法：

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` 是 [!DNL .metadata] 包含DRM中繼資料的檔案。

>[!NOTE]
>
>封裝期間，Media Packager預設不再產生.header檔案。 若要產生此檔案，請使用 `-h` 封裝期間選項。

下表包含上述語法中所顯示的命令列選項說明：

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定組態檔的位置。 如果未使用此選項，「媒體封裝程式」將會尋找 <span class="filepath"> flashaccesstools.properties </span> 於工作目錄中。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph"> encryptedfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">顯示已封裝檔案的相關資訊。 來源和目的地檔案並非必要檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> 中繼資料檔 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">顯示現有中繼資料的相關資訊。 來源和目的地檔案並非必要檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">使用此選項搭配 <span class="codeph"> -d </span> 從封裝檔案擷取原則。 將使用檔案名稱和原則識別碼，在加密檔案的相同目錄中建立檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">搭配使用 <span class="codeph"> -d </span> 從封裝檔案中擷取DRM標頭。 檔案會使用檔案名稱和副檔名，在與加密檔案相同的目錄中建立 <span class="filepath"> .header </span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定此內容片段的唯一識別碼。 如果未指定識別碼，將會使用destfile檔案名稱。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> 金鑰 </span>= <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要新增至內容中繼資料的自訂索引鍵/值。 多個 <span class="codeph"> -k </span> 可指定選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">使用此選項搭配 <span class="codeph"> -d </span> 以從封裝檔案擷取中繼資料。 將使用檔案名稱和副檔名在與加密檔案相同的目錄中建立檔案 <span class="codeph"> .metadata </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要詢問是否應該覆寫目的地檔案。 如果目的地檔案已存在且 <span class="codeph"> -o </span> 未設定，則會傳回錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">覆寫目的地檔案（如果已經存在），而不提示使用者。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> 檔案名稱[domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定包含原則的檔案名稱。 如果原則要求使用屬性檔案中指定的傳輸憑證以外的其他傳輸憑證的伺服器進行網域註冊，則還需要提供網域傳輸憑證。 </p> <p class="- topic/p ">多個 <span class="codeph"> -p </span> 可指定選項，使用者端預設會使用第一個選項。 命令列上指定的值優先於組態檔中指定的值。 </p> </td> 
  </tr> 
 </tbody> 
</table>
