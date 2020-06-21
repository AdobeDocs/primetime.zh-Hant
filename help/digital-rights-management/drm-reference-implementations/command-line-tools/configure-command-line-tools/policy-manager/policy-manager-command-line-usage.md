---
description: 'null'
seo-description: 'null'
seo-title: 策略管理器命令行使用
title: 策略管理器命令行使用
uuid: 9b17bc9a-0b1b-405f-a62b-0310c43c9255
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---


# 策略管理器命令行使用 {#policy-manager-command-line-usage}

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

**表1: 命令**

| 命令 | 說明 |
|---|---|
| `new` | 建立新的DRM策略 |
| `detail` | 描述現有的DRM策略 |
| `update` | 更新現有的DRM政策 |

**表2: 選項**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c配置檔案 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置檔案的名稱和位置。 </p> <p class="- topic/p ">如果未指定名稱或位置，DRM策略管理器將在當前工作目錄中 <span class="filepath"> 搜索flashaccessools. </span> properties。 </p> <p>注意：  在命令行上指定的選項優先於在配置檔案中指定的選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目標檔案存在，則無需提示即可覆寫檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">請勿詢問是否應覆寫目標檔案。 如果目標檔案存在且 <span class="codeph"> 未設 </span> 置-o，則發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">表示DRM策略具有根許可。 </p> <p class="- topic/p ">此選項不適用於更新。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權生效的日期。 </p> <p>您可以指定 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd或yyyy-mm-dd-h24:min:sec格式的日 </span><span class="+ topic/ph pr-d/codeph codeph"></span> 期。 例如，2008年12月1日午夜的2008-12-1或2008-12-1-00:00:00。 </p> <p> 
     <ul id="ul_D5DB5044756D4BD6A734813971598425"> 
      <li id="li_B6BD62A524384060A9DDA14FF50936FA">值必須大於-s的值(如 <span class="codeph"> 果存 </span> 在)。 </li> 
      <li id="li_C3C5AD0231A240EC9AC57685B9206E8D">不能將此選項與 <span class="codeph"> -r一起應用 </span>。 </li> 
      <li id="li_3790E2F829A149979BF44E0914CFF431">要在更新DRM策略時刪除結束日期，請在不指 <span class="codeph"> 定日 </span> 期的情況下應用-e。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r分鐘 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">受保護內容有效的持續時間（分鐘）。 </p> <p class="- topic/p ">當內容使用封裝器保護時，DRM原則就會生效。 </p> <p> 
     <ul id="ul_4690A0E4677A4DF6A006B7FCBD46F1BE"> 
      <li id="li_D1F098D44B494EE7A8647C0B62D5ACFA">值必須是非負值。 </li> 
      <li id="li_ADFDCB01EEE04B37AFA42886AAEF47EB">您不能將此選項與 <span class="codeph"> -e一起應用 </span>。 </li> 
      <li id="li_E80563E68BEB43FC9E29A694594CAE01">要在更新DRM策略時刪除或刪除持續時間，請應用 <span class="codeph"> -r而不 </span> 需指定任何分鐘。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權生效的日期。 </p> <p>您可以指定 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd或yyyy-mm-dd-h24:min:sec格式的日 </span><span class="+ topic/ph pr-d/codeph codeph"></span> 期。 例如， <span class="codeph"> 2008年12月1日 </span> 的 <span class="codeph"></span> 午夜為2008-12-12-1-00:00:00。 </p> <p> 
     <ul id="ul_D52B337F547F4E7AB87FE025236CA930"> 
      <li id="li_DBAE380972434DB1A4EF20D399038AB8">值必須小於-e的值(如 <span class="codeph"> 果 </span>存在)。 </li> 
      <li id="li_2899EC5559CF44319A4AC4ECD90A5B9A">您不能將此選項與 <span class="codeph"> -r一起應用 </span>。 </li> 
      <li id="li_19861B1A64E44B95B649948EAB3E4085">要在更新DRM策略時刪除或刪除開始日期，請使用 <span class="codeph"> -s而 </span> 不指定日期。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w [&lt;分鐘&gt;[,enableHS|disableHS]] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">播放視窗，這是從第一次播放中可檢視內容的分鐘數。 </p> <p>如果未指定，或 <span class="codeph"> 者使 </span> 用-w而未指定分鐘數，則沒有播放窗口限制。 值必須是非負值。 </p> <p>可選的 <span class="codeph"> enableHS </span> 或disable <span class="codeph"> HS標誌 </span> 信號表示要啟用或禁用硬停止。 該標誌指示解密上下文在播放窗口的結尾處是否被破壞（啟用）或未被破壞（禁用）。 </p> <p>例如，若要指定內容只能檢視60分鐘，而且需要硬停止： 
     <codeblock>
       -w&amp;nbsp;60,enableHS 
     </codeblock> </p> <p>注意：  <i>Flash Player</i> 、Android和iOS目前不支援硬式停止功能。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l分鐘 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權快取持續時間是指授權在伺服器核發後，可在用戶端的授權商店中快取授權的時間（以分鐘為單位）。 值必須是非負值。 </p> <p>您可以指 <span class="codeph"> 定-l </span> 0以指出不允許進行授權快取。 若為不限次數的授權快取，請 <span class="codeph"> 指定-l </span> ，不需要幾分鐘。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -ldate </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權快取結束日期。 </p> <p class="- topic/p ">這表示Primetime DRM伺服器核發授權後，用戶端可在用戶端的授權商店中快取授權的最後日期。 </p> <p>您可以以下列格式指定日期： 
     <ul id="ul_112DE7248A9C48B19520A3AA9E5D1F03"> 
      <li id="li_01C5400E78B84A3B8955972FBA875AAC"> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> </li> 
      <li id="li_AA13B1EFA07A4542A3DB41FA3320B143"> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span> </li> 
     </ul>例如， <span class="codeph"> 2008年12月1日 </span> 的 <span class="codeph"></span> 午夜為2008-12-12-1-00:00:00。 您需要套用 <span class="codeph"> -l，而 </span> 不需指定任何分鐘，即可無限制進行授權快取。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">驗證命名空間。 </p> <p class="- topic/p ">如果您套用此選項，則用戶端需要輸入由指定授權機構核發的使用者名稱和密碼。 </p> <p>不能將此選項與 <span class="codeph"> -x一起應用 </span>。 </p> <p>更新不允許使用此選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許匿名存取。 </p> <p class="- topic/p ">您不能將此選項與 <span class="codeph"> -authNS一起應用 </span>。 </p> <p class="- topic/p ">更新不允許使用此選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId </span>[: <span class="+ topic/ph pr-d/codeph codeph"> appId </span>[:[ <span class="+ topic/ph pr-d/codeph codeph"> 最小 </span>]:[最大 <span class="+ topic/ph pr-d/codeph codeph"></span>]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可播放受保護內容的AIR應用程式允許清單。 </p> <p class="- topic/p ">您可以套用此選項，以限制哪些發佈者、應用程式和版本可以存取使用此DRM原則保護的內容。 </p> <p class="- topic/p ">如果您未指定 <i class="+ topic/ph hi-d/i ">appId</i>，則允許發佈者 <i class="+ topic/ph hi-d/i ">pubId的所有應用程</i> 式。 </p> <p>注意：  <i class="+ topic/ph hi-d/i ">最小</i> 和最 <i class="+ topic/ph hi-d/i ">大版本號</i> 為可選。 </p> <p class="- topic/p ">您可以指定多個 <span class="codeph"> -air選項 </span> 來允許多個應用程式。 如果您未指定AIR或SWF應用程式，所有應用程式都可存取此內容。 在更新期間，要從清單中刪除或刪除所有條目，請應用 <span class="codeph"> -air而不 </span> 使用其餘參數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmBlacklist name </span> / <i class="+ topic/ph hi-d/i ">value</i><span class="+ topic/ph pr-d/codeph codeph"></span><i class="+ topic/ph hi-d/i "></i><span class="+ topic/ph pr-d/codeph codeph"> pairs </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">受到限制的DRM客戶端無法訪問受保護的內容。 </p> <p class="- topic/p ">值支援以下格式的逗號分隔名稱：值對： </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | release= stringValue </span> </p> <p class="- topic/p ">例如， <span class="codeph"> os=Win,release=2.0.1 </span>。 在更新期間，要從清單中刪除所有條目，請應用 <span class="codeph"> -drmBlacklist，而不 </span> 使用其餘引數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指出DRM用戶端必須有指定的最低安全等級才能存取受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog NO_PROTECTION | USE_IF_AVAILABLE |必要 | NO_PLAYBACK |必要_ACP |必要_CGMSA | USE_IF_AVAILABLE_ACP | USE_IF_AVAILABLE_CGMSA </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">模擬輸出保護限制 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE |必要 | NO_PLAYBACK </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">數位輸出保護限制 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtime黑名單名 </span> 稱/ <i class="+ topic/ph hi-d/i ">值</i> 值對 <span class="+ topic/ph pr-d/codeph codeph"> 的 </span><i class="+ topic/ph hi-d/i "></i><span class="+ topic/ph pr-d/codeph codeph"> Laklist </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">限制存取受保護內容的應用程式執行時期。 </p> <p class="- topic/p ">值支援以下格式的逗號分隔名稱：值對： </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os |應用程式 | release= stringValue </span> </p> <p class="- topic/p ">例如， <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>。 在更新期間，要從清單中刪除所有條目，請應用 <span class="codeph"> -runtimeBlacklist，而不 </span> 使用其餘引數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指出應用程式執行時期必須具備指定的最低安全等級才能存取受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf檔案= swf_file </span>, <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許播放受保護內容的SWF應用程式清單。 </p> <p class="- topic/p ">您可以指定多個 <span class="codeph"> -swf選 </span> 項，以允許多個應用程式。 如果您未指定任何AIR或SWF應用程式，所有應用程式都可存取此內容。 </p> <p>在更新期間，若要從清單中移除所有項目，請套用 <span class="codeph"> -swf </span> 而不需其餘引數。 如果您想要依據SWF的雜湊值來識別SWF，則需要指定要計算雜湊的SWF檔案，以及允許完成SWF驗證的最長時間（以秒為單位）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k名稱=值 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要添加到DRM策略的自定義密鑰／值。 </p> <p class="- topic/p ">您可以指定多 <span class="codeph"> 個-k </span> 選項。 在更新期間，如果要刪 <span class="codeph"> 除所有 </span> 屬性，可以應用-k而不應用其餘參數。 資料的解釋或處理由Primetime DRM許可伺服器管理。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p名稱=值 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">新增自訂屬性，該屬性會顯示在為每個用戶端產生的授權中。 </p> <p class="- topic/p ">您可以指定多個 <span class="codeph"> -p選 </span> 項來新增多個屬性。 在更新期間，如果要刪除所有 <span class="codeph"> 屬性， </span> 則需要應用-p而不應用其餘參數。 此資料的解釋或處理由用戶端應用程式的實作管理。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> <span class="codeph"> -opOTA白名單=&lt;連接類型&gt; </span> </span> </td> 
   <td colname="2" class="- topic/entry "> 空中(OTA)輸出保護限制。 白 <span class="codeph"> 名單字 </span> 段指定允許清單的連接類型和&lt;連接類型&gt;的格式為 <span class="codeph"> [type(,type)*] </span>，其中類型可以是以下任何類型： 奇跡，空中，維迪，德爾納 </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opResolution &lt;檔案名&gt; </span> </td> 
   <td colname="2" class="- topic/entry "> <p>指定檔案中定義的基於解析度的輸出保護約束。 </p> <p>此檔案的編碼為JSON。 格式的語法可在關於基於解析度 <i>的輸出保護中找到</i>。 </p> </td> 
  </tr> 
 </tbody> 
</table>

**範例**

要使用您自己的配置屬性檔案建立允許匿名訪問內容的策略：

```
java -jar libs\AdobePolicyManager.jar new policy_test.pol -x -c my_configuration.properties
```
