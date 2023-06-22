---
title: 組態檔屬性
description: 組態檔屬性
copied-description: true
exl-id: 6405126d-4cf2-4ffc-821d-fbfdc00b60ef
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 0%

---

# 組態檔屬性 {#configuration-file-properties}

組態檔指定下列屬性。 屬性名稱包含 `n`， `n` 代表屬性的每個例項都從1開始並遞增的整數。

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 屬性/命令列選項 </th> 
   <th colname="2" class="- topic/entry entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -n</span> <i class="+ topic/ph hi-d/i ">policyname</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 人類可讀的原則名稱。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requireKeyServer</span> <p class="- topic/p "><span class="codeph"> -keyServer</span> <i class="+ topic/ph hi-d/i ">布林值</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 如果為true，則需要HTTPS金鑰伺服器，才能將金鑰傳遞至iOS。 若未指定，預設值為false。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.enforceJailbreak</span> <p class="- topic/p "><span class="codeph"> -enforceJailbreak</span> <i class="+ topic/ph hi-d/i ">布林值</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 如果為true，對於支援越獄偵測的裝置，在偵測到越獄時不允許播放。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> -critical</span> <i class="+ topic/ph hi-d/i ">布林值</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 設定原則重要性。 如果為true，則伺服器必須瞭解原則的所有部分（這是預設行為）。 如果為false，則伺服器可能會忽略它不瞭解的原則屬性。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">授權伺服器憑證，其公開金鑰用於加密的根加密金鑰 <a href="../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md" format="dita" scope="local"> 增強授權鏈結 </a>
   此屬性指定僅包含憑證的檔案（可以接受PEM或DER格式）。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -rootKey</span> <i class="+ topic/ph hi-d/i ">root-key</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 指定增強型授權鏈結的根加密金鑰。 若未指定金鑰，且已啟用增強授權鏈結，則會產生隨機金鑰。 金鑰的長度必須是16個位元組，並指定為十六進位值。 十六進位值之間的空白字元為選用。 更新時，不允許使用命令列選項，並忽略屬性。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -domainUrl</span> <i class="+ topic/ph hi-d/i ">url</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 網域伺服器的URL （如果需要網域註冊）。 更新時，不允許使用命令列選項，並忽略屬性。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry "> 指定是否允許匿名網域註冊。 將屬性設定為true或包含此命令列選項以允許匿名存取。 此選項無法搭配 — domainAuthNS使用。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS</span> <i class="+ topic/ph hi-d/i ">名稱空間</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 網域註冊的驗證名稱空間。 若指定，使用者端應使用指定授權單位所簽發的使用者名稱和密碼進行驗證。 更新時，不允許使用命令列選項，並忽略屬性。 此選項無法與 — domainAnon搭配使用。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analog</span> <p class="- topic/p "><span class="codeph"> -opAnalog</span> <i class="+ topic/ph hi-d/i ">類比選項</i> </p> </td> 
   <td colname="2" class="- topic/entry ">類比輸出保護限制。 支援下列值： 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_5BC8F39B61894E83A7B27570FF848F09"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> 無保護(_P)</span> </p> </li> 
     <li class="- topic/li " id="li_FF14594A0714480496793A82C3FA1610"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </p> </li> 
     <li class="- topic/li " id="li_721FCC4DC1F34AE398EFAE4C0D3F50F5"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_D588BB278BEE4CEAB034BD48550EBCDC"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_7E5F006D2F114502BA6D0A9C4173004E"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> 必填</span> </p> </li> 
     <li class="- topic/li " id="li_9EBFAA4AACF249C2A94432D88E12C3B9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_6720C6A085864BEB957C0BF2C38551C9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_6FD98473ECDB4A66AC4B506FB9B3B360"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -drm黑名單</span> <i class="+ topic/ph hi-d/i ">名稱/值組</i> </p> </td> 
   <td colname="2" class="- topic/entry ">DRM使用者端無法存取受保護的內容。 此選項會指定不可使用的DRM模組版本清單（區塊清單）。 值包含逗號分隔的名稱=值配對，格式如下： <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">其他名稱/值組必須以逗號分隔。 例如： <span class="codeph"> os=Win，release=2.0，arch=32</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -runtimeBlacklist</span> <i class="+ topic/ph hi-d/i ">名稱/值組</i> </p> </td> 
   <td colname="2" class="- topic/entry ">應用程式執行階段無法存取受保護的內容。 此選項會指定不可使用的執行階段模組版本清單（封鎖清單）。 值包含逗號分隔的名稱=值配對，格式如下： <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|版本|application|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">其他名稱/值組必須以逗號分隔。 例如， <span class="codeph"> os=Win，application=AIR</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">名稱/值組</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定存取受保護內容所需的裝置功能。 值包含逗號分隔的名稱=值配對，格式如下： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">例如， <span class="codeph"> nonUserAccessibleBus=false，hardwareRootOfTrust=true</span>. 在更新期間，使用 <span class="codeph"> -devCapabilitiesV1</span> 移除裝置功能限制的剩餘引數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -sync</span> <i class="+ topic/ph hi-d/i ">名稱/值組</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定使用者端傳送同步化訊息至伺服器的頻率。 如果未設定，使用者端在播放受此原則保護的內容時，將不會傳送同步處理訊息。 值包含逗號分隔 <span class="codeph"> name=value</span> 以下列格式配對： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force|hardStop=numberValue</span> </p> <p class="- topic/p "> 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_25CAF96C27F34848A95B2E3693847C71"><span class="codeph"> 開始</span> （必要） — 開始間隔會指定自上次同步化後，使用者端應該開始與伺服器同步化的分鐘數。 </li> 
      <li id="li_CC9068CFE75645029C947C9E1B53351F"><span class="codeph"> 強制</span> （選用） — 強制同步機率是使用者端在播放期間強制同步訊息的機率(0-100)。 </li> 
      <li id="li_C31A6250F19348FBB8B7569D00C6314E"><span class="codeph"> hardStop</span> （選用） — 硬停止間隔是使用者端在無法同步處理時播放失敗的時間（分鐘）。 如果已設定，則必須大於開始間隔。 </li> 
     </ul>在更新期間，使用 <span class="codeph"> -sync</span> 移除同步化要求的剩餘引數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">指出此原則是否有根授權(請參閱 <i class="+ topic/ph hi-d/i ">增強授權鏈結</i> 在 <i class="+ topic/ph hi-d/i ">使用Adobe存取權來保護內容</i>)。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">內容有效期的截止日期。 使用格式 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> (例如， <span class="codeph"> 2009-01-31</span> 代表1月31日凌晨12:00)或 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span> (例如， <span class="codeph"> 2009-01-31-14:30:00</span> 代表1月31日下午2:30)。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">內容有效之前的日期。 兩者 <span class="codeph"> policy.expiration.endDate</span> 和policy.expiration.duration不能同時指定。 使用格式 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> 或 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span> (例如，2009-01-31-14:30:00代表1月31日下午2:30)。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">內容的有效時間（以分鐘為單位），從封裝時開始。 兩者 <span class="codeph"> policy.expiration.endDate</span> 和 <span class="codeph"> policy.expiration.duration</span> 不能同時指定。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權在使用者端上可快取的時間（以分鐘為單位）。 將此屬性設定為0可不允許授權快取。 值必須大於或等於0。 兩者 <span class="codeph"> policy.licenseCaching.duration</span> 和 <span class="codeph"> policy.licenseCaching.endDate</span> 不可同時使用。 </p> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">注意</b>：這個原則設定只會套用至磁碟上的授權快取。 它無法控制記憶體快取授權期間。 即使原則指定的持續時間為零，也可以在記憶體上快取授權。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不可快取授權的截止日期。 兩者 <span class="codeph"> policy.licenseCaching.duration</span> 和 <span class="codeph"> policy.licenseCaching.endDate</span> 不可同時使用。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonymous</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示是否允許匿名授權贏取。 若未指定，預設值為「false」（需要使用者名稱/密碼驗證）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果需要使用者名稱/密碼驗證，此屬性會為使用者名稱指定選用的名稱限定詞。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">伺服器在取得授權期間使用的自訂名稱/值組。 使用下列格式指定屬性： <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">名稱</span>=<span class="+ topic/ph pr-d/codeph codeph">值</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定播放視窗（以分鐘為單位），這是授權首次用於播放受保護內容後有效的持續時間。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">輸出保護限制。 值必須是下列其中一項： </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">NO_PROTECTION， USE_IF_AVAILABLE， REQUIRED， NO_PLAYBACK</i> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM模組必須具有指定的最低安全性等級或以上，才能存取受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">應用程式執行階段模組必須具有指定的最低安全性等級或以上，才能存取受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRAapplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許播放受保護內容的Adobe AIR或iOS應用程式允許清單。 屬性必須使用下列格式： <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[：<span class="+ topic/ph pr-d/codeph codeph">appId</span>[：[<span class="+ topic/ph pr-d/codeph codeph">分鐘</span>]：[<span class="+ topic/ph pr-d/codeph codeph">max</span>]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許播放受保護內容的SWF應用程式允許清單。 使用以下格式： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">URL</span> 或檔案=<span class="+ topic/ph pr-d/codeph codeph">swf_file</span>，時間=<i class="+ topic/ph hi-d/i ">max_time_to_verify</i> <i class="+ topic/ph hi-d/i ">swf_file</i> 是要計算雜湊的SWF檔案，並且 <i class="+ topic/ph hi-d/i ">max_time_to_verify</i> 允許下載和驗證SWF完成的最長時間（以秒為單位）。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">要包含在發給使用者的授權中的自訂名稱/值組。 使用以下格式： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">名稱</span>=<span class="+ topic/ph pr-d/codeph codeph">值</span> </p> <p class="- topic/p ">此選項可針對多個自訂屬性定義多次。 </p> </td> 
  </tr> 
 </tbody> 
</table>
