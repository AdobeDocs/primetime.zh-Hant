---
keywords: 硬式停止
title: 設定屬性
description: 設定屬性
copied-description: true
exl-id: f88c57d6-d951-4d7a-8de1-44cd1aa8e5f7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 0%

---

# 設定屬性 {#configuration-properties}

<!--<a id="section_20A96CDCC5C340DEAF455C6E300E5712"></a>-->

>[!NOTE]
>
>屬性名稱包含 `.n`，則 `n` 代表以1開頭的整數，並且對於屬性的每個執行個體都會增加。 例如： `policy.license.customProp.n`.

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
   <td colname="2" class="- topic/entry "> 人類看得懂的DRM原則名稱。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requireKeyServer</span> <p class="- topic/p "><span class="codeph"> -keyServer</span> <i class="+ topic/ph hi-d/i ">布林值</i> </p> </td> 
   <td colname="2" class="- topic/entry ">下列條件適用： 
    <ul id="ul_AF4EBD6C19DC4DFAAB4756EF24BAC57D"> 
     <li id="li_6CC48ABF78EC426E9FC51458BD946BC9">如果為true，則需要HTTPS金鑰伺服器，才能將金鑰傳遞至iOS。 </li> 
     <li id="li_63046A4ED7354C1E9E823B475E4AEFF7">如果未指定，預設值為false。 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.enforceJailbreak</span> <p class="- topic/p "><span class="codeph"> -enforceJailbreak</span> <i class="+ topic/ph hi-d/i ">布林值</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 對於支援越獄偵測的裝置，如果為true，則不允許在偵測到越獄時播放。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> -critical</span> <i class="+ topic/ph hi-d/i ">布林值</i> </p> </td> 
   <td colname="2" class="- topic/entry ">設定DRM原則的重要性： 
    <ul id="ul_63F1994798894233A67AC4F8220AB642"> 
     <li id="li_D05DD9AD70464D6B9DB9DFF95846E589">如果為true，則伺服器必須瞭解DRM政策的所有部分，這代表預設行為。 </li> 
     <li id="li_0211473DAF1F426787CC4A68F47643C6">如果為false，則伺服器可以忽略它無法識別的DRM原則屬性。 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">授權伺服器憑證，其公開金鑰用於加密的根加密金鑰 <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> 增強授權鏈結</a>. 此屬性會指定僅包含憑證的檔案。 <p>注意：同時支援PEM或DER格式。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -rootKey</span> <i class="+ topic/ph hi-d/i ">root-key</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>指定根加密金鑰 <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> 增強授權鏈結</a>. 若未指定金鑰且已啟用增強授權鏈結，則會自動產生隨機金鑰。 </p> <p>金鑰長度必須是16個位元組，並指定為十六進位值。 十六進位值之間的空白字元為選用。 更新時，無法使用命令列選項，並忽略屬性。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -domainUrl</span> <i class="+ topic/ph hi-d/i ">url</i> </p> </td> 
   <td colname="2" class="- topic/entry ">如果需要網域註冊， <i>url</i> 指定網域伺服器的URL。 更新時，無法使用命令列選項，並忽略屬性。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry ">指定是否允許匿名網域註冊。 將屬性設定為true或包含此命令列選項以允許匿名存取。 <p>注意：此選項無法搭配 <span class="codeph"> -domainAuthNS</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS</span> <i class="+ topic/ph hi-d/i ">名稱空間</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>網域註冊的驗證名稱空間。 如果指定，使用者端需要使用指定授權單位所簽發的使用者名稱和密碼進行驗證。 </p> <p>更新時，無法使用命令列選項，並忽略屬性。 </p> <p>注意：此選項無法搭配 <span class="codeph"> -domainAnon</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analog</span> <p class="- topic/p "><span class="codeph"> -opAnalog</span> <i class="+ topic/ph hi-d/i ">類比選項</i> </p> </td> 
   <td colname="2" class="- topic/entry ">支援類比輸出保護限制，以及下列值： 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_F920EC01159C4231AFBE579D487C8770"><span class="+ topic/ph pr-d/codeph codeph"> 無保護(_P)</span> </li> 
     <li class="- topic/li " id="li_2DE0494AF8C446EB9E4567915F5E97C3"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </li> 
     <li class="- topic/li " id="li_207D2D6256D6423FBDABA7A8627A9B7D"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </li> 
     <li class="- topic/li " id="li_E17D944BED5F403FAE94708EE6AE4BBE"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </li> 
     <li class="- topic/li " id="li_66D5A0C8FE154445A522D91EFB05B7ED"><span class="+ topic/ph pr-d/codeph codeph"> 必填</span> </li> 
     <li class="- topic/li " id="li_AF2024F212A249ED99AEECCF3E844A11"><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_ACP</span> </li> 
     <li class="- topic/li " id="li_FFF9B7DAE77740EE895EC35D1606A527"><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </li> 
     <li class="- topic/li " id="li_52DED572F3AE495EB6A6450C611B440E"><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -drm黑名單</span> <i class="+ topic/ph hi-d/i ">名稱/值組</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>無法存取受保護內容的DRM使用者端。 此選項會指定不可使用的DRM模組版本清單（區塊清單）。 </p> <p>值包含逗號分隔 <span class="codeph"> name=value</span> 以下列格式配對： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">其他名稱/值組必須以逗號分隔。 例如， <span class="codeph"> os=Win，release=2.0，arch=32</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -runtimeBlacklist</span> <i class="+ topic/ph hi-d/i ">名稱/值組</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>應用程式執行階段無法存取受保護的內容。 此選項會指定不可使用的執行階段模組版本清單（封鎖清單）。 </p> <p>值包含逗號分隔 <span class="codeph"> name=value</span> 以下列格式配對： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|版本|application|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">其他名稱/值組必須以逗號分隔。 例如， <span class="codeph"> os=Win，application=AIR</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">名稱/值組</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定存取受保護內容所需的裝置功能。 值包含逗號分隔 <span class="codeph"> name=value</span> 以下列格式配對： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">例如， <span class="codeph"> nonUserAccessibleBus=false，hardwareRootOfTrust=true</span>. </p> <p>在更新期間，您需要套用 <span class="codeph"> -devCapabilitiesV1</span> 不包含移除裝置功能限制的其餘引數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -sync</span> <i class="+ topic/ph hi-d/i ">名稱/值組</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定使用者端傳送同步化訊息至伺服器的頻率。 </p> <p>如果未設定此屬性，使用者端播放受DRM原則保護的內容時，將不會傳送同步處理訊息。 值包含逗號分隔 <span class="codeph"> name=value</span> 以下列格式配對： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force=numberValue</span> </p> <p class="- topic/p ">下列清單提供有關選項的其他資訊： 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_FD2C0C6DA19E455AA1917A56E09A7F84">（必要） <span class="codeph"> 開始</span> 指定使用者端必須在自上次同步後指定的分鐘內，開始與伺服器同步。 </li> 
      <li id="li_9DEBC57385A442C3929AE3D0E3FA8992">（選擇性） <span class="codeph"> 強制</span> 是使用者端在播放期間需要強制同步化訊息的機率(0-100)。 </li> 
     </ul>在更新期間，使用 <span class="codeph"> -sync</span> 移除同步化要求的剩餘引數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">指出此DRM原則是否有根授權。 <p>如需詳細資訊，請參閱 <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> 增強授權鏈結</a>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">內容生效的日期。 您可以套用下列其中一種格式： 
    <ul id="ul_6610B44D0C16485098F6F45DE3F151D7"> 
     <li id="li_986707D4C6164C44B3CCBE2EEB4C09B6"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> <p>例如， <span class="codeph"> 2009-01-31</span> 表示1月31日凌晨12:00。 </p> </li> 
     <li id="li_E15B782716124F6EAEFB04D16E5280DB"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span> <p>例如， <span class="codeph"> 2009-01-31-14:30:00</span> 表示1月31日下午2:30。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">內容變成無效之前的日期。 </p> <p>附註：您無法指定 <span class="codeph"> policy.expiration.endDate</span> 和 <span class="codeph"> policy.expiration.duration</span> 同時。 </p> <p>例如，2009-01-31-14:30:00表示內容將於1月31日下午2:30過期。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">內容變得無效的時間，以分鐘為單位。 時間從您封裝內容時開始。 </p> <p>附註：您無法指定 <span class="codeph"> policy.expiration.endDate</span> 和 <span class="codeph"> policy.expiration.duration</span> 同時。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可在使用者端快取授權的時間（分鐘）。 您可以將此屬性設為0，以防止授權快取。 值必須大於或等於0。 </p> <p>附註：您無法指定 <span class="codeph"> policy.licenseCaching.duration</span> 和 <span class="codeph"> policy.licenseCaching.endDate</span> 同時。 </p> <p class="- topic/p ">此DRM原則設定僅套用至磁碟上的授權快取，不會控制記憶體快取的授權期間。 即使您未指定持續期間為零的DRM原則，亦可在記憶體中快取授權。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">之後不能再快取授權的日期。 </p> <p>附註：您無法指定 <span class="codeph"> policy.licenseCaching.duration</span> 和 <span class="codeph"> policy.licenseCaching.endDate</span> 同時。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonymous</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示是否允許匿名授權贏取。 預設值設為 <span class="codeph"> false</span>，這表示需要使用者名稱和密碼。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果需要使用者名稱和密碼，此屬性會為使用者名稱指定選用的名稱限定詞。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">伺服器在取得授權期間使用的自訂名稱/值組。 您可以套用下列格式來指定屬性： <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">名稱</span>=<span class="+ topic/ph pr-d/codeph codeph">值</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定播放視窗（以分鐘為單位）。 此值代表在第一次播放受保護內容後，授權的有效時間。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">輸出保護限制，必須為下列其中一個值： 
     <ul id="ul_wsb_kfp_fs"> 
      <li id="li_FE012306F22F4F3FB981FE167C7A8B94"><span class="codeph"> 無保護(_P)</span> </li> 
      <li id="li_A5591DC8983848FE9823C2A261BF7713"><span class="codeph"> USE_IF_AVAILABLE</span> </li> 
      <li id="li_74102C36ADE841C4B9ED71156E0A4C2C"><span class="codeph"> 必填</span> </li> 
      <li id="li_769E15C85B4E4DD48213DBD019D60BA7"><span class="codeph"> NO_PLAYBACK</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.ota</span> </td> 
   <td colname="2" class="- topic/entry ">指定應該允許列出的無線傳送(OTA)連線型別。 有效的連線型別包括： 
    <ul id="ul_iz5_4fp_fs"> 
     <li id="li_FB07519EFEFE4B95B3B1F5BFD4DE6591"><span class="codeph"> MIRACAST</span> </li> 
     <li id="li_51E7DE83679F4630B01264407DAD0E84"><span class="codeph"> AIRPLAY</span> </li> 
     <li id="li_D499A0487AAC409CB2CEA6164265D3CF"><span class="codeph"> DLNA</span> </li> 
     <li id="li_4FCC0EC4A0FC48F99A13EC8A1B78D6A1"><span class="codeph"> WIDI</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.resolution</span> </td> 
   <td colname="2" class="- topic/entry "> 指定定義以解析度為基礎的限制的組態檔案。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定允許DRM模組存取受保護內容的最低安全性等級。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">應用程式執行階段模組必須至少具有指定的最低安全性層級，才能存取受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRAapplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">非Flash應用程式的允許清單(Adobe AIR、iOS、Android等) 可播放受保護內容的內容。 屬性必須使用下列格式： <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[：<span class="+ topic/ph pr-d/codeph codeph">appId</span>[：[<span class="+ topic/ph pr-d/codeph codeph">分鐘</span>]：[<span class="+ topic/ph pr-d/codeph codeph">max</span>]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許播放受保護內容的SWF應用程式允許清單。 屬性必須使用下列格式： </p> <p class="- topic/p "> 
     <ul id="ul_EC20F52AD95C4BE3B7F703048A43CDF0"> 
      <li id="li_3E4A47D925C24834A2C25BC5943279D4"><span class="+ topic/ph pr-d/codeph codeph">URL</span> </li> 
      <li id="li_9A7CAF081C5F488FB5CDA6D38C5552F6"><span class="+ topic/ph pr-d/codeph codeph">file=swf_file</span> </li> 
      <li id="li_E10EA4223137489CBE4015DE999F7154"><span class="codeph">time=max_time_to_verify</span> </li> 
     </ul> <i class="+ topic/ph hi-d/i ">swf_file</i> 是用於運算雜湊的SWF檔案，並且 <i class="+ topic/ph hi-d/i ">max_time_to_verify</i> 是允許下載及驗證SWF完成的最長時間（秒）。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">將授權核發給使用者時，您必須在授權中包含的自訂名稱/值組。 您必須指定下列格式： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n=name</span> </p> <p class="- topic/p ">您可以為多個自訂屬性多次定義此選項。 </p> </td> 
  </tr> 
 </tbody> 
</table>
