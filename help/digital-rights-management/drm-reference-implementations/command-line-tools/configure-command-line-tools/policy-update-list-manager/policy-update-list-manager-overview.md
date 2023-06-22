---
title: 概觀
description: 概觀
copied-description: true
exl-id: 1e06bead-4b45-4bf0-8bcf-1ea376af6bd8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# DRM原則更新清單管理員 {#policy-update-list-manager}

使用Primetime DRM原則更新清單管理員命令列工具( [!DNL AdobePolicyUpdateListManager.jar])，以建立和管理DRM原則更新清單，並檢查原則是否已更新或撤銷。

執行「原則更新清單管理員」命令列工具之前，您必須在 *原則更新清單管理員和撤銷清單管理員屬性* 區段。

>[!NOTE]
>
>您也可以從命令列指定所有「原則更新清單管理員」屬性。

## 原則更新清單管理員命令列使用方式 {#policy-update-list-manager-command-line-usage}

**建立原則更新清單：**

```
java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` 指示寫入DRM原則更新清單的檔案名稱。

**檢視現有的原則更新清單：**

```
java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

* `filename` 原則更新清單檔案的名稱。

**表4：命令列選項**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令列選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c設定檔 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定組態檔的名稱和位置。 </p> <p class="- topic/p ">如果您未指定名稱或位置，則「DRM原則更新清單管理員」會搜尋 <span class="filepath"> flashaccesstools.properties </span> 在目前工作目錄中。 </p> <p>注意：您在命令列上指定的選項優先於您在組態檔案中指定的選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d檔案名稱 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">顯示DRM原則更新清單的相關資訊。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p>（選用） DRM原則更新清單的到期日。 </p> <p>使用格式 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span> (例如，2009-01-31-14:30:00代表1月31日下午2:30)。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f檔案名稱[certfile] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">新增現有DRM原則更新清單中的所有專案。 您只能指定一個現有檔案。 </p> <p class="- topic/p ">如果現有清單已使用用於簽署新清單的認證以外的認證進行簽署，則您需要指定其憑證檔案以驗證其簽名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要詢問是否應該覆寫目的地檔案。 如果目的地檔案已存在且 <span class="codeph"> -o </span> 未設定，則會發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目的地檔案已經存在，請覆寫它而不提示。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyID </span> <span class="+ topic/ph pr-d/codeph codeph"> 日期 </span> " <span class="+ topic/ph pr-d/codeph codeph"> 原因代碼 </span>「 」 <span class="+ topic/ph pr-d/codeph codeph"> 原因文字 </span>「 」 <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（可選）在指定的日期撤銷DRM原則ID。 您可以提供選擇性的原因代碼、原因文字和原因URL。 您需要指定空字串「」，以表示未提供選用引數的值。 您可以指定日期於 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span> 這些格式時。 例如，2008-12-1或2008-12-1-00:00:00代表2008年12月1日的午夜)。 如果您未指定日期，則會自動套用目前的日期。 因此，原因代碼必須大於或等於0。 您也可以指定多個 — r選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> 日期 </span> " <span class="+ topic/ph pr-d/codeph codeph"> 原因代碼 </span>「 」 <span class="+ topic/ph pr-d/codeph codeph"> 原因文字 </span>「 」 <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">執行與相同的動作 <span class="codeph"> -r </span> 選項。 不過，它會從指定的檔案中擷取DRM原則識別碼。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" " reasonURL" </span> </td> 
   <td colname="2" class="- topic/entry "> <p>使用指定的原因代碼（選擇性）、原因文字（選擇性）和原因URL （選擇性），以此DRM原則取代授權請求中的任何相符的DRM原則。 </p> <p>空白字串「」表示您尚未為選用引數提供任何值。 </p> <p>原因代碼必須大於或等於 <span class="codeph"> 0 </span>. 您可以指定多個 <span class="codeph"> -u </span> 選項。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 設定屬性 {#configuration-properties}

下列Primetime DRM原則更新清單管理員屬性會指定PKCS12檔案，其中包含簽署撤銷清單的認證（授權伺服器憑證）以及密碼。

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`
