---
title: 命令行用法
description: 命令行用法
copied-description: true
exl-id: 2142cb76-e71c-4443-8b5d-348e45587331
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 0%

---

# 命令行用法 {#command-line-usage}

使用策略管理器之前，請確保滿足「要求」中列出的要求。

策略管理器位於 [!DNL \Reference Implementation\Command Line Tools] 的下界。 要運行該工具，請使用以下語法：

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

下表包含上述語法中所示的命令行操作的說明：

| 命令行操作 | 說明 |
|---|---|
| `new` | 建立新策略。 |
| `detail` | 描述現有策略。 |
| `update` | 更新現有策略。 |

下表介紹了可以連同上述語法一起指定的命令行選項：

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置檔案的位置。 如果未使用此選項，策略管理器將查找 <span class="filepath"> flashaccessols.properties </span> 的子菜單。 在命令行上指定的選項優先於配置檔案中存在的選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目標檔案已存在，則覆蓋它而不出現提示。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要詢問是否應覆蓋目標檔案。 如果目標檔案已存在，並且 <span class="codeph"> -o </span> 未設定，將返回錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph">  — 根 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示策略具有根許可證。 不允許進行更新。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">許可證生效的日期。 指定為 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span>。 例如，2008-12-1或2008-12-1-00:00:2008年12月1日午夜0點。 值必須大於 <span class="codeph"> -s </span>，也請參見Wiki頁。 此選項不能與 <span class="codeph"> -r </span>。 要在更新策略時刪除結束日期，請使用 <span class="codeph"> -e </span> 不指定日期。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r分鐘 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">使用此策略保護的內容的有效持續時間（分鐘），從使用打包程式保護內容時開始。 值必須為非負。 此選項不能與 <span class="codeph"> -e </span>。 要在更新策略時刪除持續時間，請使用 <span class="codeph"> -r </span> 而不指定分鐘數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">許可證有效的日期。 指定為 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span>。 例如，2008-12-1或2008-12-1-00:00:2008年12月1日午夜0點。 值必須小於 <span class="codeph"> -e </span>，也請參見Wiki頁。 此選項不能與 <span class="codeph"> -r </span>。 要在更新策略時刪除開始日期，請使用 <span class="codeph"> -s </span> 不指定日期。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w分鐘 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">播放窗口（從第一次播放開始，可以查看內容的分鐘數）。 如果未指定此選項，或 <span class="codeph"> -w </span> 在未指定分鐘數的情況下使用，沒有播放窗口限制。 值必須為非負。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l分鐘 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">許可證快取持續時間（分鐘），即在伺服器頒發許可證後允許許可證在客戶端許可證儲存中快取的時間。 值必須為非負。 指定 <span class="codeph"> -l 0 </span> 表示不允許使用許可證快取。 使用 <span class="codeph"> -l </span> 不指定無限制許可證快取的分鐘數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -ldate日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">許可證快取結束日期（在伺服器頒發許可證後，許可證不能快取到客戶端許可證儲存中的日期）。 指定為 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span><i class="+ topic/ph hi-d/i "> </i>或<i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span>。 例如，2008-12-1或2008-12-1-00:00:2008年12月1日午夜0點。 使用 <span class="codeph"> -l </span> 不指定無限制許可證快取的分鐘數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">身份驗證命名空間。 如果指定，客戶端應使用指定機構頒發的用戶名和密碼進行身份驗證。 此選項不能與 <span class="codeph"> -x </span>。 不允許進行更新。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許匿名訪問。 此選項不能與 <span class="codeph"> -authNS </span>。 不允許進行更新。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId </span>[: <span class="+ topic/ph pr-d/codeph codeph"> 應用ID </span>[:[ <span class="+ topic/ph pr-d/codeph codeph"> 分鐘 </span>]:[ <span class="+ topic/ph pr-d/codeph codeph"> 最大 </span>]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許播放受保護內容的AIR應用程式清單。 使用此策略可限制哪些發佈者、應用程式和版本可以訪問受此策略保護的內容。 </p> <p class="- topic/p ">如果 <i class="+ topic/ph hi-d/i ">應用ID</i> 未指定，發佈伺服器的所有應用程式 <i class="+ topic/ph hi-d/i ">pubId</i> 的子菜單。 </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">分鐘</i> 和 <i class="+ topic/ph hi-d/i ">最大</i> 版本號是可選的。 </p> <p class="- topic/p ">多重 <span class="codeph"> 空氣 </span> 可以指定選項以允許多個應用程式。 如果未指定AIR或SWF應用程式，則所有應用程式都可以訪問此內容。 在更新期間，使用 — air（不含剩餘參數）從清單中刪除所有條目。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drm黑名單名稱 </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 配對 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM客戶端被限制訪問受保護的內容。 值由逗號分隔的名稱：值對組成，格式如下： </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> 作業系統 | release= stringValue </span> </p> <p class="- topic/p ">比如說， <span class="codeph"> os=Win,release=2.0.1 </span>。 在更新期間，使用 <span class="codeph"> -drm黑名單 </span> 刪除清單中的所有條目。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示DRM客戶端必須具有指定的最低安全級別才能訪問受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -op模擬NO_PROTECTION | USE_IF_AVAILABLE |必需 |無播放(_P) | ACP_REQUIRED | CGMS-A_REQUIRED | USE_ACP_IF_AVAILABLE | USE_CGMS-A_IF_AVAILABLE </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">模擬輸出保護限制。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -op數字NO_PROTECTION | USE_IF_AVAILABLE |必需 |無播放(_P) </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">數字輸出保護限制。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlickst名稱 </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 配對 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">應用程式運行時限制訪問受保護的內容。 值由逗號分隔的名稱：值對組成，格式如下： </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> 作業系統 |應用程式 | release= stringValue </span> </p> <p class="- topic/p ">比如說， <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>。 在更新期間，使用 <span class="codeph"> -runtime黑名單 </span> 刪除清單中的所有條目。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示應用程式運行時必須具有指定的最低安全級別才能訪問受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swfurl </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf檔案=swf檔案 </span>。 <span class="+ topic/ph pr-d/codeph codeph"> 時間=最大時間到檢驗 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許播放受保護內容的SWF應用程式清單。 可以指定多個 — swf選項以允許多個應用程式。 如果未指定AIR或SWF應用程式，則所有應用程式都可以訪問此內容。 在更新過程中，使用 — swf（不包含其餘參數）從清單中刪除所有條目。 要通過SWF的哈希值來標識SWF，請指定要計算其哈希的SWF檔案以及允許完成驗證的最長時間（以秒為單位）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k名稱=值 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要添加到策略的自定義鍵/值。 多重 <span class="codeph"> -k </span> 可以指定選項。 在更新期間，使用 <span class="codeph"> -k </span> 刪除所有屬性的其餘參數。 對此資料的解釋或處理完全取決於Adobe訪問許可證伺服器的實施。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p名稱=值 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">添加一個自定義屬性，該屬性將出現在為每個客戶端生成的許可證中。 多重 <span class="codeph"> -p </span> 可以指定選項以添加多個屬性。 在更新期間，使用 <span class="codeph"> -p </span> 刪除所有屬性的其餘參數。 對這些資料的解釋或處理完全取決於客戶端應用程式的實現。 </p> </td> 
  </tr> 
 </tbody> 
</table>
