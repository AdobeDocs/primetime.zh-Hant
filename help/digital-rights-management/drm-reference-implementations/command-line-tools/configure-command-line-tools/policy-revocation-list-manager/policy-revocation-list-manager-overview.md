---
title: DRM吊銷清單管理器
description: DRM吊銷清單管理器
copied-description: true
exl-id: 5b17d195-30ca-4005-b710-83a6f77779a2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# DRM吊銷清單管理器 {#policy-revocation-list-manager}

使用黃金時段DRM吊銷清單管理器命令行工具( [!DNL AdobeRevocationListManager.jar])建立和管理吊銷清單，並檢查策略是否已吊銷。

運行前 [!DNL AdobeRevocationListManager.jar]，必須在 *策略更新清單管理器和吊銷清單管理器屬性* 的下界。

>[!NOTE]
>
>也可以從命令行指定所有「吊銷清單管理器」屬性。

## 吊銷清單管理器命令行用法 {#revocation-list-manager-command-line-usage}

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

* `destfile` 指定保存吊銷清單屬性的檔案的名稱。
* `crlNumber` 表示證書吊銷清單(CRL)的非負版本號。 每次更新CRL時，都需要增加此數。

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
   <td colname="2" class="- topic/entry "><p class="- topic/p ">指定配置檔案的名稱和位置。 </p><p class="- topic/p ">如果未指定名稱或位置，則DRM吊銷清單管理器將搜索 <span class="filepath"> flashaccessols.properties</span> 的子菜單。 </p><p>注：在命令行上指定的選項優先於在配置檔案中指定的選項。 </p>指定配置檔案的位置。 如果不應用此選項，則吊銷清單管理器將搜索 <span class="filepath"> flashaccessols.properties</span> 的子菜單。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d檔案名</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">顯示有關吊銷清單的資訊。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e日期</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（可選）吊銷清單的到期日期。 使用以下格式之一： 
     <ul id="ul_2C89F8183C3647C593CB67576D9DED07"> 
      <li id="li_A866F6CBCB464193A119A6609C8F3B2A"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> </li> 
      <li id="li_B5F9F6C995E64464838DDE447848F707"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span> </li> 
     </ul>例如，2009-01-31-14:30:00表示1月31日下午2:30 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f檔案名[certfile]</span> </td> 
   <td colname="2" class="- topic/entry "> <p>添加現有吊銷清單中的所有條目。 只能指定一個現有檔案。 </p> <p class="- topic/p ">如果現有清單是使用您用來簽署新清單的憑據以外的憑據簽名的，則需要在驗證其簽名的旁邊指定其證書檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要詢問是否應覆蓋目標檔案。 如果目標檔案已存在，並且 <span class="codeph"> -o</span> 未設定，出現錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目標檔案已存在，則無需提示即可覆蓋它。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber revocationDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">撤消已由 <span class="codeph"> 頒發者名稱</span> 和 <span class="codeph"> 序列號</span> 在指定日期。 的 <span class="codeph"> 頒發者名稱</span> 必須使用509名稱格式。 比如說， <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>。 </p> <p>必須以十六進位格式指定序列號。 您還需要使用以下格式之一指定吊銷日期： 
     <ul id="ul_1524FBC6818248F3A2B271243E649400"> 
      <li id="li_BC618EA2332D42A59B1B5434CAFFD2AF"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> </li> 
      <li id="li_97F77810D20C4CF2944EFCFF5DFAE467"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span> </li> 
     </ul>例如，2008-12-1或2008-12-1-00:00:2008年12月1日午夜0點。 如果未指定吊銷日期，則系統會自動應用當前日期。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 配置屬性 {#configuration-properties}

您需要應用憑據來簽署吊銷清單。 以下「吊銷清單管理器」屬性指定PKCS12檔案，該檔案包括簽名吊銷清單（許可證伺服器證書）的憑據以及證書的密碼：

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`
