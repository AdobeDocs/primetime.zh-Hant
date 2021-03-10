---
title: 概觀
description: 概觀
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---


# DRM策略更新清單管理器{#policy-update-list-manager}

使用Primetime DRM策略更新清單管理器命令行工具([!DNL AdobePolicyUpdateListManager.jar])建立和管理DRM策略更新清單，並檢查策略是否已更新或撤銷。

在運行策略更新清單管理器命令行工具之前，必須在配置檔案的&#x200B;*策略更新清單管理器和撤銷清單管理器屬性*&#x200B;部分中設定屬性。

>[!NOTE]
>
>您也可以從命令行指定所有策略更新清單管理器屬性。

## 策略更新清單管理器命令行用法{#policy-update-list-manager-command-line-usage}

**建立策略更新清單：**

```
java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` 指示寫入DRM策略更新清單的檔案的名稱。

**查看現有策略更新清單：**

```
java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

* `filename` 策略更新清單檔案的名稱。

**表4:命令行選項**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c配置檔案  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置檔案的名稱和位置。 </p> <p class="- topic/p ">如果未指定名稱或位置，DRM策略更新清單管理器將在當前工作目錄中搜索<span class="filepath"> flashaccessools.properties </span>。 </p> <p>注意： 在命令行上指定的選項優先於在配置檔案中指定的選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d檔案名  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">顯示有關DRM策略更新清單的資訊。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e日期  </span> </td> 
   <td colname="2" class="- topic/entry "> <p>（可選）DRM策略更新清單的到期日。 </p> <p>使用格式<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span>或<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>（例如，2009-01-31-14:30:00代表1月31日下午2:30）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f檔案名[certfile]  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">從現有DRM策略更新清單添加所有條目。 您只能指定一個現有檔案。 </p> <p class="- topic/p ">如果現有清單的簽署憑證不是用於簽署新清單的憑證，則您必須指定其憑證檔案以驗證其簽名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">請勿詢問是否應覆寫目標檔案。 如果目標檔案已存在且未設定<span class="codeph"> -o </span> ，則會發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目標檔案已存在，請不提示而覆寫它。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyDATE  </span> <span class="+ topic/ph pr-d/codeph codeph"> date  </span> reasonCode " " "  <span class="+ topic/ph pr-d/codeph codeph"> reasonText  </span>" "reasonURL  <span class="+ topic/ph pr-d/codeph codeph">  </span> <span class="+ topic/ph pr-d/codeph codeph">  </span>ID" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（可選）在指定日期廢止DRM原則ID。 您可以提供可選的原因代碼、原因文字和原因URL。 您需要指定空字串""，以指出未為可選參數提供任何值。 您可以在<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span>或<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>中指定這些格式的日期。 例如，2008-12-1或2008-12-1-00:00:00代表2008年12月1日的午夜)。 如果您未指定日期，則會自動套用目前的日期。 因此，原因代碼必須大於或等於0。 您也可以指定多個-r選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> date </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">執行與<span class="codeph"> -r </span>選項相同的操作。 但是，它從指定檔案中提取DRM策略標識符。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" " reasonURL"  </span> </td> 
   <td colname="2" class="- topic/entry "> <p>使用指定的原因碼（選用）、原因文字（選用）和原因URL（選用），將授權要求中任何符合的DRM原則取代為此DRM原則。 </p> <p>空字串""表示您未為可選參數提供任何值。 </p> <p>原因代碼必須大於或等於<span class="codeph"> 0 </span>。 您可以指定多個<span class="codeph"> -u </span>選項。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 配置屬性{#configuration-properties}

以下Primetime DRM策略更新清單管理器屬性指定PKCS12檔案，該檔案包括用於簽署撤銷清單（許可證伺服器證書）的憑據以及密碼。

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`