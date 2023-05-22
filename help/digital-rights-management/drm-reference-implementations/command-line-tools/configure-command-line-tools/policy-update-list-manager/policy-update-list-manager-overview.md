---
title: 概述
description: 概述
copied-description: true
exl-id: 1e06bead-4b45-4bf0-8bcf-1ea376af6bd8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# DRM策略更新清單管理器 {#policy-update-list-manager}

使用Mogfire DRM策略更新清單管理器命令行工具( [!DNL AdobePolicyUpdateListManager.jar])建立和管理DRM策略更新清單，並檢查策略是否已更新或吊銷。

在運行「策略更新清單管理器」(Policy Update List Manager)命令行工具之前，必須在 *策略更新清單管理器和吊銷清單管理器屬性* 的下界。

>[!NOTE]
>
>也可以從命令行指定所有「策略更新清單管理器」屬性。

## 策略更新清單管理器命令行用法 {#policy-update-list-manager-command-line-usage}

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
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c配置檔案 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置檔案的名稱和位置。 </p> <p class="- topic/p ">如果未指定名稱或位置，則DRM策略更新清單管理器將搜索 <span class="filepath"> flashaccessols.properties </span> 的子菜單。 </p> <p>注：在命令行上指定的選項優先於在配置檔案中指定的選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d檔案名 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">顯示有關DRM策略更新清單的資訊。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p>（可選）DRM策略更新清單的到期日期。 </p> <p>使用格式 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span> (例如，2009-01-31-14:30:00表示1月31日下午2:30)。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f檔案名[certfile] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">添加現有DRM策略更新清單中的所有條目。 只能指定一個現有檔案。 </p> <p class="- topic/p ">如果現有清單已用除用於簽署新清單的憑據之外的憑據簽名，則需要指定其證書檔案以驗證其簽名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要詢問是否應覆蓋目標檔案。 如果目標檔案已存在，並且 <span class="codeph"> -o </span> 未設定，出現錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目標檔案已存在，則覆蓋它而不出現提示。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r策略ID </span> <span class="+ topic/ph pr-d/codeph codeph"> 日期 </span> " <span class="+ topic/ph pr-d/codeph codeph"> 原因代碼 </span>" <span class="+ topic/ph pr-d/codeph codeph"> 原因文本 </span>" <span class="+ topic/ph pr-d/codeph codeph"> 原因URL </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（可選）在指定日期撤消DRM策略ID。 可以提供可選的原因代碼、原因文本和原因URL。 需要指定空字串「」以指示沒有為可選參數提供值。 可以在中指定日期 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span> 格式。 例如，2008-12-1或2008-12-1-00:00:00代表2008年12月1日午夜)。 如果未指定日期，則系統會自動應用當前日期。 因此，原因代碼必須大於或等於0。 還可以指定多個 — r選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> 策略檔案名 </span> <span class="+ topic/ph pr-d/codeph codeph"> 日期 </span> " <span class="+ topic/ph pr-d/codeph codeph"> 原因代碼 </span>" <span class="+ topic/ph pr-d/codeph codeph"> 原因文本 </span>" <span class="+ topic/ph pr-d/codeph codeph"> 原因URL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">執行與 <span class="codeph"> -r </span> 的雙曲餘切值。 但是，它從指定檔案中提取DRM策略標識符。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" "reasonText" "reasonURL" </span> </td> 
   <td colname="2" class="- topic/entry "> <p>使用給定原因代碼（可選）、原因文本（可選）和原因URL（可選），將許可請求中的任何匹配DRM策略替換為此DRM策略。 </p> <p>空字串「」表示您未為可選參數提供任何值。 </p> <p>原因代碼必須大於或等於 <span class="codeph"> 0 </span>。 可以指定多個 <span class="codeph"> -u </span> 頁籤 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 配置屬性 {#configuration-properties}

以下Mogfi時段DRM策略更新清單管理器屬性指定PKCS12檔案，該檔案包括簽名吊銷清單（許可證伺服器證書）的憑據以及密碼。

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`
