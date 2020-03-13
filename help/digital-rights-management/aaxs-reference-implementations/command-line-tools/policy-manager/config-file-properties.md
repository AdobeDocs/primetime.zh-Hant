---
seo-title: 配置檔案屬性
title: 配置檔案屬性
uuid: aec5fee7-4d77-4299-8d85-3e9042b2bbd1
translation-type: tm+mt
source-git-commit: 99d7eea63b18a97d2b99d0bb7aab5cdc50ae5ffc

---


# 配置檔案屬性 {#configuration-file-properties}

配置檔案指定以下屬性。 對於包含的屬性名 `n`稱， `n` 表示從1開始的整數，並遞增屬性的每個實例。

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 屬性／命令行選項 </th> 
   <th colname="2" class="- topic/entry entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -n</span> 策略 <i class="+ topic/ph hi-d/i ">名</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 人類可讀的策略名稱。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requireKeyServer</span> <p class="- topic/p "><span class="codeph"> -keyServer</span> 布 <i class="+ topic/ph hi-d/i ">爾</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 如果為true，則需要HTTPS金鑰伺服器才能將金鑰傳送至iOS。 若未指定，預設為false。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.enforceJailbreak</span> <p class="- topic/p "><span class="codeph"> -enforceJailbreak</span> 布爾 <i class="+ topic/ph hi-d/i ">型</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 若為true，則對於支援越獄偵測的裝置，若偵測到越獄，則不允許播放。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> -critical</span> 布 <i class="+ topic/ph hi-d/i ">爾</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 設定策略關鍵性。 如果為true，則伺服器必須瞭解策略的所有部分（這是預設行為）。 如果為false，伺服器可能會忽略它不瞭解的策略屬性。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.ansymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">許可證伺服器證書，其公鑰用於加密「增強的許可連結」的根加密密鑰。 <a href="../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md" format="dita" scope="local"></a>此屬性指定一個僅包含證書的檔案（可接受PEM或DER格式）。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -rootKey</span> <i class="+ topic/ph hi-d/i ">root-key</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 指定「增強授權鏈結」的根加密金鑰。 如果未指定任何金鑰，並啟用「增強授權鏈結」，則會產生隨機金鑰。 索引鍵長度必須為16個位元組，並指定為十六進位值。 十六進位值之間的空格是可選的。 對於更新，不允許使用命令行選項，並忽略該屬性。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -domainURL</span> <i class="+ topic/ph hi-d/i ">url</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 網域伺服器的URL（如果需要網域註冊）。 對於更新，不允許使用命令行選項，並忽略該屬性。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry "> 指定是否允許匿名域註冊。 將屬性設為true或包含此命令行選項以允許匿名訪問。 此選項不能與-domainAuthNS一起使用。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS命名空</span><i class="+ topic/ph hi-d/i ">間</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 網域註冊的驗證命名空間。 如果指定，則客戶端應使用由指定授權機構發出的用戶名和密碼進行身份驗證。 對於更新，不允許使用命令行選項，並忽略該屬性。 此選項不能與-domainAnon一起使用。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analog</span> <p class="- topic/p "><span class="codeph"> -opAnalog</span> <i class="+ topic/ph hi-d/i ">AnalogOption</i> </p> </td> 
   <td colname="2" class="- topic/entry ">模擬輸出保護限制。 支援下列值： 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_5BC8F39B61894E83A7B27570FF848F09"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> 無保護</span> </p> </li> 
     <li class="- topic/li " id="li_FF14594A0714480496793A82C3FA1610"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </p> </li> 
     <li class="- topic/li " id="li_721FCC4DC1F34AE398EFAE4C0D3F50F5"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_D588BB278BEE4CEAB034BD48550EBCDC"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_7E5F006D2F114502BA6D0A9C4173004E"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> 必要</span> </p> </li> 
     <li class="- topic/li " id="li_9EBFAA4AACF249C2A94432D88E12C3B9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> 必需_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_6720C6A085864BEB957C0BF2C38551C9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_6FD98473ECDB4A66AC4B506FB9B3B360"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -drmBlacklist</span> <i class="+ topic/ph hi-d/i ">name/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry ">DRM用戶端無法存取受保護的內容。 此選項指定不能使用的DRM模組版本清單（黑名單）。 該值由逗號分隔的名稱=值對組成，其格式如下： <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|vendor|env|screen|value</span> </p> <p class="- topic/p ">其他名稱／值配對必須以逗號分隔。 例如： <span class="codeph"> os=Win,release=2.0,arch=32</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -runtimeBlacklsit</span> <i class="+ topic/ph hi-d/i ">name/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry ">應用程式執行時期無法存取受保護的內容。 此選項指定不能使用的運行時模組版本清單（黑名單）。 該值由逗號分隔的名稱=值對組成，其格式如下： <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|application|arch|model|vendor|env|screen|value</span> </p> <p class="- topic/p ">其他名稱／值配對必須以逗號分隔。 例如， <span class="codeph"> os=Win,application=AIR</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">name/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定存取受保護內容所需的裝置功能。 該值由逗號分隔的名稱=值對組成，其格式如下： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">例如， <span class="codeph"> nonUserAccessibleBus=false,hardwareRootOfTrust=true</span>。 在更新期間，請 <span class="codeph"> 使用-devCapabilitiesV1</span> ，而不使用其餘引數來移除裝置功能限制。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -sync</span> <i class="+ topic/ph hi-d/i ">name/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定客戶端向伺服器發送同步消息的頻率。 如果未設定，客戶端在播放使用此策略保護的內容時將不會發送同步消息。 值由逗號分隔的 <span class="codeph"> name=value</span> 對組成，格式如下： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force|hardStop=numberValue</span> </p> <p class="- topic/p "> 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_25CAF96C27F34848A95B2E3693847C71"><span class="codeph"> start</span> （必需）-啟動間隔指定自上次同步以來多分鐘的客戶端應開始與伺服器同步。 </li> 
      <li id="li_CC9068CFE75645029C947C9E1B53351F"><span class="codeph"> force</span> （可選）-強制同步概率是客戶端在播放期間應強制同步消息的概率(0-100)。 </li> 
      <li id="li_C31A6250F19348FBB8B7569D00C6314E"><span class="codeph"> hardStop</span> （可選）-硬停止間隔是在幾分鐘內的時間，在此時間之後，如果無法同步，客戶端將無法播放。 如果設定，則必須大於啟動間隔。 </li> 
     </ul>在更新期間， <span class="codeph"> 使用</span> -sync（不含其餘參數）來刪除同步要求。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">指出此政策是否具有根授權(請參閱使 <i class="+ topic/ph hi-d/i ">用Adobe Access</i> <i class="+ topic/ph hi-d/i ">for Protecting Content</i>)。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">內容有效的日期。 使用 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> (例如， <span class="codeph"> 2009-01-31</span> 代表1月31日12:00 AM)或 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span><span class="codeph"></span> （例如， 2009-01-31-14:3）0:00代表1月31日下午2:30)。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">內容有效的日期。 不 <span class="codeph"> 能同時指定policy.expiration.endDate</span> 和policy.expiration.duration。 使用 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> 或 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span> （例如，2009-01-31-14:30:00代表1月31日下午2:30）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">內容的有效時間（以分鐘為單位），從封裝時開始。 不 <span class="codeph"> 能同時指定policy.expiration.endDate</span><span class="codeph"> 和policy.expiration.duration</span> 。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在用戶端上快取授權的時間長度（以分鐘為單位）。 將此屬性設為0可禁止授權快取。 值必須為0或更高。 policy. <span class="codeph"> licenseCaching.duration</span><span class="codeph"> 和policy.licenseCaching.endDate</span> 不能同時使用。 </p> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">注意</b>:此策略設定僅應用於磁碟上的許可證快取。 它無法控制記憶體快取的授權持續時間。 即使策略指定的持續時間為零，也可以在記憶體上快取許可證。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不得快取授權的日期。 policy. <span class="codeph"> licenseCaching.duration</span><span class="codeph"> 和policy.licenseCaching.endDate</span> 不能同時使用。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonymous</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指出是否允許匿名取得授權。 如果未指定，則預設為「false」（需要使用者名稱／密碼驗證）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果需要用戶名／密碼驗證，則此屬性指定用戶名的可選名稱限定符。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">伺服器在取得授權期間使用的自訂名稱／值配對。 使用下列格式指定屬性： <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定播放視窗（以分鐘為單位），此時段是授權在首次用於播放受保護內容後的有效期間。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">輸出保護限制。 值必須是下列其中一項： </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">NO_PROTECTION, USE_IF_AVAILABLE, REQUIRED, NO_PLAYBACK</i> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM模組必須具有指定的最低安全級別或更高級別，才能訪問受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">應用程式執行時期模組必須具備指定的最低安全等級或更高等級，才能存取受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許播放受保護內容的Adobe AIR或iOS應用程式白名單。 屬性必須使用下列格式： <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min</span>]:[<span class="+ topic/ph pr-d/codeph codeph"></span>max]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許播放受保護內容的SWF應用程式白名單。 使用下列格式： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">URL</span> =<span class="+ topic/ph pr-d/codeph codeph">swf</span>,time=max_time_to_verify<i class="+ topic/ph hi-d/i ">swf_file</i><i class="+ topic/ph hi-d/i "></i><i class="+ topic/ph hi-d/i "></i> ，是SWF檔案，它計算散列和max_time_to驗證SWF的最大時間是允許下載和驗證SWF以（以秒為單位）完成的最大時間。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">要包含在授予使用者之授權中的自訂名稱／值配對。 使用下列格式： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> <p class="- topic/p ">此選項可針對多個自訂屬性多次定義。 </p> </td> 
  </tr> 
 </tbody> 
</table>

