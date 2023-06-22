---
title: Policy Manager命令列用法
description: Policy Manager命令列用法
copied-description: true
exl-id: 888be282-7eaa-4101-b4b1-4f8df99a967a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 0%

---

# Policy Manager命令列用法 {#policy-manager-command-line-usage}

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

**表1：命令**

| 命令 | 說明 |
|---|---|
| `new` | 建立新的DRM原則 |
| `detail` | 說明現有的DRM原則 |
| `update` | 更新現有的DRM原則 |

**表2：選項**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令列選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c設定檔 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定組態檔的名稱和位置。 </p> <p class="- topic/p ">如果您未指定名稱或位置，則「DRM原則管理員」會搜尋 <span class="filepath"> flashaccesstools.properties </span> 在目前工作目錄中。 </p> <p>注意：您在命令列上指定的選項優先於您在組態檔案中指定的選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目的地檔案存在，您可在不提示的情況下覆寫檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要詢問是否應該覆寫目的地檔案。 如果目的地檔案存在且 <span class="codeph"> -o </span> 未設定，則會發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指出DRM原則具有根授權。 </p> <p class="- topic/p ">此選項不適用於更新。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權生效的日期。 </p> <p>您可以指定日期於 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span> 格式。 例如，2008-12-1或2008-12-1-00:00:00 （2008年12月1日午夜）。 </p> <p> 
     <ul id="ul_D5DB5044756D4BD6A734813971598425"> 
      <li id="li_B6BD62A524384060A9DDA14FF50936FA">值必須大於下列專案的值： <span class="codeph"> -s </span> 如果有的話。 </li> 
      <li id="li_C3C5AD0231A240EC9AC57685B9206E8D">您無法將此選項套用至 <span class="codeph"> -r </span>. </li> 
      <li id="li_3790E2F829A149979BF44E0914CFF431">若要移除更新DRM原則的結束日期，請套用 <span class="codeph"> -e </span> 而不指定日期。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r分鐘 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">受保護內容有效的持續時間（分鐘）。 </p> <p class="- topic/p ">當內容受到封裝程式保護時，DRM政策會生效。 </p> <p> 
     <ul id="ul_4690A0E4677A4DF6A006B7FCBD46F1BE"> 
      <li id="li_D1F098D44B494EE7A8647C0B62D5ACFA">值必須為非負數。 </li> 
      <li id="li_ADFDCB01EEE04B37AFA42886AAEF47EB">您無法將此選項與 <span class="codeph"> -e </span>. </li> 
      <li id="li_E80563E68BEB43FC9E29A694594CAE01">若要移除或刪除更新DRM原則時的持續時間，請套用 <span class="codeph"> -r </span> 而不指定任何分鐘。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權生效的日期。 </p> <p>您可以在 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span> 格式。 例如， <span class="codeph"> 2008-12-1 </span> 或 <span class="codeph"> 2008-12-1-00:00:00 </span> 2008年12月1日午夜。 </p> <p> 
     <ul id="ul_D52B337F547F4E7AB87FE025236CA930"> 
      <li id="li_DBAE380972434DB1A4EF20D399038AB8">值必須小於的值 <span class="codeph"> -e </span>，如果有的話。 </li> 
      <li id="li_2899EC5559CF44319A4AC4ECD90A5B9A">您無法將此選項與 <span class="codeph"> -r </span>. </li> 
      <li id="li_19861B1A64E44B95B649948EAB3E4085">若要在更新DRM原則時移除或刪除開始日期，請使用 <span class="codeph"> -s </span> 而不指定日期。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w [&lt;minutes&gt;[，enableHS|disableHS]] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">播放視窗，這是從第一次播放起可檢視內容的分鐘數。 </p> <p>若未指定，或 <span class="codeph"> -w </span> 使用，不指定分鐘數，沒有播放視窗限制。 值必須為非負數。 </p> <p>選填 <span class="codeph"> enableHS </span> 或 <span class="codeph"> disableHS </span> 標幟代表要啟用或停用硬停止。 此旗標會指出解密內容在播放視窗結束時是否被銷毀（啟用），或是否被銷毀（停用）。 </p> <p>例如，若要指定內容僅能檢視60分鐘並需要硬式停止，請執行下列動作： 
     <codeblock>
       -w&amp;nbsp；60，enableHS 
     </codeblock> </p> <p>注意：  <i>硬式停止</i> Flash Player、Android和iOS目前不支援。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l分鐘 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權快取持續時間是指伺服器簽發授權後，使用者端的「授權存放區」中可快取授權的時間（以分鐘為單位）。 值必須為非負數。 </p> <p>您可以指定 <span class="codeph"> -l 0 </span> 表示不允許授權快取。 對於無限制的授權快取，請指定 <span class="codeph"> -l </span> 沒有任何分鐘數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -ldate日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權快取結束日期。 </p> <p class="- topic/p ">這表示在Primetime DRM伺服器核發授權後，使用者端可在使用者端的「授權存放區」中快取授權的最終日期。 </p> <p>您可以下列格式指定日期： 
     <ul id="ul_112DE7248A9C48B19520A3AA9E5D1F03"> 
      <li id="li_01C5400E78B84A3B8955972FBA875AAC"> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> </li> 
      <li id="li_AA13B1EFA07A4542A3DB41FA3320B143"> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span> </li> 
     </ul>例如， <span class="codeph"> 2008-12-1 </span> 或 <span class="codeph"> 2008-12-1-00:00:00 </span> 2008年12月1日午夜。 您需要套用 <span class="codeph"> -l </span> 而不指定無限制授權快取的任何分鐘。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">驗證名稱空間。 </p> <p class="- topic/p ">如果套用此選項，使用者端必須輸入由指定授權單位所發出的使用者名稱和密碼。 </p> <p>您無法將此選項與 <span class="codeph"> -x </span>. </p> <p>更新不允許使用此選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許匿名存取。 </p> <p class="- topic/p ">您無法將此選項與 <span class="codeph"> -authNS </span>. </p> <p class="- topic/p ">更新不允許使用此選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId </span>[： <span class="+ topic/ph pr-d/codeph codeph"> appId </span>[：[ <span class="+ topic/ph pr-d/codeph codeph"> 分鐘 </span>]：[ <span class="+ topic/ph pr-d/codeph codeph"> max </span>]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可播放受保護內容的AIR應用程式允許清單。 </p> <p class="- topic/p ">您可以套用此選項，限制哪些發行者、應用程式和版本可以存取受此DRM原則保護的內容。 </p> <p class="- topic/p ">如果您不指定 <i class="+ topic/ph hi-d/i ">appId</i>，發佈者的所有應用程式 <i class="+ topic/ph hi-d/i ">pubId</i> 允許。 </p> <p>注意：  <i class="+ topic/ph hi-d/i ">分鐘</i> 和 <i class="+ topic/ph hi-d/i ">max</i> 版本編號為選用。 </p> <p class="- topic/p ">您可以指定多個 <span class="codeph"> -air </span> 允許多個應用程式的選項。 如果您未指定AIR或SWF應用程式，則所有應用程式都可以存取此內容。 在更新期間，若要移除或刪除清單中的所有專案，請套用 <span class="codeph"> -air </span> 不含其餘引數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drm黑名單名稱 </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 配對 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">限制存取受保護內容的DRM使用者端。 </p> <p class="- topic/p ">值支援以下列格式的、以逗號分隔的名稱：值配對： </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> 作業系統 |版本= stringValue </span> </p> <p class="- topic/p ">例如， <span class="codeph"> os=Win，release=2.0.1 </span>. 在更新期間，若要從清單中移除所有專案，請套用 <span class="codeph"> -drm黑名單 </span> 不含其餘引數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指出DRM使用者端必須擁有指定的最低安全性層級，才能存取受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog無保護 | USE_IF_AVAILABLE |必填 |無播放(_P) |必要ACP(_A) | REQUIRED_CGMSA | USE_IF_AVAILABLE_ACP | USE_IF_AVAILABLE_CGMSA </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">類比輸出保護限制 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECT | USE_IF_AVAILABLE |必填 |無播放(_P) </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">數位輸出保護限制 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist名稱 </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 配對 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">無法存取受保護內容的應用程式執行階段。 </p> <p class="- topic/p ">值支援以下列格式的、以逗號分隔的名稱：值配對： </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> 作業系統 |應用程式 |版本= stringValue </span> </p> <p class="- topic/p ">例如， <span class="codeph"> os=Win，release=2.0.1，application=AIR </span>. 在更新期間，若要從清單中移除所有專案，請套用 <span class="codeph"> -runtimeBlacklist </span> 不含其餘引數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指出應用程式執行階段必須具有指定的最低安全性層級，才能存取受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf檔案= swf檔案 </span>， <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許播放受保護內容的SWF應用程式允許清單。 </p> <p class="- topic/p ">您可以指定多個 <span class="codeph"> -swf </span> 允許多個應用程式的選項。 如果您未指定任何AIR或SWF應用程式，則所有應用程式都可以存取此內容。 </p> <p>在更新期間，若要從清單中移除所有專案，請套用 <span class="codeph"> -swf </span> 不含其餘引數。 如果您想要透過雜湊值來識別SWF，您需要指定計算雜湊的SWF檔案，以及允許SWF驗證完成的最長時間（以秒為單位）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name= value </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要新增至DRM原則的自訂金鑰/值。 </p> <p class="- topic/p ">您可以指定多個 <span class="codeph"> -k </span> 選項。 在更新期間，您可以套用 <span class="codeph"> -k </span> 如果要移除所有屬性，請不含其餘引數。 資料的解釋或處理由Primetime DRM授權伺服器管理。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p name= value </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">新增自訂屬性，顯示在為每個使用者端產生的授權中。 </p> <p class="- topic/p ">您可以指定多個 <span class="codeph"> -p </span> 用於新增多個屬性的選項。 在更新期間，您需要套用 <span class="codeph"> -p </span> 如果要移除所有屬性，請不含其餘引數。 此資料的解譯或處理是由使用者端應用程式的實作來管理。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> <span class="codeph"> -opOTA白名單=&lt;connection types=""&gt; </span> </span> </td> 
   <td colname="2" class="- topic/entry "> 無線傳輸(OTA)輸出保護限制。 此 <span class="codeph"> 白名單 </span> 欄位指定允許清單的連線型別及格式 &lt;connection types=""&gt; 是 <span class="codeph"> [type(，type)*] </span>，其中型別可以是下列任一專案：MIRACAST、AIRPLAY、WIDI、DLNA </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opResolution &lt;filename&gt; </span> </td> 
   <td colname="2" class="- topic/entry "> <p>指定檔案中定義的以解析度為基礎的輸出保護限制。 </p> <p>此檔案的編碼為JSON。 格式化的文法可在以下網址找到： <i>關於以解析度為基礎的輸出保護</i>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**範例**

若要使用您自己的設定屬性檔案，建立允許匿名存取您內容的原則：

```
java -jar libs\AdobePolicyManager.jar new policy_test.pol -x -c my_configuration.properties
```
