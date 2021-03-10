---
title: 命令列使用
description: 命令列使用
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---


# 命令行用法{#command-line-usage}

在使用Media Packager之前，請確定您符合「需求」中所列的要求，且設定檔包含必要資訊(請參閱&#x200B;*使用Adobe存取參考實作*&#x200B;中的設定檔。

Media Packager位於DVD的[!DNL \Reference Implementation\Command Line tools]目錄中。 若要加密單一檔案，請使用下列語法：

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
* `dest` 指定加密內容的寫入位置。如果指定了目錄，則加密檔案將使用與源檔案相同的檔案名保存在此資料夾中，但該目錄不能是包含源檔案的目錄。

若要使用相同的金鑰加密多個檔案（針對多位元速率支援），請使用下列語法：

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

* `sourcefiles` 是一系列以空格分隔的來源項，代表要加密的檔案。
* `dest-directory` 指定加密內容的寫入位置。加密的檔案將使用與源檔案相同的檔案名保存在此資料夾中，但目錄不能是包含源檔案的目錄。

要查看加密檔案的資訊，請使用以下語法：

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

* `metadatafile` 是包含 [!DNL .metadata] DRM元資料的檔案。

>[!NOTE]
>
>在封裝期間，Media Packager預設不會再產生。header檔案。 若要產生此檔案，請在封裝期間使用`-h`選項。

下表包含上述語法中所示命令行選項的說明：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_wgz_spy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-c <span class="+ topic/ph pr-d/codeph codeph">configfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置檔案的位置。 如果未使用此選項，Media Packager將在工作目錄中查找<span class="filepath"> flashaccessools.properties </span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph">加密檔案</span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">顯示已打包檔案的相關資訊。 源檔案和目標檔案不是必需的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> metadatafile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">顯示現有中繼資料的相關資訊。 源檔案和目標檔案不是必需的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">將此選項與<span class="codeph"> -d </span>一起使用，從打包的檔案中提取策略。 將使用檔案名和策略標識符在與加密檔案相同的目錄中建立檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">與<span class="codeph"> -d </span>一起使用，從打包的檔案中提取DRM頭。 使用檔案名和副檔名<span class="filepath"> .header </span>在與加密檔案相同的目錄中建立檔案 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定此內容的唯一識別碼。 如果未指定任何標識符，則將使用目標檔案名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph">鍵</span>= <span class="+ topic/ph pr-d/codeph codeph">值</span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要新增至內容中繼資料的自訂索引鍵／值。 可以指定多個<span class="codeph"> -k </span>選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">此選項與<span class="codeph"> -d </span>一起使用，可從封裝的檔案擷取中繼資料。 將使用檔案名和副檔名<span class="codeph"> .metadata </span>在加密檔案的同一目錄中建立檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">請勿詢問是否應覆寫目標檔案。 如果目標檔案已存在且未設定<span class="codeph"> -o </span> ，則將返回錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">覆寫目標檔案（如果檔案已存在）而不出現提示。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph">檔案名[domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定包含策略的檔案的名稱。 如果策略要求向使用與屬性檔案中指定的傳輸證書不同的伺服器註冊域，則還需要提供域傳輸證書。 </p> <p class="- topic/p ">可以指定多個<span class="codeph"> -p </span>選項，預設情況下，客戶端將使用第一個選項。 命令行上指定的值優先於配置檔案中指定的值。 </p> </td> 
  </tr> 
 </tbody> 
</table>

