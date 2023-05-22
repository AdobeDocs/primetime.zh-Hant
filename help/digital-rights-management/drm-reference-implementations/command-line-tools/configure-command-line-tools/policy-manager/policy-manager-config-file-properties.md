---
keywords: 硬停
title: 配置屬性
description: 配置屬性
copied-description: true
exl-id: f88c57d6-d951-4d7a-8de1-44cd1aa8e5f7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 0%

---

# 配置屬性 {#configuration-properties}

<!--<a id="section_20A96CDCC5C340DEAF455C6E300E5712"></a>-->

>[!NOTE]
>
>對於包含的屬性名 `.n`，也請參見Wiki頁。 `n` 表示以1開頭的整數，並為屬性的每個實例增加。 例如： `policy.license.customProp.n`。

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
   <td colname="2" class="- topic/entry "> 人可讀的DRM策略名稱。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requireKeyServer</span> <p class="- topic/p "><span class="codeph"> -keyServer</span> <i class="+ topic/ph hi-d/i ">布爾</i> </p> </td> 
   <td colname="2" class="- topic/entry ">適用以下條件： 
    <ul id="ul_AF4EBD6C19DC4DFAAB4756EF24BAC57D"> 
     <li id="li_6CC48ABF78EC426E9FC51458BD946BC9">如果為true，則需要HTTPS密鑰伺服器才能將密鑰傳遞到iOS。 </li> 
     <li id="li_63046A4ED7354C1E9E823B475E4AEFF7">如果未指定，則預設值為false。 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.enforceJailbreak</span> <p class="- topic/p "><span class="codeph"> -enforceJailbreak</span> <i class="+ topic/ph hi-d/i ">布爾</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 對於支援越獄檢測的設備（如果為true），則在檢測到越獄時不允許播放。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> 策略。關鍵</span> <p class="- topic/p "><span class="codeph"> 關鍵</span> <i class="+ topic/ph hi-d/i ">布爾</i> </p> </td> 
   <td colname="2" class="- topic/entry ">設定DRM策略的重要性： 
    <ul id="ul_63F1994798894233A67AC4F8220AB642"> 
     <li id="li_D05DD9AD70464D6B9DB9DFF95846E589">如果為true，則伺服器必須瞭解DRM策略的所有部分，這表示預設行為。 </li> 
     <li id="li_0211473DAF1F426787CC4A68F47643C6">如果為false，則伺服器可以忽略它無法識別的DRM策略屬性。 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.asymmetric.cerfile</span> </td> 
   <td colname="2" class="- topic/entry ">其公鑰用於加密的根加密密鑰的許可證伺服器證書 <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> 增強的許可證連結</a>。 此屬性指定僅包含證書的檔案。 <p>注：支援PEM或DER格式。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -rootKey</span> <i class="+ topic/ph hi-d/i ">根密鑰</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>指定的根加密密鑰 <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> 增強的許可證連結</a>。 如果未指定密鑰，並且啟用了「增強的許可證連結」，則會自動生成隨機密鑰。 </p> <p>該密鑰必須長16個位元組，並指定為十六進位值。 十六進位值之間的空格是可選的。 對於更新，命令行選項不可用，屬性被忽略。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph">  — 域URL</span> <i class="+ topic/ph hi-d/i ">url</i> </p> </td> 
   <td colname="2" class="- topic/entry ">如果需要域註冊， <i>url</i> 指定域伺服器的URL。 對於更新，命令行選項不可用，屬性被忽略。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph">  — 域匿名</span> </p> </td> 
   <td colname="2" class="- topic/entry ">指定是否允許匿名域註冊。 將屬性設定為true或包括此命令行選項以允許匿名訪問。 <p>注：此選項不能與 <span class="codeph"> -domainAuthNS</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS</span> <i class="+ topic/ph hi-d/i ">命名空間</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>域註冊的驗證命名空間。 如果指定，則客戶端需要使用指定機構頒發的用戶名和密碼進行身份驗證。 </p> <p>對於更新，命令行選項不可用，屬性被忽略。 </p> <p>注：此選項不能與 <span class="codeph">  — 域匿名</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analog</span> <p class="- topic/p "><span class="codeph"> -op模擬</span> <i class="+ topic/ph hi-d/i ">模擬選項</i> </p> </td> 
   <td colname="2" class="- topic/entry ">支援模擬輸出保護約束和以下值： 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_F920EC01159C4231AFBE579D487C8770"><span class="+ topic/ph pr-d/codeph codeph"> 無保護</span> </li> 
     <li class="- topic/li " id="li_2DE0494AF8C446EB9E4567915F5E97C3"><span class="+ topic/ph pr-d/codeph codeph"> 使用_IF_AVAILABLE</span> </li> 
     <li class="- topic/li " id="li_207D2D6256D6423FBDABA7A8627A9B7D"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </li> 
     <li class="- topic/li " id="li_E17D944BED5F403FAE94708EE6AE4BBE"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </li> 
     <li class="- topic/li " id="li_66D5A0C8FE154445A522D91EFB05B7ED"><span class="+ topic/ph pr-d/codeph codeph"> 必需</span> </li> 
     <li class="- topic/li " id="li_AF2024F212A249ED99AEECCF3E844A11"><span class="+ topic/ph pr-d/codeph codeph"> 必需_ACP</span> </li> 
     <li class="- topic/li " id="li_FFF9B7DAE77740EE895EC35D1606A527"><span class="+ topic/ph pr-d/codeph codeph"> 必需_CGMSA</span> </li> 
     <li class="- topic/li " id="li_52DED572F3AE495EB6A6450C611B440E"><span class="+ topic/ph pr-d/codeph codeph"> 無回放(_P)</span> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlickst.n</span> <p class="- topic/p "><span class="codeph"> -drm黑名單</span> <i class="+ topic/ph hi-d/i ">名稱/值對</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>限制訪問受保護內容的DRM客戶端。 此選項指定可能不使用的DRM模組版本清單（阻止清單）。 </p> <p>值由逗號分隔 <span class="codeph"> 名稱=值</span> 成對，格式如下： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|模型|vendor|env|screen|value</span> </p> <p class="- topic/p ">其他名稱/值對必須以逗號分隔。 比如說， <span class="codeph"> os=Win,release=2.0,arch=32</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlickst.n</span> <p class="- topic/p "><span class="codeph"> -runtimeBlacklsit</span> <i class="+ topic/ph hi-d/i ">名稱/值對</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>應用程式運行時間被限制為無法訪問受保護的內容。 此選項指定可能未使用的運行時模組版本清單（阻止清單）。 </p> <p>值由逗號分隔的 <span class="codeph"> 名稱=值</span> 成對，格式如下： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|application|arch|模型|vendor|env|screen|value</span> </p> <p class="- topic/p ">其他名稱/值對必須以逗號分隔。 比如說， <span class="codeph"> os=Win,application=AIR</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">名稱/值對</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定訪問受保護內容所需的設備功能。 值由逗號分隔 <span class="codeph"> 名稱=值</span> 成對，格式如下： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">比如說， <span class="codeph"> nonUserAccessibleBus=false,hardwareRootOfTrust=true</span>。 </p> <p>在更新期間，您需要應用 <span class="codeph"> -devCapabilitiesV1</span> 刪除設備功能限制的其餘參數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.sync頻率</span> <p class="- topic/p "><span class="codeph">  — 同步</span> <i class="+ topic/ph hi-d/i ">名稱/值對</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定客戶端向伺服器發送同步消息的頻率。 </p> <p>如果未設定屬性，則客戶端在播放使用DRM策略保護的內容時不會發送同步消息。 值由逗號分隔的 <span class="codeph"> 名稱=值</span> 成對，格式如下： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force=numberValue</span> </p> <p class="- topic/p ">以下清單提供了有關這些選項的附加資訊： 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_FD2C0C6DA19E455AA1917A56E09A7F84">（必需） <span class="codeph"> 開始</span> 指定客戶端需要在自上次同步以來的指定分鐘內開始與伺服器同步。 </li> 
      <li id="li_9DEBC57385A442C3929AE3D0E3FA8992">（可選） <span class="codeph"> 力</span> 是客戶端在回放期間需要強制執行同步消息的概率(0-100)。 </li> 
     </ul>在更新期間，使用 <span class="codeph">  — 同步</span> 刪除同步要求的其餘參數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">指示此DRM策略是否具有根許可證。 <p>有關詳細資訊，請參見 <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> 增強的許可證連結</a>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">內容生效的日期。 可以應用以下格式之一： 
    <ul id="ul_6610B44D0C16485098F6F45DE3F151D7"> 
     <li id="li_986707D4C6164C44B3CCBE2EEB4C09B6"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> <p>比如說， <span class="codeph"> 2009-01-31</span> 意味著1月31日凌晨12點。 </p> </li> 
     <li id="li_E15B782716124F6EAEFB04D16E5280DB"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span> <p>比如說， <span class="codeph"> 2009-01-31-14:30:00</span> 意味著1月31日下午2:30 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">內容變為無效的日期。 </p> <p>注：無法指定 <span class="codeph"> policy.expiration.endDate</span> 和 <span class="codeph"> policy.expiration.duration</span> 同時。 </p> <p>例如，2009-01-31-14:30:00表示內容將於1月31日下午2:30過期。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">內容變為無效的時間（以分鐘為單位）。 打包內容時開始的時間。 </p> <p>注：無法指定 <span class="codeph"> policy.expiration.endDate</span> 和 <span class="codeph"> policy.expiration.duration</span> 同時。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在客戶端上快取許可證的時間（以分鐘為單位）。 可以將此屬性設定為0以阻止許可證快取。 值必須為0或更高。 </p> <p>注：無法指定 <span class="codeph"> policy.licenseCaching.duration</span> 和 <span class="codeph"> policy.licenseCaching.endDate</span> 同時。 </p> <p class="- topic/p ">此DRM策略設定僅應用於磁碟上的許可證快取，不控制記憶體快取的許可證持續時間。 即使您未指定持續時間為零的DRM策略，也可以在記憶體中快取許可證。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">您無法再快取許可證的日期。 </p> <p>注：無法指定 <span class="codeph"> policy.licenseCaching.duration</span> 和 <span class="codeph"> policy.licenseCaching.endDate</span> 同時。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anomy</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示是否允許匿名獲取許可證。 預設值設定為 <span class="codeph"> 假</span>，表示需要用戶名和密碼。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果需要用戶名和密碼，此屬性指定用戶名的可選名稱限定符。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在獲取許可證期間由伺服器使用的自定義名稱/值對。 可以應用以下格式來指定屬性： <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">名稱</span>=<span class="+ topic/ph pr-d/codeph codeph">值</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定播放窗口（以分鐘為單位）。 此值表示在首次播放受保護內容之後許可證的有效時間。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">輸出保護約束，它必須是以下值之一： 
     <ul id="ul_wsb_kfp_fs"> 
      <li id="li_FE012306F22F4F3FB981FE167C7A8B94"><span class="codeph"> 無保護</span> </li> 
      <li id="li_A5591DC8983848FE9823C2A261BF7713"><span class="codeph"> 使用_IF_AVAILABLE</span> </li> 
      <li id="li_74102C36ADE841C4B9ED71156E0A4C2C"><span class="codeph"> 必需</span> </li> 
      <li id="li_769E15C85B4E4DD48213DBD019D60BA7"><span class="codeph"> 無回放(_P)</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.ota</span> </td> 
   <td colname="2" class="- topic/entry ">指定應允許列出的空中(OTA)連接類型。 有效的連接類型包括： 
    <ul id="ul_iz5_4fp_fs"> 
     <li id="li_FB07519EFEFE4B95B3B1F5BFD4DE6591"><span class="codeph"> Miracast</span> </li> 
     <li id="li_51E7DE83679F4630B01264407DAD0E84"><span class="codeph"> AIRPLAY</span> </li> 
     <li id="li_D499A0487AAC409CB2CEA6164265D3CF"><span class="codeph"> DLNA</span> </li> 
     <li id="li_4FCC0EC4A0FC48F99A13EC8A1B78D6A1"><span class="codeph"> 維迪</span> </li> 
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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">應用程式運行時模組必須至少具有指定的最低安全級別才能訪問受保護的內容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">非Flash應用程式(Adobe AIR、iOS、Android等)的允許清單 允許播放受保護內容。 該屬性必須使用以下格式： <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">應用ID</span>[:[<span class="+ topic/ph pr-d/codeph codeph">分鐘</span>]:[<span class="+ topic/ph pr-d/codeph codeph">最大</span>]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允許播放受保護內容的SWF應用程式清單。 該屬性必須使用以下格式： </p> <p class="- topic/p "> 
     <ul id="ul_EC20F52AD95C4BE3B7F703048A43CDF0"> 
      <li id="li_3E4A47D925C24834A2C25BC5943279D4"><span class="+ topic/ph pr-d/codeph codeph">URL</span> </li> 
      <li id="li_9A7CAF081C5F488FB5CDA6D38C5552F6"><span class="+ topic/ph pr-d/codeph codeph">檔案=swf_file</span> </li> 
      <li id="li_E10EA4223137489CBE4015DE999F7154"><span class="codeph">時間=最大時間到檢驗</span> </li> 
     </ul> <i class="+ topic/ph hi-d/i ">swf_file</i> 是用於計算哈希的SWF檔案， <i class="+ topic/ph hi-d/i ">max_time_to_verify</i> 是允許下載和驗證SWF完成的最長時間（秒）。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在向用戶頒發許可證時必須包括在許可證中的自定義名稱/值對。 您需要指定以下格式： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n=name</span> </p> <p class="- topic/p ">可以多次為多個自定義屬性定義此選項。 </p> </td> 
  </tr> 
 </tbody> 
</table>
