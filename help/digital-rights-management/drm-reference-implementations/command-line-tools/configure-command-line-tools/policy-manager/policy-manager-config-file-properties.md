---
keywords: 硬停
title: 配置屬性
description: 配置屬性
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 0%

---


# 配置屬性{#configuration-properties}

<!--<a id="section_20A96CDCC5C340DEAF455C6E300E5712"></a>-->

>[!NOTE]
>
>對於包含`.n`的屬性名稱，`n`代表一個整數，從1開始，並且會針對屬性的每個實例增加。 例如：`policy.license.customProp.n`。

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 屬性／命令行選項 </th> 
   <th colname="2" class="- topic/entry entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">npolicyname</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 人類可讀的DRM策略名稱。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requireKeyServer</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">keyServerboolean</i> </p> </td> 
   <td colname="2" class="- topic/entry ">適用下列條件： 
    <ul id="ul_AF4EBD6C19DC4DFAAB4756EF24BAC57D"> 
     <li id="li_6CC48ABF78EC426E9FC51458BD946BC9">如果為true，則需要HTTPS金鑰伺服器才能將金鑰傳送至iOS。 </li> 
     <li id="li_63046A4ED7354C1E9E823B475E4AEFF7">如果未指定，則預設為false。 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.enforceJailbreak</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">enforceJailbreakboolean</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 對於支援越獄偵測的裝置（若為true），則不允許在偵測到越獄時播放。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> -關</span> <i class="+ topic/ph hi-d/i ">鍵布爾值</i> </p> </td> 
   <td colname="2" class="- topic/entry ">設定DRM策略的重要性： 
    <ul id="ul_63F1994798894233A67AC4F8220AB642"> 
     <li id="li_D05DD9AD70464D6B9DB9DFF95846E589">如果為true，則伺服器必須瞭解DRM策略的所有部分，這些部分代表預設行為。 </li> 
     <li id="li_0211473DAF1F426787CC4A68F47643C6">如果為false，則伺服器可以忽略它無法識別的DRM策略屬性。 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.ansymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">許可證伺服器證書，其公鑰用於加密<a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external">增強型許可證鏈</a>的根加密密鑰。 此屬性指定僅包含證書的檔案。 <p>注意： 支援PEM或DER格式。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">rootKeyroot-key</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>指定<a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external">增強授權連結</a>的根加密密鑰。 如果未指定任何金鑰，並啟用「增強授權鏈結」，則會自動產生隨機金鑰。 </p> <p>索引鍵必須長16個位元組，並指定為十六進位值。 十六進位值之間的空格是可選的。 對於更新，命令行選項不可用，而屬性將被忽略。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">domainURLurl</i> </p> </td> 
   <td colname="2" class="- topic/entry ">如果需要域註冊，<i>url</i>會指定域伺服器的URL。 對於更新，命令行選項不可用，而屬性將被忽略。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry ">指定是否允許匿名域註冊。 將屬性設為true或包含此命令列選項以允許匿名訪問。 <p>注意：此選項不能與<span class="codeph"> -domainAuthNS</span>一起使用。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS</span> <i class="+ topic/ph hi-d/i ">namespace</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>網域註冊的驗證命名空間。 如果指定，客戶端需要使用指定授權機構發出的用戶名和密碼進行驗證。 </p> <p>對於更新，命令行選項不可用，而屬性將被忽略。 </p> <p>注意：此選項不能與<span class="codeph"> -domainAnon</span>一起使用。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analog</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">opAnalogAnalogOption</i> </p> </td> 
   <td colname="2" class="- topic/entry ">支援模擬輸出保護約束和以下值： 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_F920EC01159C4231AFBE579D487C8770"><span class="+ topic/ph pr-d/codeph codeph"> 無保護</span> </li> 
     <li class="- topic/li " id="li_2DE0494AF8C446EB9E4567915F5E97C3"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </li> 
     <li class="- topic/li " id="li_207D2D6256D6423FBDABA7A8627A9B7D"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </li> 
     <li class="- topic/li " id="li_E17D944BED5F403FAE94708EE6AE4BBE"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </li> 
     <li class="- topic/li " id="li_66D5A0C8FE154445A522D91EFB05B7ED"><span class="+ topic/ph pr-d/codeph codeph"> 必要</span> </li> 
     <li class="- topic/li " id="li_AF2024F212A249ED99AEECCF3E844A11"><span class="+ topic/ph pr-d/codeph codeph"> 必需_ACP</span> </li> 
     <li class="- topic/li " id="li_FFF9B7DAE77740EE895EC35D1606A527"><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </li> 
     <li class="- topic/li " id="li_52DED572F3AE495EB6A6450C611B440E"><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">drmBlacklistname/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>DRM用戶端無法存取受保護的內容。 此選項指定可能未使用的DRM模組版本清單（塊清單）。 </p> <p>值由逗號分隔的<span class="codeph"> name=value</span>對組成，格式如下： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|vendor|env|screen|value</span> </p> <p class="- topic/p ">其他名稱／值配對必須以逗號分隔。 例如，<span class="codeph"> os=Win,release=2.0,arch=32</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">runtimeBlacklsitname/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>應用程式執行時期無法存取受保護的內容。 此選項指定不能使用的運行時模組版本清單（塊清單）。 </p> <p>值由逗號分隔的<span class="codeph"> name=value</span>對組成，格式如下： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|application|arch|model|vendor|env|screen|value</span> </p> <p class="- topic/p ">其他名稱／值配對必須以逗號分隔。 例如，<span class="codeph"> os=Win,application=AIR</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">名稱／值配對</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定存取受保護內容所需的裝置功能。 值由逗號分隔的<span class="codeph"> name=value</span>對組成，格式如下： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">例如，<span class="codeph"> nonUserAccessibleBus=false,hardwareRootOfTrust=true</span>。 </p> <p>在更新期間，您需要應用<span class="codeph"> -devCapabilitiesV1</span>，而不應使用移除裝置功能限制的其餘引數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">syncname/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定客戶端向伺服器發送同步消息的頻率。 </p> <p>如果未設定屬性，則客戶端在播放使用DRM策略保護的內容時不會發送同步消息。 值由逗號分隔的<span class="codeph"> name=value</span>對組成，格式如下： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force=numberValue</span> </p> <p class="- topic/p ">下列清單提供選項的其他資訊： 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_FD2C0C6DA19E455AA1917A56E09A7F84">（必要）<span class="codeph"> start</span>指定客戶端需要在上次同步後指定的分鐘內開始與伺服器同步。 </li> 
      <li id="li_9DEBC57385A442C3929AE3D0E3FA8992">（可選）<span class="codeph"> force</span>是客戶端在播放期間需要強制同步消息的概率(0-100)。 </li> 
     </ul>在更新期間，請使用<span class="codeph"> -sync</span>而不使用其餘參數來刪除同步要求。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">指出此DRM策略是否具有根許可證。 <p>如需詳細資訊，請參閱<a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external">增強授權鏈結</a>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">內容生效的日期。 您可以套用下列其中一種格式： 
    <ul id="ul_6610B44D0C16485098F6F45DE3F151D7"> 
     <li id="li_986707D4C6164C44B3CCBE2EEB4C09B6"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> <p>例如，<span class="codeph"> 2009-01-31</span>表示1月31日12:00 AM。 </p> </li> 
     <li id="li_E15B782716124F6EAEFB04D16E5280DB"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span> <p>例如，<span class="codeph"> 2009-01-31-14:30:00</span>表示1月31日下午2:30。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">內容變為無效的日期。 </p> <p>注意：您無法同時指定<span class="codeph"> policy.expiration.endDate</span>和<span class="codeph"> policy.expiration.duration</span>。 </p> <p>例如，2009-01-31-14:30:00表示內容將於1月31日下午2:30到期。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">內容變為無效的時間（以分鐘為單位）。 封裝內容時的開始時間。 </p> <p>注意：您無法同時指定<span class="codeph"> policy.expiration.endDate</span>和<span class="codeph"> policy.expiration.duration</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在用戶端上快取授權的時間（以分鐘為單位）。 您可以將此屬性設為0以防止授權快取。 值必須為0或更高。 </p> <p>注意：您無法同時指定<span class="codeph"> policy.licenseCaching.duration</span>和<span class="codeph"> policyneCaching.endDate</span>。 </p> <p class="- topic/p ">此DRM策略設定僅應用於磁碟上的許可證快取，而不控制記憶體快取的許可證持續時間。 即使您未指定持續時間為零的DRM政策，授權仍可快取在記憶體中。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">您無法再快取授權的日期。 </p> <p>注意：您無法同時指定<span class="codeph"> policy.licenseCaching.duration</span>和<span class="codeph"> policyneCaching.endDate</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonymous</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指出是否允許匿名取得授權。 預設值設為<span class="codeph"> false</span>，表示需要使用者名稱和密碼。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果需要用戶名和密碼，此屬性會為用戶名指定可選的名稱限定符。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">伺服器在取得授權期間使用的自訂名稱／值配對。 您可以套用下列格式來指定屬性：<span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定以分鐘為單位的播放窗口。 此值代表授權在第一次播放受保護的內容後有效的時間。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">輸出保護約束，必須是以下值之一： 
     <ul id="ul_wsb_kfp_fs"> 
      <li id="li_FE012306F22F4F3FB981FE167C7A8B94"><span class="codeph"> 無保護</span> </li> 
      <li id="li_A5591DC8983848FE9823C2A261BF7713"><span class="codeph"> USE_IF_AVAILABLE</span> </li> 
      <li id="li_74102C36ADE841C4B9ED71156E0A4C2C"><span class="codeph"> 必要</span> </li> 
      <li id="li_769E15C85B4E4DD48213DBD019D60BA7"><span class="codeph"> NO_PLAYBACK</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.ota</span> </td> 
   <td colname="2" class="- topic/entry ">指定應允許的Over the Air(OTA)連接類型。 有效的連接類型包括： 
    <ul id="ul_iz5_4fp_fs"> 
     <li id="li_FB07519EFEFE4B95B3B1F5BFD4DE6591"><span class="codeph"> MIRACAST</span> </li> 
     <li id="li_51E7DE83679F4630B01264407DAD0E84"><span class="codeph"> AIRPLAY</span> </li> 
     <li id="li_D499A0487AAC409CB2CEA6164265D3CF"><span class="codeph"> DLNA</span> </li> 
     <li id="li_4FCC0EC4A0FC48F99A13EC8A1B78D6A1"><span class="codeph"> WIDI</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.resolution</span> </td> 
   <td colname="2" class="- topic/entry "> 指定在其中定義基於解析度的約束的配置檔案。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定允許DRM模組訪問受保護內容的最低安全級別。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">應用程式執行時期模組必須至少具備指定的最低安全等級才能存取受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">非Flash應用程式(Adobe AIR、iOS、Android等)的允許清單 可播放受保護內容。 屬性必須使用下列格式：<span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min</span>]:[<span class="+ topic/ph pr-d/codeph codeph">max</span>] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許播放受保護內容的SWF應用程式清單。 屬性必須使用下列格式： </p> <p class="- topic/p "> 
     <ul id="ul_EC20F52AD95C4BE3B7F703048A43CDF0"> 
      <li id="li_3E4A47D925C24834A2C25BC5943279D4"><span class="+ topic/ph pr-d/codeph codeph">URL</span> </li> 
      <li id="li_9A7CAF081C5F488FB5CDA6D38C5552F6"><span class="+ topic/ph pr-d/codeph codeph">file=swf_file</span> </li> 
      <li id="li_E10EA4223137489CBE4015DE999F7154"><span class="codeph">time=max_time_to_verify</span> </li> 
     </ul> <i class="+ topic/ph hi-d/i ">swf_</i> file是用於計算散列的SWF檔案， <i class="+ topic/ph hi-d/i ">max_time_to_</i> verify是允許下載並驗證SWF完成的最大時間（秒）。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在授權給使用者時，您必須在授權中加入的自訂名稱／值配對。 您必須指定下列格式： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n=name</span> </p> <p class="- topic/p ">您可以多次為多個自訂屬性定義此選項。 </p> </td> 
  </tr> 
 </tbody> 
</table>
