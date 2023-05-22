---
title: 配置檔案屬性
description: 配置檔案屬性
copied-description: true
exl-id: 6405126d-4cf2-4ffc-821d-fbfdc00b60ef
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 0%

---

# 配置檔案屬性 {#configuration-file-properties}

配置檔案指定以下屬性。 對於包含的屬性名 `n`。 `n` 表示以1開頭的整數，並且為屬性的每個實例遞增。

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 屬性/命令行選項 </th> 
   <th colname="2" class="- topic/entry entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -n</span> <i class="+ topic/ph hi-d/i ">策略名</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 可讀的策略名稱。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requireKeyServer</span> <p class="- topic/p "><span class="codeph"> -keyServer</span> <i class="+ topic/ph hi-d/i ">布爾</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 如果為true，則需要HTTPS密鑰伺服器才能將密鑰傳遞到iOS。 如果未指定，則預設值為false。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.enforceJailbreak</span> <p class="- topic/p "><span class="codeph"> -enforceJailbreak</span> <i class="+ topic/ph hi-d/i ">布爾</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 如果為true，則對於支援越獄檢測的設備，如果檢測到越獄，則不允許播放。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> 策略。關鍵</span> <p class="- topic/p "><span class="codeph"> 關鍵</span> <i class="+ topic/ph hi-d/i ">布爾</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 設定策略關鍵程度。 如果為true，則伺服器必須瞭解策略的所有部分（這是預設行為）。 如果為false，則伺服器可能會忽略它不理解的策略屬性。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.asymmetric.cerfile</span> </td> 
   <td colname="2" class="- topic/entry ">其公鑰用於加密的根加密密鑰的許可證伺服器證書 <a href="../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md" format="dita" scope="local"> 增強的許可證連結 </a>
   此屬性指定僅包含證書的檔案（PEM或DER格式可接受）。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -rootKey</span> <i class="+ topic/ph hi-d/i ">根密鑰</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 為增強的許可證連結指定根加密密鑰。 如果未指定密鑰，並且啟用了增強的許可證連結，則將生成隨機密鑰。 密鑰的長度必須為16個位元組，並指定為十六進位值。 十六進位值之間的空格是可選的。 對於更新，不允許使用命令行選項，並忽略屬性。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph">  — 域URL</span> <i class="+ topic/ph hi-d/i ">url</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 域伺服器的URL（如果需要域註冊）。 對於更新，不允許使用命令行選項，並忽略屬性。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph">  — 域匿名</span> </p> </td> 
   <td colname="2" class="- topic/entry "> 指定是否允許匿名域註冊。 將屬性設定為true或包括此命令行選項以允許匿名訪問。 此選項不能與 — domainAuthNS一起使用。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS</span> <i class="+ topic/ph hi-d/i ">命名空間</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 域註冊的驗證命名空間。 如果指定，客戶端應使用指定機構頒發的用戶名和密碼進行身份驗證。 對於更新，不允許使用命令行選項，並忽略屬性。 此選項不能與 — domainAnon一起使用。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analog</span> <p class="- topic/p "><span class="codeph"> -op模擬</span> <i class="+ topic/ph hi-d/i ">模擬選項</i> </p> </td> 
   <td colname="2" class="- topic/entry ">模擬輸出保護限制。 支援以下值： 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_5BC8F39B61894E83A7B27570FF848F09"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> 無保護</span> </p> </li> 
     <li class="- topic/li " id="li_FF14594A0714480496793A82C3FA1610"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> 使用_IF_AVAILABLE</span> </p> </li> 
     <li class="- topic/li " id="li_721FCC4DC1F34AE398EFAE4C0D3F50F5"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_D588BB278BEE4CEAB034BD48550EBCDC"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_7E5F006D2F114502BA6D0A9C4173004E"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> 必需</span> </p> </li> 
     <li class="- topic/li " id="li_9EBFAA4AACF249C2A94432D88E12C3B9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> 必需_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_6720C6A085864BEB957C0BF2C38551C9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> 必需_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_6FD98473ECDB4A66AC4B506FB9B3B360"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> 無回放(_P)</span> </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlickst.n</span> <p class="- topic/p "><span class="codeph"> -drm黑名單</span> <i class="+ topic/ph hi-d/i ">名稱/值對</i> </p> </td> 
   <td colname="2" class="- topic/entry ">DRM客戶端被限制訪問受保護的內容。 此選項指定可能不使用的DRM模組版本清單（阻止清單）。 值由逗號分隔的name=value對組成，其格式如下： <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|模型|vendor|env|screen|value</span> </p> <p class="- topic/p ">其他名稱/值對必須以逗號分隔。 例如： <span class="codeph"> os=Win,release=2.0,arch=32</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlickst.n</span> <p class="- topic/p "><span class="codeph"> -runtimeBlacklsit</span> <i class="+ topic/ph hi-d/i ">名稱/值對</i> </p> </td> 
   <td colname="2" class="- topic/entry ">應用程式運行時限制訪問受保護的內容。 此選項指定可能未使用的運行時模組版本清單（阻止清單）。 值由逗號分隔的name=value對組成，其格式如下： <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|application|arch|模型|vendor|env|screen|value</span> </p> <p class="- topic/p ">其他名稱/值對必須以逗號分隔。 比如說， <span class="codeph"> os=Win,application=AIR</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">名稱/值對</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定訪問受保護內容所需的設備功能。 值由逗號分隔的name=value對組成，其格式如下： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">比如說， <span class="codeph"> nonUserAccessibleBus=false,hardwareRootOfTrust=true</span>。 在更新期間，使用 <span class="codeph"> -devCapabilitiesV1</span> 刪除設備功能限制。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.sync頻率</span> <p class="- topic/p "><span class="codeph">  — 同步</span> <i class="+ topic/ph hi-d/i ">名稱/值對</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定客戶端向伺服器發送同步消息的頻率。 如果未設定，則客戶端在播放受此策略保護的內容時不會發送同步消息。 值由逗號分隔 <span class="codeph"> 名稱=值</span> 格式對： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force|hardStop=numberValue</span> </p> <p class="- topic/p "> 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_25CAF96C27F34848A95B2E3693847C71"><span class="codeph"> 開始</span> （必需） — 啟動間隔指定客戶端應自上次同步以來開始與伺服器同步這麼長時間。 </li> 
      <li id="li_CC9068CFE75645029C947C9E1B53351F"><span class="codeph"> 力</span> （可選） — 強制同步概率是客戶端在回放期間強制同步消息的概率(0-100)。 </li> 
      <li id="li_C31A6250F19348FBB8B7569D00C6314E"><span class="codeph"> 硬停止</span> （可選） — 硬停止時間間隔是客戶端在無法同步時無法播放的時間（以分鐘為單位）。 如果設定，則必須大於啟動間隔。 </li> 
     </ul>在更新期間，使用 <span class="codeph">  — 同步</span> 刪除同步要求的其餘參數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">指示此策略是否具有根許可證(請參見 <i class="+ topic/ph hi-d/i ">增強的許可證連結</i> 在 <i class="+ topic/ph hi-d/i ">使用Adobe訪問保護內容</i>)。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">內容有效的日期。 使用格式 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> (例如， <span class="codeph"> 2009-01-31</span> 代表1月31日上午12點)或 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span> (例如， <span class="codeph"> 2009-01-31-14:30:00</span> 代表1月31日下午2:30)。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">內容有效之前的日期。 兩者 <span class="codeph"> policy.expiration.endDate</span> 和policy.expiration.duration不能同時指定。 使用格式 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> 或 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span> (例如，2009-01-31-14:30:00表示1月31日下午2:30)。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">內容的有效時間（以分鐘為單位），從打包時開始。 兩者 <span class="codeph"> policy.expiration.endDate</span> 和 <span class="codeph"> policy.expiration.duration</span> 不能同時指定。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">許可證可以快取到客戶端上的時間（以分鐘為單位）。 將此屬性設定為0以禁止許可證快取。 值必須為0或更高。 兩者 <span class="codeph"> policy.licenseCaching.duration</span> 和 <span class="codeph"> policy.licenseCaching.endDate</span> 不能同時使用。 </p> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">注釋</b>:此策略設定僅應用於磁碟上的許可證快取。 它不控制記憶體快取的許可證持續時間。 即使策略指定的持續時間為零，也可以在記憶體上快取許可證。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不能快取許可證的日期。 兩者 <span class="codeph"> policy.licenseCaching.duration</span> 和 <span class="codeph"> policy.licenseCaching.endDate</span> 不能同時使用。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anomy</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示是否允許匿名獲取許可證。 如果未指定，則預設值為"false"（需要用戶名/密碼驗證）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果需要用戶名/密碼驗證，此屬性指定用戶名的可選名稱限定符。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在獲取許可證期間由伺服器使用的自定義名稱/值對。 使用以下格式指定屬性： <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">名稱</span>=<span class="+ topic/ph pr-d/codeph codeph">值</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定播放窗口（以分鐘為單位），該窗口是許可證在首次用於播放受保護內容之後的有效持續時間。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">輸出保護限制。 值必須是以下值之一： </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">NO_PROTECTION、USE_IF_AVAILABLE、REQUIRED、NO_PLAYBACK</i> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM模組必須具有指定的最低安全級別或更高級別才能訪問受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">應用程式運行時模組必須具有指定的最低安全級別或更高級別才能訪問受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許播放受保護內容的Adobe AIR或iOS應用程式的允許清單。 該屬性必須使用以下格式： <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">應用ID</span>[:[<span class="+ topic/ph pr-d/codeph codeph">分鐘</span>]:[<span class="+ topic/ph pr-d/codeph codeph">最大</span>]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許播放受保護內容的SWF應用程式清單。 使用以下格式： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">URL</span> 或檔案=<span class="+ topic/ph pr-d/codeph codeph">swf_file</span>，時間=<i class="+ topic/ph hi-d/i ">max_time_to_verify</i> <i class="+ topic/ph hi-d/i ">swf_file</i> 是SWF檔案，用於計算哈希和 <i class="+ topic/ph hi-d/i ">max_time_to_verify</i> 是允許完成SWF下載和驗證的最長時間（以秒為單位）。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">要包括在發給用戶的許可證中的自定義名稱/值對。 使用以下格式： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">名稱</span>=<span class="+ topic/ph pr-d/codeph codeph">值</span> </p> <p class="- topic/p ">可以多次為多個自定義屬性定義此選項。 </p> </td> 
  </tr> 
 </tbody> 
</table>
