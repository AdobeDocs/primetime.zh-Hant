---
title: DRM撤銷清單管理員
description: DRM撤銷清單管理員
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# DRM撤銷清單管理員 {#policy-revocation-list-manager}

使用Primetime DRM撤銷清單管理員命令列工具( [!DNL AdobeRevocationListManager.jar])以建立及管理撤銷清單，以及檢查原則是否已撤銷。

執行之前 [!DNL AdobeRevocationListManager.jar]，您必須在中 *原則更新清單管理員和撤銷清單管理員屬性* 區段。

>[!NOTE]
>
>您也可以從命令列指定所有「撤銷清單管理員」屬性。

## 撤銷清單管理員命令列使用方式 {#revocation-list-manager-command-line-usage}

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

* `destfile` 指定儲存撤銷清單屬性的檔案名稱。
* `crlNumber` 代表憑證撤銷清單(CRL)的非負數版本號碼。 每次更新CRL時，您都需要增加此數字。

**表5：命令列選項**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_a3y_wqy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 命令列選項 </th> 
   <th colname="2" class="- topic/entry entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c設定檔</span> </td> 
   <td colname="2" class="- topic/entry "><p class="- topic/p ">指定組態檔的名稱和位置。 </p><p class="- topic/p ">如果您未指定名稱或位置，則「DRM撤銷清單管理員」會搜尋 <span class="filepath"> flashaccesstools.properties</span> 於目前工作目錄中。 </p><p>注意：您在命令列中指定的選項優先於您在組態檔案中指定的選項。 </p>指定組態檔的位置。 如果您未套用此選項，「撤銷清單管理員」會搜尋 <span class="filepath"> flashaccesstools.properties</span> 於工作目錄中。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d檔案名稱</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">顯示撤銷清單的相關資訊。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e日期</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（選用）撤銷清單的到期日。 請使用下列其中一種格式： 
     <ul id="ul_2C89F8183C3647C593CB67576D9DED07"> 
      <li id="li_A866F6CBCB464193A119A6609C8F3B2A"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> </li> 
      <li id="li_B5F9F6C995E64464838DDE447848F707"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span> </li> 
     </ul>例如：2009-01-31-14:30:00代表1月31日下午2:30。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f filename[certfile]</span> </td> 
   <td colname="2" class="- topic/entry "> <p>從現有的撤銷清單新增所有專案。 您只能指定一個現有檔案。 </p> <p class="- topic/p ">如果現有清單是使用您用來簽署新清單的認證以外的認證所簽署，則您必須指定其憑證檔案，以驗證其簽章。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要詢問是否應該覆寫目的地檔案。 如果目的地檔案已存在，並且 <span class="codeph"> -o</span> 未設定，則會發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目的地檔案已經存在，您便可以覆寫該檔案，而不需要系統提示。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber撤銷日期</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">撤銷已識別的憑證 <span class="codeph"> issuerName</span> 和 <span class="codeph"> 序號</span> 於指定日期。 此 <span class="codeph"> issuerName</span> 必須使用509名稱格式。 例如， <span class="codeph"> CN=12345，O=Adobe Systems Incorporated，C=US</span>. </p> <p>您必須以十六進位格式指定序號。 您還需要以下列其中一種格式指定撤銷日期： 
     <ul id="ul_1524FBC6818248F3A2B271243E649400"> 
      <li id="li_BC618EA2332D42A59B1B5434CAFFD2AF"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> </li> 
      <li id="li_97F77810D20C4CF2944EFCFF5DFAE467"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span> </li> 
     </ul>例如：2008-12-1或2008-12-1-00:00:2008年12月1日午夜00。 若未指定撤銷日期，系統會自動套用目前日期。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 設定屬性 {#configuration-properties}

您必須套用認證以簽署撤銷清單。 下列「撤銷清單管理員」屬性會指定PKCS12檔案，其中包含簽署撤銷清單（授權伺服器憑證）的認證，以及憑證的密碼：

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`
