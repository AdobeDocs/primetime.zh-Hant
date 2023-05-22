---
title: 策略管理器命令行用法
description: 策略管理器命令行用法
copied-description: true
exl-id: 888be282-7eaa-4101-b4b1-4f8df99a967a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 0%

---

# 策略管理器命令行用法 {#policy-manager-command-line-usage}

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

**表1:命令**

| 命令 | 說明 |
|---|---|
| `new` | 建立新的DRM策略 |
| `detail` | 描述現有DRM策略 |
| `update` | 更新現有DRM策略 |

**表2:選項**

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置檔案的名稱和位置。 </p> <p class="- topic/p ">如果未指定名稱或位置，DRM策略管理器將搜索 <span class="filepath"> flashaccessols.properties </span> 的子菜單。 </p> <p>注：在命令行上指定的選項優先於在配置檔案中指定的選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目標檔案存在，則無需提示即可覆蓋該檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要詢問是否應覆蓋目標檔案。 如果目標檔案存在，並且 <span class="codeph"> -o </span> 未設定，出現錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph">  — 根 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示DRM策略具有根許可證。 </p> <p class="- topic/p ">此選項不可用於更新。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">許可證生效前的日期。 </p> <p>可以在中指定日期 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span> 的子菜單。 例如，2008-12-1或2008-12-1-00:00:2008年12月1日午夜0點。 </p> <p> 
     <ul id="ul_D5DB5044756D4BD6A734813971598425"> 
      <li id="li_B6BD62A524384060A9DDA14FF50936FA">值必須大於 <span class="codeph"> -s </span> 的下界。 </li> 
      <li id="li_C3C5AD0231A240EC9AC57685B9206E8D">不能將此選項應用於 <span class="codeph"> -r </span>。 </li> 
      <li id="li_3790E2F829A149979BF44E0914CFF431">要在更新DRM策略時刪除結束日期，請應用 <span class="codeph"> -e </span> 不指定日期。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r分鐘 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">受保護內容有效的持續時間（分鐘）。 </p> <p class="- topic/p ">當使用打包器保護內容時，DRM策略將變為有效。 </p> <p> 
     <ul id="ul_4690A0E4677A4DF6A006B7FCBD46F1BE"> 
      <li id="li_D1F098D44B494EE7A8647C0B62D5ACFA">值必須為非負。 </li> 
      <li id="li_ADFDCB01EEE04B37AFA42886AAEF47EB">不能同時應用此選項 <span class="codeph"> -e </span>。 </li> 
      <li id="li_E80563E68BEB43FC9E29A694594CAE01">要在更新DRM策略時刪除或刪除持續時間，請應用 <span class="codeph"> -r </span> 不指定任何分鐘。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">許可證生效的日期。 </p> <p>可以在 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span> 的子菜單。 比如說， <span class="codeph"> 2008-12-1 </span> 或 <span class="codeph"> 2008-12-1-00:00:00 </span> 2008年12月1日午夜。 </p> <p> 
     <ul id="ul_D52B337F547F4E7AB87FE025236CA930"> 
      <li id="li_DBAE380972434DB1A4EF20D399038AB8">值必須小於 <span class="codeph"> -e </span>，也請參見Wiki頁。 </li> 
      <li id="li_2899EC5559CF44319A4AC4ECD90A5B9A">不能同時應用此選項 <span class="codeph"> -r </span>。 </li> 
      <li id="li_19861B1A64E44B95B649948EAB3E4085">要在更新DRM策略時刪除或刪除開始日期，請使用 <span class="codeph"> -s </span> 不指定日期。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w [&lt;minutes&gt;[,enableHS|disableHS]] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">播放窗口，即從第一次播放中可以查看內容的分鐘數。 </p> <p>如果未指定，或 <span class="codeph"> -w </span> 在未指定分鐘數的情況下使用，不存在播放窗口限制。 值必須為非負。 </p> <p>可選 <span class="codeph"> 啟用HS </span> 或 <span class="codeph"> 禁用HS </span> 標籤指示是啟用還是禁用硬停止。 該標誌指示解密上下文在播放窗口的結尾處是否被破壞（啟用）或是否被破壞（禁用）。 </p> <p>例如，要指定內容只能查看60分鐘，並且需要硬停止： 
     <codeblock>
       -nbsp;60,enableHS(&amp;N) 
     </codeblock> </p> <p>注：  <i>硬停</i> 當前在Flash Player、Android和iOS不支援。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l分鐘 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">許可證快取持續時間是在伺服器發出許可證後，許可證可以快取到客戶端許可證儲存中的時間（以分鐘為單位）。 值必須為非負。 </p> <p>可以指定 <span class="codeph"> -l 0 </span> 以指示不允許進行許可證快取。 對於無限制的許可證快取，請指定 <span class="codeph"> -l </span> 沒幾分鐘。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -ldate日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">許可證快取結束日期。 </p> <p class="- topic/p ">這表示在Mogfire DRM伺服器頒發許可證後，客戶端可以快取客戶端許可證儲存中的許可證的最終日期。 </p> <p>可以以下列格式指定日期： 
     <ul id="ul_112DE7248A9C48B19520A3AA9E5D1F03"> 
      <li id="li_01C5400E78B84A3B8955972FBA875AAC"> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> </li> 
      <li id="li_AA13B1EFA07A4542A3DB41FA3320B143"> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span> </li> 
     </ul>比如說， <span class="codeph"> 2008-12-1 </span> 或 <span class="codeph"> 2008-12-1-00:00:00 </span> 2008年12月1日午夜。 你需要申請 <span class="codeph"> -l </span> 不為無限制的許可證快取指定任何分鐘。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">身份驗證命名空間。 </p> <p class="- topic/p ">如果應用此選項，則客戶端需要輸入由指定機構頒發的用戶名和密碼。 </p> <p>不能同時應用此選項 <span class="codeph"> -x </span>。 </p> <p>不允許對更新使用此選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許匿名訪問。 </p> <p class="- topic/p ">不能同時應用此選項 <span class="codeph"> -authNS </span>。 </p> <p class="- topic/p ">不允許對更新使用此選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId </span>[: <span class="+ topic/ph pr-d/codeph codeph"> 應用ID </span>[:[ <span class="+ topic/ph pr-d/codeph codeph"> 分鐘 </span>]:[ <span class="+ topic/ph pr-d/codeph codeph"> 最大 </span>]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可播放受保護內容的AIR應用程式的允許清單。 </p> <p class="- topic/p ">您可以應用此選項來限制哪些發佈者、應用程式和版本可以訪問使用此DRM策略保護的內容。 </p> <p class="- topic/p ">如果未指定 <i class="+ topic/ph hi-d/i ">應用ID</i>，發佈伺服器的所有應用程式 <i class="+ topic/ph hi-d/i ">pubId</i> 的子菜單。 </p> <p>注：  <i class="+ topic/ph hi-d/i ">分鐘</i> 和 <i class="+ topic/ph hi-d/i ">最大</i> 版本號是可選的。 </p> <p class="- topic/p ">可以指定多個 <span class="codeph"> 空氣 </span> 選項以允許多個應用程式。 如果未指定AIR或SWF應用程式，則所有應用程式都可以訪問此內容。 在更新期間，要從清單中刪除或刪除所有條目，請應用 <span class="codeph"> 空氣 </span> 而沒有其餘的論據。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drm黑名單名稱 </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 配對 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">限制訪問受保護內容的DRM客戶端。 </p> <p class="- topic/p ">值支援以下格式的逗號分隔名稱：值對： </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> 作業系統 | release= stringValue </span> </p> <p class="- topic/p ">比如說， <span class="codeph"> os=Win,release=2.0.1 </span>。 在更新期間，要從清單中刪除所有條目，請應用 <span class="codeph"> -drm黑名單 </span> 沒有其餘的參數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示DRM客戶端必須具有指定的最低安全級別才能訪問受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -op模擬NO_PROTECTION | USE_IF_AVAILABLE |必需 |無播放(_P) |必需_ACP |必需的_CGMSA | USE_IF_AVAILABLE_ACP | USE_IF_AVAILABLE_CGMSA </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">模擬輸出保護限制 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -op數字NO_PROTECTION | USE_IF_AVAILABLE |必需 |無播放(_P) </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">數字輸出保護限制 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlickst名稱 </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 配對 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">限制訪問受保護內容的應用程式運行時。 </p> <p class="- topic/p ">值支援以下格式的逗號分隔名稱：值對： </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> 作業系統 |應用程式 | release= stringValue </span> </p> <p class="- topic/p ">比如說， <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>。 在更新期間，要從清單中刪除所有條目，請應用 <span class="codeph"> -runtime黑名單 </span> 而沒有其餘的論據。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示應用程式運行時必須具有指定的最低安全級別才能訪問受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swfurl </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf檔案=swf檔案 </span>。 <span class="+ topic/ph pr-d/codeph codeph"> 時間=最大時間到檢驗 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許播放受保護內容的SWF應用程式清單。 </p> <p class="- topic/p ">可以指定多個 <span class="codeph"> -swf </span> 選項以允許多個應用程式。 如果未指定任何AIR或SWF應用程式，則所有應用程式都可以訪問此內容。 </p> <p>在更新期間，要從清單中刪除所有條目，請應用 <span class="codeph"> -swf </span> 而沒有其餘的論據。 如果要通過SWF的散列值來標識SWF，則需要指定要計算其散列的SWF檔案以及允許完成驗證的最長時間（以秒為單位）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k名稱=值 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要添加到DRM策略的自定義密鑰/值。 </p> <p class="- topic/p ">可以指定多個 <span class="codeph"> -k </span> 頁籤 在更新期間，您可以應用 <span class="codeph"> -k </span> 刪除所有屬性時，不使用其餘參數。 資料的解釋或處理由黃金時段DRM許可伺服器管理。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p名稱=值 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">添加在為每個客戶端生成的許可證中顯示的自定義屬性。 </p> <p class="- topic/p ">可以指定多個 <span class="codeph"> -p </span> 選項以添加多個屬性。 在更新期間，您需要應用 <span class="codeph"> -p </span> 刪除所有屬性時，不使用其餘參數。 該資料的解釋或處理通過客戶端應用程式的實施來管理。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> <span class="codeph"> -opOTA白名單=&lt;connection types=""&gt; </span> </span> </td> 
   <td colname="2" class="- topic/entry "> 空中(OTA)輸出保護限制。 的 <span class="codeph"> 白名單 </span> 欄位指定允許清單的連接類型和 &lt;connection types=""&gt; 是 <span class="codeph"> [type(,type)*] </span>，其中類型可以是下列任一值：MIRACAST, AIRPLAY, WIDI, DLNA </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -op解析度 &lt;filename&gt; </span> </td> 
   <td colname="2" class="- topic/entry "> <p>在指定檔案中定義的基於解析度的輸出保護約束。 </p> <p>此檔案的編碼為JSON。 格式的語法可在 <i>關於基於解析度的輸出保護</i>。 </p> </td> 
  </tr> 
 </tbody> 
</table>

**示例**

使用您自己的配置屬性檔案建立允許匿名訪問內容的策略：

```
java -jar libs\AdobePolicyManager.jar new policy_test.pol -x -c my_configuration.properties
```
