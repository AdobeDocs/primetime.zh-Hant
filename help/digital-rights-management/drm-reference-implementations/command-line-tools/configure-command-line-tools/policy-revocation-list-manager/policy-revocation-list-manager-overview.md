---
seo-title: DRM撤銷清單管理員
title: DRM撤銷清單管理員
uuid: 30ab5f54-4aac-4535-b30c-b4e5dbfbc475
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# DRM撤銷清單管理器{#policy-revocation-list-manager}

使用Primetime DRM撤銷清單管理器命令列工具([!DNL AdobeRevocationListManager.jar])來建立和管理撤銷清單，並檢查原則是否已撤銷。

在運行[!DNL AdobeRevocationListManager.jar]之前，必須在配置檔案的&#x200B;*策略更新清單管理器和撤銷清單管理器屬性*&#x200B;部分中設定屬性。

>[!NOTE]
>
>您也可以從命令行指定所有「撤銷清單管理器」屬性。

## 撤銷清單管理器命令行用法{#revocation-list-manager-command-line-usage}

```
java -jar AdobeRevocationListManager.jar 
<i class="+ topic ph hi-d="" i "="">
 destfile 
 <i class="+ topic ph hi-d="" i "="">
  crlNumber [
  <i class="+ topic ph hi-d="" i "="">
   options] 
       java -jar AdobeRevocationListManager.jar -d 
   <i class="+ topic ph hi-d="" i "="">
     filename
   </i class="+ topic>
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `destfile` 指定保存撤銷清單屬性的檔案的名稱。
* `crlNumber` 表示「證書撤銷清單」(CRL)的非負版本號。每次更新CRL時，都需要增加此數字。

**表5:命令行選項**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_a3y_wqy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 命令行選項 </th> 
   <th colname="2" class="- topic/entry entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c配置檔案</span> </td> 
   <td colname="2" class="- topic/entry "><p class="- topic/p ">指定配置檔案的名稱和位置。 </p><p class="- topic/p ">如果您未指定名稱或位置，DRM撤銷清單管理器會在目前工作目錄中搜尋<span class="filepath"> flashaccessools.properties</span>。 </p><p>注意： 在命令行上指定的選項優先於在配置檔案中指定的選項。 </p>指定配置檔案的位置。 如果您未套用此選項，「撤銷清單管理員」會在工作目錄中搜尋<span class="filepath"> flashaccessools.properties</span>。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d檔案名</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">顯示關於撤銷清單的資訊。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e日期</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（選擇性）撤銷清單的到期日。 使用下列格式之一： 
     <ul id="ul_2C89F8183C3647C593CB67576D9DED07"> 
      <li id="li_A866F6CBCB464193A119A6609C8F3B2A"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> </li> 
      <li id="li_B5F9F6C995E64464838DDE447848F707"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span> </li> 
     </ul>例如，2009-01-31-14:30:00代表1月31日下午2:30。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f檔案名[certfile]</span> </td> 
   <td colname="2" class="- topic/entry "> <p>從現有撤銷清單新增所有項目。 您只能指定一個現有檔案。 </p> <p class="- topic/p ">如果現有清單的簽署憑證不是您用來簽署新清單的憑證，則您必須在確認其簽名旁指定其憑證檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">請勿詢問是否應覆寫目標檔案。 如果目標檔案已存在且未設定<span class="codeph"> -o</span> ，則會出現錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目標檔案已存在，則無需提示即可覆蓋它。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber revocationDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">撤銷在指定日期由<span class="codeph"> issuberName</span>和<span class="codeph"> serialNumber</span>識別的憑證。 <span class="codeph"> issuberName</span>必須使用509名稱格式。 例如，<span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>。 </p> <p>您必須以十六進位格式指定序列號。 您也需要以下列其中一種格式指定撤銷日期： 
     <ul id="ul_1524FBC6818248F3A2B271243E649400"> 
      <li id="li_BC618EA2332D42A59B1B5434CAFFD2AF"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> </li> 
      <li id="li_97F77810D20C4CF2944EFCFF5DFAE467"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span> </li> 
     </ul>例如，2008年12月1日午夜的2008-12-1或2008-12-1-00:00:00。 如果您未指定撤銷日期，則會自動套用目前日期。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 配置屬性{#configuration-properties}

您必須套用認證才能簽署撤銷清單。 以下「撤銷清單管理器」屬性指定PKCS12檔案，該檔案包括用於簽署撤銷清單（許可證伺服器證書）的憑據，以及證書的密碼：

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`