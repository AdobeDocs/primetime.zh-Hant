---
title: NATIVE_ERROR通知的詳細資訊
description: NATIVE_ERROR通知的詳細資訊
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '6888'
ht-degree: 2%

---


# NATIVE_ERROR通知{#details-for-the-native-error-notification}的詳細資訊

當TVSDK處理原生錯誤時，會傳回下列部分或全部中繼資料索引鍵值為字串。

<table id="table_7F713B7A56024D8DA3C84E449D09CC91"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>中繼資料索引鍵名稱</b></th> 
   <th colname="col2" class="entry"><b>中繼資料值</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR_CODE</span> </td> 
   <td colname="col2"> <p>AVE中的原生錯誤代碼。 </p> <p>這些代碼代表下列： 
     <ul id="ul_1F33D523DDFE4CE8B4F0DC279FF7E4F8"> 
      <li id="li_07A2D9BEE6364935A61EF3BD4AB6DE27">DRM錯誤（代碼3300到3367）。 這些錯誤代碼與等效Flash Player錯誤代碼相同 </li> 
      <li id="li_433BA22DE3504AEEB623598BB4F939FA">視訊播放錯誤（-1到89） </li> 
      <li id="li_B347CB151DB94DE0A1DDEB1B33D2DABA">加密錯誤（300到307） </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR</span> </td> 
   <td colname="col2">通知的簡短說明（例如，<span class="codeph"> AAXS_InvalidVoucher</span>或<span class="codeph"> DECODER_FAILED</span>）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 說明</span> </td> 
   <td colname="col2"> 通知的詳細說明（例如，廣告解析操作失敗）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR_CODE</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.</span> PSDKErrorCoodumeric值，例如"13")。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.</span> PSDKErrorCodeas字串(例如 <span class="codeph"> kECNetworkError</span>)。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 警告</span> </td> 
   <td colname="col2"> 警告說明。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 錯誤</span> </td> 
   <td colname="col2"> 錯誤說明。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>DRM</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_SUBERROR_CODE</span> </td> 
   <td colname="col2"> DRM模組的小錯誤。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DRM_ERROR_STRING</span> </td> 
   <td colname="col2"> 錯誤說明。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DRM_ERROR_SERVER_URL</span> </td> 
   <td colname="col2"> TVSDK嘗試與之交談的DRM伺服器URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>廣告資訊清單載入失敗</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_URL</span> </td> 
   <td colname="col2"> 無法載入之內容的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_TYPE</span> </td> 
   <td colname="col2">廣告類型（<span class="codeph"> MediaResource.Type</span>列舉的常數）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_DURATION</span> </td> 
   <td colname="col2"> 廣告持續時間（以毫秒為單位）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_ID</span> </td> 
   <td colname="col2"> 指派給廣告的ID。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>檔案錯誤</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DOWNLOAD_ERROR</span> </td> 
   <td colname="col2"> 媒體檔案下載期間的錯誤說明。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> URL</span> </td> 
   <td colname="col2"> 正在下載的檔案的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> MANIFEST_ERROR</span> </td> 
   <td colname="col2"> 資訊清單檔案下載期間的錯誤說明。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> CONTENT_ERROR</span> </td> 
   <td colname="col2">片段下載期間的錯誤說明（例如<span class="codeph"> ts</span>）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>音軌錯誤</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_NAME</span> </td> 
   <td colname="col2"> 無法載入的音軌名稱，如資訊清單中所指定。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_LANGUAGE</span> </td> 
   <td colname="col2"> 音軌的語言，如資訊清單中所指定。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>尋找錯誤</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_PERIOD</span> </td> 
   <td colname="col2"> 句點的ID（整數）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_POSITION</span> </td> 
   <td colname="col2"> <p>尋找的位置（以毫秒為單位）（雙倍）。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>其他</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDITUDE_ERROR_CODE</span> </td> 
   <td colname="col2"> Auditude錯誤碼（數字）。 </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR:DRM值{#section_D240082B93D34902A18C3923C1C717B3}

Adobe視訊引擎的視訊編碼器介面會傳回`NATIVE_ERROR`中繼資料物件中的這些DRM通知。

向Adobe報告DRM錯誤時，請確定您包含`NATIVE_SUBERROR_CODE`和`DRM_ERROR_STRING`以取得疑難排解協助。

>[!TIP]
>
>此清單提供有關錯誤的TVSDK特定資訊。 有關完整說明，請參閱[ActionScript運行時錯誤ActionScript參考，以瞭解Adobe Flash Platform](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html#3300)。

<table id="table_CD59A859865F4FFDBAA249C89C74770A"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>NATIVE_- ERROR_CODE元資料鍵的值</b></th> 
   <th colname="col2" class="entry"><b>NATIVE_ERROR_NAME元資料鍵的值</b></th> 
   <th colname="col3" class="entry"><b>意義</b></th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 3300 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidVoucher</span> </td> 
   <td colname="col3"> 
    <ul id="ul_516E4CB32D624B22892DDB9266CB04CA"> 
     <li id="li_348FC0F38B11417994119B61C9244076">配銷商的軟體應該如何運作： 
      <ul id="ul_7AFD45CF92454BA4927783FAA628FBC4"> 
       <li id="li_0D9CCE61612643648C12DCDDD252E52A">如果您使用Google Chrome，而且您處於Incognito模式，且您的Flash Player版本低於11.6，則可能會發生此錯誤。 <p>我們建議播放器檢查瀏覽器的版本號，並建議用戶退出Incognito模式。 </p> </li> 
       <li id="li_1DC6B755BD0840D48BEC92568FD330BA">再次申請授權。 <p>如果請求成功，您不需要記錄或呈報。 如果請求失敗，請記錄導致錯誤的內容。 <span class="codeph"> subErrorId</span> 包含行錯誤（如果存在）。 </p> </li> 
      </ul> </li> 
     <li id="li_060B5D60C9BB419CBFA7B062FBCF2632">配銷商應該如何： 
      <ul id="ul_FADB29DBF0DA4A0E8E54134AEB7DCD8A"> 
       <li id="li_FC5B1C04D21E4AECB0EBD9ADD3198504">如果Chrome以外的Flash低於11.6版的組態未成功重試，封裝中可能會發生失敗。 </li> 
       <li id="li_A720ECE591254021879B335B81B1F76D">檢查問題是否特定於特定內容並重新封裝。 </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3301 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthenticationFailed</span> </td> 
   <td colname="col3"> <p>伺服器無法驗證或授權客戶端。 </p> 
    <ul id="ul_BE77AC1848FB4C09B6318359ACF1B8EE"> 
     <li id="li_6FB37D317D174E8488C5070D20CD241C">配銷商軟體應採取必要行動，以重新建立使用者的認證或引導使用者取得內容存取權。 </li> 
     <li id="li_BE071D59805B42D38E3E7650BC936417">配銷商應確認配銷商的授權與驗證機制運作正常。 <p>如果發佈商不打算使用驗證或授權功能，他們應檢查違規內容的政策是否需要驗證，並查看診斷策略／授權差異。 </p> </li> 
    </ul> <p>有關此錯誤代碼的詳細資訊，請參閱<a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> DRM錯誤3301的原因和解析度</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3302 </td> 
   <td colname="col2"><span class="codeph"> AAXS_RequireSSL</span> </td> 
   <td colname="col3"> <p>在Access 4.0和更新版本中，當遠端金鑰URL未使用HTTPS做為配置時，此錯誤會在iOS上引發。 需要HTTPS。 </p> 
    <ul id="ul_3D47777BBCA14B67B107FBBE3E37E40C"> 
     <li id="li_7F7BBB27AE754CC39ABAAF9269739C49">如果授權代理商使用的版本早於Access v4，或版本至少為4，但平台不是iOS，則授權代理商的軟體應記錄錯誤。 <p>錯誤只會在iOS上擲回。 </p> </li> 
     <li id="li_D83C427D2A0D47408F723EF7195070B6">如果配銷商的軟體至少是Adobe存取版本4，而平台為iOS，則配銷商必須將其使用的遠端金鑰伺服器URL變更為HTTPS。 <p>如果他們只使用HTTP，則發佈商可能必須設定HTTPS伺服器。 否則，配銷商必須將記錄的資訊提交給Adobe並呈報問題。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3303 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentExpired</span> </td> 
   <td colname="col3"> <p>您檢視的內容已根據內容提供者設定的規則過期。 subErrorId包含用戶端特定的錯誤或行錯誤。 </p> <p> 
     <ul id="ul_1E4B3B8AE87A4E79997553BB2A0E52B9"> 
      <li id="li_EE3F2EEBF73743B9A38E4FCB7531E275">配銷商的軟體應嘗試從伺服器重新取得授權一次，以判斷是否有新的未過期授權。 <p>如果沒有可用的授權或授權已過期，請允許使用者取得新的授權，或通知使用者內容無法觀看。如果內容已封裝有過期／結束日期的原則，授權伺服器記錄會報告<span class="codeph"> PolicyEvaluationException</span>，並指出原則結束日期已過期（伺服器錯誤碼303）。 檢查伺服器的日誌檔案以驗證。 </p> <p>如果可能，客戶應檢查包裝期間使用的原則，以查看其是否已過期。 Java命令行工具是：<code> java&nbsp;-jar&nbsp;libs/AdobePolicyManager.jar&nbsp;&nbsp;&nbsp;detail&nbsp;demo.pol</code> </p> </li> 
      <li id="li_50DBE680D8F04E7DA3E29C65A93188E7">配銷商應確認授權到期日是否依預期設定。 </li> 
     </ul> </p> <p>如需此錯誤程式碼的詳細資訊，請參閱使用即時串流的AMS/FMS的<a href="https://forums.adobe.com/thread/1300813" format="https" scope="external"> 3303（內容已過期）?</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三零四年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthorizationFailed</span> </td> 
   <td colname="col3">有關此錯誤代碼的詳細資訊，請參閱<a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> DRM錯誤3301的原因和解析度</a>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3305 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerConnectionFailed</span> </td> 
   <td colname="col3"> <p>由於網路延遲或客戶端離線，與許可證或域伺服器的連接超時。 通常subErrorId包含HTTP傳回程式碼。 </p> 
    <ul id="ul_938C7D8F07F64B4FA71A09DDF37E2E64"> 
     <li id="li_6648EA0049094E369BD9AE9CCA6B148D">配銷商的軟體應嘗試連接至已知正常的伺服器。 <p>如果嘗試失敗，提示用戶重新連接到網路。 如果嘗試成功，請記錄它。 </p> </li> 
     <li id="li_2ECA2C04BA08449DA3AD79A52EFAA229">配銷商應確認使用中的任何授權和網域伺服器皆已連線，且可從用戶端網路上檢視。 </li> 
    </ul> <p>有關此錯誤代碼的詳細資訊，請參閱<a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> DRM 3305 [ServerConnectionFailed]原因和解析度</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3306 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClientUpdateRequire</span> </td> 
   <td colname="col3"> 使用Android專用的較新版TVSDK。 <p>目前的用戶端無法完成所要求的動作，但更新的用戶端可以完成請求。 </p> <p>這可能有幾個原因： 
     <ul id="ul_2EC4D42D5273439FA1AFDA1A2578B3D6"> 
      <li id="li_FCA926F5FAED4E7190BE855545AB6ACF">已使用此客戶端上不可用的共用域。 在Chrome上播放時，可能會發生這種情況，但不會是其他瀏覽器，反之亦然。 <p> <p>提示：Chrome使用的PHDS/PHLS金鑰與其他瀏覽器所使用的不同。 如需詳細資訊，請參閱<a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>。 </p> </p> </li> 
      <li id="li_3B633FB699234DCEA136E9BE3CC3386D">當應用程式在5.0之前的iOS版本上執行時，會嘗試新增多個DRMSassion。 </li> 
      <li id="li_F7ED993AF0B941A7A27216B4D587A999">只支援第2版時，中繼資料的版本為3或更新版本。 </li> 
     </ul> </p> 
     <ul id="ul_EE4AE6AD4F1745A5B5623E53B599DB62"> 
      <li id="li_7A83869D4262443DA35FA1DF8D3097DD">配銷商的軟體應提醒使用者並中止作業。 <p>如果軟體可以判斷是否提供升級，請以適當的方式引導使用者前往該平台。 </p> </li> 
      <li id="li_AF9C2711FDE54DA196EB9D2864632000">如果因共用網域而發生問題，配銷商將需要向Adobe檢查更新的執行階段或程式庫。 <p>對於Flash執行階段，配銷商可強制其應用程式直接升級。 若是資料庫，配銷商需要取得更新的資料庫、重建其應用程式，並將它部署給其使用者。 </p> <p>如果因多個DRMSassion而發生問題，授權代理商將需要更新其應用程式，以在新增多個DRMSassion之前檢查iOS版本號碼。 或者，他們可以限制將應用程式散發至iOS v5和更新版本。 </p> <p>如果因為中繼資料版本高於第2版而發生問題，則問題可能已損毀中繼資料。 他們可以嘗試重建中繼資料並查看結果。 如果他們繼續看到問題，請記錄問題並呈報至Adobe。 </p> </li> 
     </ul> <p>有關此錯誤代碼的詳細資訊，請參閱<a href="https://forums.adobe.com/thread/1266675" format="https" scope="external">如何補救3306 DRMErrorEvent錯誤代碼</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3307 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InternalFailure</span> </td> 
   <td colname="col3"> <p>這通常代表「Adobe存取」程式碼中的錯誤，且未預期，除非有下列已知錯誤。 subErrorId包含用戶端特定的錯誤或行錯誤。 </p> 
    <ul id="ul_79F4A9655A2148519B1E9509C41F78C3"> 
     <li id="li_0E093AB4D6BD489B852279E6C1525A15">如果瀏覽器是Windows版的Chrome，而Flash版本是11.6（SWF版本19或更新版本），配銷商的軟體應假設使用者按下資訊列上的<span class="uicontrol">拒絕</span>，並視為3368。 </li> 
     <li id="li_0215D1089B344861A2C0A73E1067CFEF">如果3307發生在瀏覽器非Chrome或Flash版本非11.6時，配銷商應呈報至Adobe。 </li> 
    </ul> <p>重要：<span class="codeph"> 3307:1107296344(FailedToGetBrokerHandle)</span>可能發生在Chrome瀏覽器版本24-28。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3308 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WrongLicenseKey</span> </td> 
   <td colname="col3"> <p>當使用的授權包含解密內容的錯誤金鑰時，就會擲出此錯誤。 subErrorId包含用戶端特定的錯誤或行錯誤。 </p> <p>產生此錯誤的方式似乎只有兩種： 
    <ul id="ul_1C955BD74C7843809D1B5A0CDCA5ED7B"> 
     <li id="li_18F0A7FDA6584887AD9DB3EDE54080D8">客戶已修改產生授權的標準Adobe工具（例如授權者伺服器Java架構）。 <p>在這種情況下，授權包含的金鑰可能不對應於任何內容。 </p> </li> 
     <li id="li_21D04ED1F1FA464785BC297D385766FF">客戶已使用相同的授權ID核發多份授權。 <p>在這種情況下，用戶端上有多份授權可供使用，這些授權會符合內容中繼資料，而「存取」程式碼已選取錯誤的授權供您使用。 </p> </li> 
    </ul> </p> 
    <ul id="ul_64AEE62BE36946F290067CF475A36ECA"> 
     <li id="li_9EEB2B11A4DA41E78C5840D8FAA81F0D">配銷商軟體應嘗試從伺服器重新取得授權。 
      <ul id="ul_ACADC5518B054D0A853AEED2B675DB23"> 
       <li id="li_394835C8731048A5BF7D9370AC12448C">如果沒有可用的授權或授權已過期，請提供工作流程讓使用者取得新的授權，或通知使用者內容無法觀看並記錄問題。 </li> 
       <li id="li_3FE50518BE53405F9563FA620F7EAD5F">如果這是網域系結內容（適用於AIR），請為使用者提供加入網域的方式。 </li> 
      </ul> </li> 
     <li id="li_C80B353C1AEA4E9398241420CB491E84">配銷商應： 
      <ul id="ul_B5C50009374C4EED9B2B050B48F5F0F6"> 
       <li id="li_D5E6B760E0BC4B5C949ED1544B398838">確認他們尚未自訂存取授權伺服器的授權簽發部分。 </li> 
       <li id="li_AA8F4E4B6DDD40BA8807C0920A92186B">確認他們正在為所有授權簽發唯一的授權ID。 </li> 
       <li id="li_A2C53FE779AC4FDDB65E00A2C4F43EC4">使用Adobe呈報問題。 </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3309 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptedAdditionalHeader  </span> </td> 
   <td colname="col3"> <p>如果標題大於65536位元組，就會發生此情況。 </p> 
    <ul id="ul_82C0F688519B4F43A764D59A891F1903"> 
     <li id="li_E66AC9149A0649E88A79C5289C12C395">配銷商的軟體應記錄導致錯誤的內容。 </li> 
     <li id="li_1C5916A33E7B4DC9968105B9BD20A727">配銷商應確認該錯誤是否可重複於特定內容。 重新封裝損壞的內容。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三一零年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppIDMismatch  </span> </td> 
   <td colname="col3">Android應用程式與使用中的應用程式不符。 <p>未使用正確的AIR應用程式或FlashSWF。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3311 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppVersionMismatch  </span> </td> 
   <td colname="col3"> 沒有使用。 此問題仍可能由AIR中的1.x版堆疊產生。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3312 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LicenseIntegrity  </span> </td> 
   <td colname="col3"> 若要修正此問題，請從伺服器重新下載授權。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3313 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WriteMicrosafedFailed  </span> </td> 
   <td colname="col3"> <p>當系統無法寫入檔案系統時，會發生此問題。 <span class="codeph"> subErrorId</span> 包含用戶端特定的錯誤或行錯誤。 </p> <p>在Microsoft Windows上，當加密內容的licenseID或policyID過長時，Active X或NPAPI外掛flash播放器可能會擲出錯誤3313。 這是因為Windows中的最大路徑長度。 （Pepper plugin沒有此問題。） </p> <p>請參閱watson 3549660 </p> 
    <ul id="ul_DFD527D1E1224A439766DF7BED878E3B"> 
     <li id="li_FAF8FD98A4E8478CA7A92F770676ADFC">配銷商的軟體應提示使用者確認其使用者目錄未鎖定，或是已滿或已鎖定的磁碟區。 </li> 
     <li id="li_6D1136EA750A459BBECEEE5F73F527BB">如果配銷商使用AIR而非Flash，則問題可能是路徑長度限制所致。 <p>配銷商應將其AIR應用程式的名稱縮短至合理的名稱。 此外，使用較短的<span class="codeph"> licenseID</span>和<span class="codeph"> policyID</span>再次發佈內容。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3314 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CrobutedDRMMetadata  </span> </td> 
   <td colname="col3"> <p>此錯誤通常表示內容已與測試PKI憑證封裝，而播放器是使用生產PKI建立，反之亦然。 subErrorId包含用戶端特定的錯誤或行錯誤。 </p> 
    <ul id="ul_A122EF304CAF48A8B4DA1E3F4413E29B"> 
     <li id="li_A9A1A5B23E884C22A71E2DE7535FEB3B">配銷商的軟體應記錄導致錯誤的內容。 </li> 
     <li id="li_7AD7F13A4B1B4998A7E49664E7645815">配銷商應確認錯誤可透過特定內容重制。 <p>您可能必須重新封裝損壞的內容。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3315 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PermissionDenied  </span> </td> 
   <td colname="col3"> <p>有已知錯誤，當預期使用3305時，會擲回此錯誤代碼。 如需詳細資訊，請參閱<a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> DRM 3305 [ServerConnectionFailed]原因和解析度</a>。 </p> <p>AIR載入的遠端SWF不允許存取Flash Access功能。 如果在網路訪問期間發生安全錯誤，也可能拋出此錯誤代碼。 例如，目標伺服器不使用crossdomain.xml連接客戶端，或者無法訪問crossdomain.xml。 </p> <p>如需詳細資訊，請參閱<a href="https://forums.adobe.com/thread/1266592" format="https" scope="external"> DRM錯誤3315可能的根本原因和解析度</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3316 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NOTUSED_MOVED  </span> </td> 
   <td colname="col3"> 是<span class="codeph"> ADOBECPSHIM_MinorErr_MissingAdobeCPModule</span>。 因與Flash錯誤代碼衝突而移至3344。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3317 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LoadAdobeCPFailed  </span> </td> 
   <td colname="col3"> <p>重要： 這是罕見的錯誤，通常不會發生在生產環境中。 </p> <p>如果發生錯誤，您可以執行下列其中一項作業： 
     <ul id="ul_BC435E61623444BB98A86216531DC892"> 
      <li id="li_FA433D0758B642D2AFDCF04906B3FE18">如果您使用AIR，請重新安裝。 </li> 
      <li id="li_F08D9AAFF46244F8842DEE5FD9CBBE0A">如果您使用Flash Player，請再次下載<span class="codeph"> AdobeCP</span>模組。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3318 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncomplativeAdobeCPVersion  </span> </td> 
   <td colname="col3"> 不適用於Android。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3319 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MissingAdobeCPGetAPI  </span> </td> 
   <td colname="col3"> 不適用於Android。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三二零年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_HostAuthenticateFailed  </span> </td> 
   <td colname="col3"> 不適用於Android。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3321 </td> 
   <td colname="col2"><span class="codeph"> AAXS_I15n失敗  </span> </td> 
   <td colname="col3"> <p>為客戶端提供密鑰的過程失敗。 subErrorId包含特定於客戶端、特定於伺服器或線路錯誤。 </p> 
    <ul id="ul_98D919B9060A441AACB6106F6D8E8DA7"> 
     <li id="li_DCAB00A8AC4A426CBBD377374B3F71AE">配銷商的軟體應至少重試一次。 <p>如果您在Windows上使用Google Chrome，請提供如何允許不在沙盒中的外掛程式存取的說明。 如需詳細資訊，請參閱<a href="https://helpx.adobe.com/adobe-access/kb/error-3321.html" format="html" scope="external"> Google Chrome的取消沙盒存取denied</a>。 </p> </li> 
     <li id="li_7FB7681FE32D444BB1BDBA3E5953A2C3">配銷商應完成下列任一項工作： 
      <ul id="ul_486B64F187C44AE3B4775953A6142836"> 
       <li id="li_095B1D4CD051427CB2BFA7082B454056">如果錯誤在所有平台上都一致，您應將問題呈報為Adobe。 </li> 
       <li id="li_0C6EB7B912FA41E59657216498DA3515">如果錯誤僅限於Windows上的Chrome，請引導使用者允許未沙盒的外掛程式存取。 </li> 
      </ul> <p>配銷商應將其SWF更新至版本19或更新版本，而Chrome專用的3321錯誤會擲回3368錯誤。 錯誤3368可由配銷商的軟體加以處理。 這項變更是在Chrome Stable頻道26.0.1410.43版中引進的。 </p> <p>提示：錯誤<span class="codeph"> 3321:1090519056</span>可能發生在Flash Player11.1到11.6版。我們建議您升級至最新的Flash Player版本。 </p> </li> 
    </ul> <p>如需詳細資訊，請參閱<a href="https://forums.adobe.com/thread/1277138" format="https" scope="external"> DRM錯誤3321原因與解析度</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>全域商店損毀錯誤</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三二二年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DeviceBindingFailed  </span> </td> 
   <td colname="col3"> <p>設備似乎與初始化時存在的配置不匹配。 subErrorId包含用戶端特定或行錯誤。 </p> <p>配銷商軟體應完成下列任一項工作： 
     <ul id="ul_444401051A2E407B95BC44491E9BB71C"> 
      <li id="li_93493EA05DB44CB1AEC368663F1ABA8D"> <p>如果設備未使用Flash Player，並且正在使用AIR、iOS等，請調用<span class="codeph"> DRMManager.resetDRMVouchers()</span>。 </p> <p>如果iOS在開發階段發生問題，請要求開發人員確認在從協力廠商搶鮮版散發系統（例如HockeyApp）下載的建置與從Xcode本機建置之間切換時，是否發現問題。 在從HockeApp分發的組建版本和從Xcode分發的組建版本之間切換時，不會完全覆寫先前安裝的屬性。 這種情況可能會觸發3322錯誤。 </p> <p>若要解決此問題，開發人員應先從裝置移除舊版建置，然後再安裝新的建置。 </p> </li> 
      <li id="li_A5C9633F11584C788A2D9A23CC18FA6D">如果裝置使用Flash Player，且無法使用3322或3346錯誤碼，請參閱Adobe中有關如何在Chrome（資訊列問題）<a href="https://forums.adobe.com/message/5535907#5535907" format="https" scope="external"> DRM Error 3322/3346/3368中以程式設計方式重設DRM授權存放區的指示。/&gt;。</a> </li> 
     </ul> </p> <p>此錯誤預期不會經常發生。 在使用漫遊配置檔案的公司環境中，如果用戶正在查看受DRM保護的內容，則當用戶從不同電腦登錄時發生的機會錯誤3322增加。 如果可能，配銷商應嘗試從使用者取得此項資訊。 </p> <p>如果錯誤頻繁發生，請呈報至Adobe。 您必須通知Adobe重設授權商店是否解決問題，並告知Adobe發生錯誤的瀏覽器。 </p> <p>如需詳細資訊，請參閱下列文章： 
     <ul id="ul_C468409D1EA046178CA7F54DCDCB84EA"> 
      <li id="li_20C8CA3853574CE486F21E7A3667DAB9"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> https://forums.adobe.com/message/5520902</a> </li> 
      <li id="li_6E6F1BD6FE7843449B3E2F06F342EFF7"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> https://forums.adobe.com/message/5535911</a> </li> 
      <li id="li_2BE40E513A0C4BAD900C7B69FEF5D690"><a href="https://forums.adobe.com/message/5748618" format="https" scope="external"> https://forums.adobe.com/message/5748618</a> </li> 
      <li id="li_9C2BD122E3874E2893DD43E082A877E0"><a href="https://forums.adobe.com/message/6061165" format="https" scope="external"> https://forums.adobe.com/message/6061165</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3323 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptGlobalStateStore  </span> </td> 
   <td colname="col3"> <p>DRM客戶端使用的檔案已意外修改。 subErrorId包含用戶端特定或行錯誤。 </p> 
    <ul id="ul_96EA771046CA4B2B9FAE24D493F43FF2"> 
     <li id="li_D2693CD8EFEF46108828BA17E3F54FF6">配銷商的軟體應引導使用者以與3322相同的方式重設。 </li> 
     <li id="li_0149B82436B64E28AC2B8C9B0EB09898">如果GlobalStore的故障率高於用戶群硬碟的預期故障率，請將問題上報給Adobe。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三二四年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MachineTokenInvalid  </span> </td> 
   <td colname="col3"> 重設此應用程式的DRM本機儲存空間。 調用DRMManager.resetDRM。 <p>許可證伺服器可能無法連接到證書撤銷清單(CRL)伺服器以刷新其CRL檔案，或者客戶機正在請求已被許可證伺服器撤銷的許可證／驗證。 </p> <p>在伺服器記錄檔中，錯誤碼111是MachineTokenInvalid。 但是，在客戶端級別，錯誤代碼111被轉換為錯誤代碼3324。 </p> <p>DRM許可證伺服器管理員應檢查客戶的許可證伺服器是否能夠檢索AdobeCRL檔案。 如果客戶使用Tomcat，則客戶可以檢查<span class="filepath"> tomcat/temp/</span>目錄，以查看是否有4個CRL檔案。 </p> 
    <ul id="ul_23B7F1A104AF49E79EA87DB8E15E337E"> 
      <li id="li_855D87F251184FE688A8D5FA0F6C9EF5">如果檔案位於此目錄中，請按兩下Windows資源管理器和CRL查看器應用程式中的檔案，確定是否有任何檔案已過期。 </li> 
      <li id="li_58EC4EDA2B5146188A0FF7B33C91E2FD">如果tomcat/temp/中沒有檔案，則可以假定此許可證伺服器由於防火牆／路由問題從未能夠到達AdobeCRL伺服器。 如需詳細資訊，請參閱<a href="https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_secure_deployment_guidelines.pdf" format="http" scope="external">防火牆規則。</a></li>
    </ul> </p> <p>如果CRL檔案不可用或已過期，則必須確認是否可以訪問許可證伺服器。 在客戶的許可證伺服器上開啟網路嗅探器，重新啟動伺服器，並讓客戶端嘗試向伺服器請求許可證。 您可以觀察網路流量，以查看對下列URL端點的呼叫是否成功： <p>提示： 您也可以在瀏覽器中輸入下列CRL URL，以查看您是否可以手動下載每個檔案。 </p> 
    <ul id="ul_9B65C7ABBDEC4AC9BF3755FFD3587971"> 
      <li id="li_6867A9050E8D421C9138AC853D1784C9"><a href="https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl</a> </li> 
      <li id="li_6431689260554EAFAFDA2EC31798DCB5"><a href="https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl</a> </li> 
      <li id="li_2939674D0F854ADEB67E45FD216288A2"><a href="https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessRootCA.crl</a> </li> 
      <li id="li_96386E00BE9D4CB99D100057A5F7C6DD">crl3.adobe.com/AdobeSystemsIncorporated FlashAccessRuntime/LatestCRL.crl</li> 
    </ul> </p> <p>如果防火牆規則已開啟且目前沒有3324錯誤，則可能會發生暫時網路問題。 檢查客戶的伺服器日誌（可能位於<span class="codeph"> /tomcat/logs/</span>目錄），以確定當許可證伺服器嘗試獲取證書撤銷清單時是否發生錯誤。 <p>重要： 當大量（或拆分）的客戶端在更新CRL檔案時向臨時網路問題報告3324錯誤時，可能會發生錯誤。 解決網路問題時，3324問題也已解決。 </p> </p> <p>如果CRL檔案中的所有4個都存在於<span class="filepath"> tomcat/temp/</span>目錄中，並且客戶端仍然收到3324個錯誤代碼，則CRL檔案可能存在檔案訪問問題。 要解決此問題，您可能需要查看日誌並清除現有的CRL檔案。 </p> <p>如果沒有伺服器問題，請提示使用者重設，如3322所述。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>伺服器儲存損壞錯誤</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
</tr> 
  <tr> 
   <td colname="col1"> 郵編：3325 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptServerStateStore  </span> </td> 
   <td colname="col3"> <p>DRM客戶端使用的檔案已意外修改。 <span class="codeph"> subErrorId</span> 包含特定於客戶端或行的錯誤。 </p> 
    <ul id="ul_860D2402DA61460AB0D938F1116F6D64"> 
     <li id="li_CF368C43452B4265B62ADA3E223894BA">配銷商的軟體應再次重試該操作，因為AdobeCP已在內部刪除了違規的伺服器存放區，且應成功重試。 如果重試失敗，請記錄問題。 </li> 
     <li id="li_51A5803A1F754970BB4EBD6494F5DC96">如果重試失敗的速率高於用戶群中硬碟的預期失敗率，請將問題呈報至Adobe。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3326 </td> 
   <td colname="col2"><span class="codeph"> AAXS_StorePharketingDetected  </span> </td> 
   <td colname="col3"> 調用<span class="codeph"> DRMManager.resetDRM</span>。 <p>授權存放區已遭竄改／損毀，無法再使用。 </p> <p>配銷商的軟體應以3322所述的相同方式引導使用者重設。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3327 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClockHappertingDetected  </span> </td> 
   <td colname="col3"> 修正時鐘或再次獲取<span class="codeph"> Authn/Lic/Domain</span>許可證。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>驗證／授權／網域伺服器錯誤</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3328 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerErrorTryAgain  </span> </td> 
   <td colname="col3"> <p>這是伺服器端錯誤，伺服器無法從用戶端完成請求。 例如，當伺服器忙、HTTP/500、伺服器沒有解密請求所需的密鑰等時，可能會發生此錯誤。 </p> <p>在客戶端上，沒有辦法確定出了什麼問題。 客戶必須檢閱Adobe存取伺服器記錄檔（通常稱為<span class="codeph"> AdobeFlashAccess.log</span>），以判斷出錯之處。 記錄檔中始終有描述性的堆疊追蹤，以指出問題。 <span class="codeph"> subErrorId</span> 包含伺服器特定或行錯誤。 </p> <p>配銷商應查看伺服器記錄，以識別是哪個伺服器傳送此錯誤。 對於具有子錯誤代碼101的3328錯誤，伺服器無法解密請求。 客戶必須驗證安裝在許可證伺服器上的許可證／傳輸伺服器證書是否與打包期間使用的證書匹配並對應。 </p> <p>此外，如果客戶使用「參考實作」，則必須確保<span class="codeph"> flashaccess-refimpl.properties</span>檔案中沒有字型錯誤，而指定了主要和其他憑證。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3329 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ApplicationSpecificError  </span> </td> 
   <td colname="col3"> <p>Flash Access時不會知道應用程式特定的子錯誤碼。 <span class="codeph"> subErrorId</span> 包含來自發佈者自訂授權伺服器的伺服器特定錯誤。伺服器在應用程式特定的命名空間中傳回錯誤。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三三零 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NeedAuthentication  </span> </td> 
   <td colname="col3"> <p>當內容設定為要求用戶端在取得授權之前進行驗證時，就會發生此錯誤。 </p> 
    <ul id="ul_712D29B8B5A6401FB014C4A283918E32"> 
     <li id="li_2D56905EB50D4FDEAD69CA8EAE38AD1A">配銷商的軟體應驗證使用者，然後再次取得授權。 <p>如果您的服務不想使用驗證，請記錄造成此錯誤的內容的識別碼。 </p> </li> 
     <li id="li_B3BCF899B8BE41C7A4F7CF84B0503483">此錯誤不應需要呈報，除非內容不應設定為需要驗證。 <p>在這種情況下，請使用適當的原則重新封裝違規內容。 如果內容封裝正確，請參閱診斷原則／授權差異。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>上述未涵蓋的授權實施錯誤</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
</tr> 
  <tr> 
   <td colname="col1"> 郵編：3331 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentNotYetValid  </span> </td> 
   <td colname="col3"> <p>取得的授權尚無效。 要解決此問題，請檢查客戶機時鐘設定是否正確。 要設定客戶端時鐘，請重新打包內容或修改許可證伺服器配置。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三三二年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CachedLicenseExpired  </span> </td> 
   <td colname="col3"> 從伺服器重新取得授權。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3333 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PlaybackWindowExpired  </span> </td> 
   <td colname="col3"> <p>您必須通知使用者，在原則到期之前，他們無法播放此內容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三三四年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMPlatform  </span> </td> 
   <td colname="col3"> <p>此平台不允許播放內容，因為例如，內容提供者已設定「Adobe存取」，以拒絕平台上的「Adobe存取」內容，或共用網域系結授權系結至用於不同分區的共用網域Token。 </p> <p>如果內容未使用適當的（CDM功能選定）封裝器認證來封裝，CDM可能會擲出此錯誤。 </p> <p>如果內容封裝有不正確的PHDS/PHLS憑證，則內容可能適用於Chrome，但不適用於其他瀏覽器（反之亦然）。 <p>提示： 這是因為Chrome使用不同的PHDS/PHLS憑證。 </p>若要確認正在使用哪個憑證，請轉儲內容中繼資料的詳細資料，並尋找<i>收件者憑證</i>。 如需詳細資訊，請參閱<a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三三五年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMVersion  </span> </td> 
   <td colname="col3"> 升級至Android專用的TVSDK最新版本。 <p>要解決此問題，請完成以下任務之一： 
     <ul id="ul_BF1742948BC9461CB8686DE70124D3CD"> 
      <li id="li_690D440C94CC45A0AE55EC319B1C4C23">升級AIR </li> 
      <li id="li_CDD20251C881466E88BE7BBB53D61EBC">若為Flash Player，請升級AdobeCP模組並重試播放。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3336 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidRuntimePlatform  </span> </td> 
   <td colname="col3"> <p>此平台不允許播放內容，因為例如，內容提供者已設定「存取」，以拒絕平台上FP/AIR的內容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三三七 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidRuntimeVersion  </span> </td> 
   <td colname="col3"> 升級至Android專用的最新版TVSDK。 <p>如果內容或伺服器設定為拒絕播放特定版本的Flash或AIR執行階段，就會發生此情況。 </p> 
    <ul id="ul_B0732D941256483CABBDD30C9BF43249"> 
     <li id="li_72782B1D638F48C0B87084689FB9C798">如果使用者使用可升級Flash的作業系統，配銷商軟體應提示使用者升級Flash，然後再試一次。 否則，建議使用者使用不同的機器。 </li> 
     <li id="li_1E3FD93CE39E43F2B7D961299B1211DA">如果懷疑有錯誤3337s，請識別是否發生在特定內容上，並重新封裝該內容。 如果正確封裝內容，請參閱診斷原則／授權差異 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3338 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnknownConnectionType  </span> </td> 
   <td colname="col3"> <p>無法檢測連接類型，策略要求您開啟「輸出保護」。 只有當內容封裝為需要數位或模擬輸出保護時，才會出現此問題。 </p> <p>11.8.800.168版以前的Flash Player版本中發生問題，導致錯誤3338偶爾發生在原則指出內容保護為<span class="codeph"> USE IF AVAILABLE</span>的內容上。 此問題已在11.8.800.168版及更新版本中修正。 </p> 
    <ul id="ul_4B6CA26A53F84838B5B95400925464D4"> 
     <li id="li_CBD890F467E449EBB5116E1561252058">配銷商的軟體選擇不需要輸出保護的內容變體（例如HD串流的SD變體）。 <p>如果<span class="codeph"> USE_IF_AVAILABLE </span>內容發生錯誤3338，請檢查播放器版本號。 如果播放器版本低於11.8.800.168，建議使用者升級Flash Player。 如果錯誤3338發生在11.8.800.168以上的版本上，請記錄導致錯誤的內容。 </p> </li> 
     <li id="li_62886C1D96264B129928A7E29E6C70E1">配銷商應檢查哪些內容造成此錯誤，並驗證內容的策略是將模擬和數字輸出設定為<span class="codeph"> NO_PROTECTION</span>或<span class="codeph"> USE_IF_AVAILABLE</span>。 <p>如果內容不慎與<span class="codeph"> NO_OUTPUT</span>或<span class="codeph"> REQUIRED</span>一起封裝，請重新封裝內容。 如果正確封裝內容，請參閱診斷原則／授權差異。 否則呈報至Adobe。 </p> </li> 
    </ul> <p>如需詳細資訊，請參閱<a href="https://forums.adobe.com/message/5518688" format="https" scope="external">當您的DRM原則設為USE_IF_AVAILABLE時，取得非預期的3338錯誤？</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3339 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogPlaybackAllowed  </span> </td> 
   <td colname="col3"> 無法在模擬設備上播放。 若要解決此問題，請連接數位裝置。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三四零年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogProtectionAvail  </span> </td> 
   <td colname="col3"> 無法播放內容，因為連接的模擬外部顯示設備（顯示器／電視）沒有正確的功能（例如，設備沒有Macrovision或ACP）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三四一年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalPlaybackAllowed  </span> </td> 
   <td colname="col3"> 無法在數位裝置上播放內容。 <p>重要： 此問題不應發生在生產環境中，因為內容發佈者不應禁止數位播放。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三四二年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalProtectionAvail  </span> </td> 
   <td colname="col3"> 連接的數字外部顯示設備（顯示器／電視）沒有正確的功能。 例如，設備沒有HDCP。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三四三年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IntegrityVerificationFailed  </span> </td> 
   <td colname="col3"> <p>不適用於Android。 </p> <p>此錯誤目前已知會在發行新版Flash後最初發生。 之所以發生此情況，是因為Flash在Flash開啟時升級，使Flash處於不良狀態，直到瀏覽器重新啟動為止。 </p> 
    <ul id="ul_A0AC4A77550E40409A04BD33748EA987"> 
     <li id="li_F41C1ABD838D41ABB0DF65093E664A29">配銷商軟體應完成下列工作： 
      <ul id="ul_79B2AB1372074D448F129851AA24F985"> 
       <li id="li_B93EDD263D78434FAF198A01938D3508">建議使用者關閉或結束所有瀏覽器，然後重新開啟。 </li> 
       <li id="li_ADFBCFA66AD849E18DB390455458528E">檢查Flash版本是否為最新版本。 <p>如果版本不是最新版本，建議客戶升級、關閉其瀏覽器中的所有標籤，然後重新開啟。 </p> </li> 
      </ul> </li> 
     <li id="li_281B54582B5949AEA7D166246917EE41">如果瀏覽器重新啟動成功後發生錯誤，請呈報至Adobe。 <p>當新版本發行時，我們建議您連絡Adobe支援以查看背景更新問題是否已修正。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三四四年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MissingAdobeCPModule  </span> </td> 
   <td colname="col3"> 不適用於Android。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三四五年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DRMNoAccessError  </span> </td> 
   <td colname="col3"> <p>不適用於Android。 </p> <p>當部分Flash或AIR未正確安裝時，會發生此錯誤。 </p> <p>配銷商軟體應執行下列其中一項作業： 
     <ul id="ul_D1188E2D4FDF4BD89A04F5629D75D981"> 
      <li id="li_B33FBCA5D4534D668B86A5E93DB3A809">要求使用者解除安裝並重新安裝AIR。 </li> 
      <li id="li_B7D2388E9FA84C26AF1C87B48AF9EF16">對於Flash Player，請調用<span class="codeph"> System.update</span>。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三四六年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MigrationFailed  </span> </td> 
   <td colname="col3"> 
    <ul id="ul_518AD4931CC64EB3A962DD451E6C5067"> 
     <li id="li_3C44F0740B08490E9C62D89C40B57DC2">配銷商軟體應執行下列其中一項作業： 
      <ul id="ul_7D90526684BF4EB2BBADCF598AA13086"> 
       <li id="li_D15B4BEDAF7340F6B9BC886DF6E346EC">如果是AIR，請呼叫<span class="codeph"> DRMManager.resetDRMVouchers()</span> </li> 
       <li id="li_40A51D35408249CFA28DBC49FDA3408B">如果Flash因錯誤3322或3346錯誤代碼而無法使用，使用者應前往<a href="https://forums.adobe.com/message/5535907#5535907" format="http" scope="external"> https://forums.adobe.com/message/5535907#5535907</a>並依照Adobe文章的指示，以程式設計方式重設其DRM授權儲存區。 </li> 
      </ul> </li> 
     <li id="li_0464471E4A094C80BF2986694341921A">如果此錯誤經常發生，配銷商應提供頻率播放器版本和瀏覽器版本的詳細資訊以供Adobe。 </li> 
    </ul> <p>如需詳細資訊，請參閱下列論壇文章： 
     <ul id="ul_44E0077FEAA749CC9549BF3846065304"> 
      <li id="li_2BE3B2443380415DA73B7AA3B6547B31"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> Chrome中的DRM錯誤3322/3346/3368（資訊列問題）</a> </li> 
      <li id="li_4E5C7414756644E1AB78BE7B8112228C"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> 硬體變更後出現3322或3346錯誤</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三四七年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IndeficDeviceCapability  </span> </td> 
   <td colname="col3"> <p>此錯誤的主要含義是授權有用戶端的DRM憑證指出其無法滿足的限制。 下列「硬體功能」是在發出用戶端DRM憑證時定義的： 
     <ul id="ul_1EB6F1469C244CF0BA52C212495C053D"> 
      <li id="li_646043CE045C4DE2BBC939E1F4963DFE"><b>非用戶可訪問匯流排</b>。如果<b>true</b>，解密的媒體絕不會流過匯流排或進入應用程式可以訪問該匯流排的主記憶體。 <p>如果<b>false</b>，則在解密後，應用程式可能會存取內容。 </p> </li> 
      <li id="li_02AAECAF4D35447BA10554541B46DE67"><b>硬體信任根</b>。如果<b>true</b>，則在啟動時在設備上載入的所有軟體都將通過僅在硬體中提供的密鑰或摘要進行驗證。 <p>當針對用戶端的DRM憑證開啟授權時，這兩個限制都會在用戶端進行檢查，而且立即發生故障。 在核發授權之前，您也可以在伺服器端檢查這些限制。 </p> </li> 
     </ul> </p> <p>此錯誤的次要含義是授權已設定「Jailbreak Enforcement」（越獄執行）政策，且裝置上已偵測到越獄。 此檢查會在用戶端定期執行，且無法在伺服器端進行檢查。 </p> <p>配銷商可以更新政策並移除限制。 對於設備功能策略，請使用<span class="codeph"> -devCapabilitiesV1</span>標誌發出策略更新命令，而不使用參數。 對於越獄強制，請設定<span class="codeph"> policy.enforceJailbreak=false</span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三四八年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_HardStopIntervalExpired  </span> </td> 
   <td colname="col3"> 硬停止間隔已過期。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三四九年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionTooHigh  </span> </td> 
   <td colname="col3"> 伺服器運行的版本高於客戶端支援的最高版本。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三五零 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionTooLow  </span> </td> 
   <td colname="col3"> 伺服器的執行版本低於用戶端支援的最低版本。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3351 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenInvalid  </span> </td> 
   <td colname="col3"> 網域Token無效。 若要解決此問題，請再次向網域註冊。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三五二年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenTooOld  </span> </td> 
   <td colname="col3"> 網域Token比授權所需的Token舊。 若要解決此問題，請再次向網域註冊。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三五三年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenTooNew  </span> </td> 
   <td colname="col3"> 網域Token比授權所需的Token新。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三五四年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenExpired  </span> </td> 
   <td colname="col3"> 網域Token已過期。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三五五年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainJoinFailed  </span> </td> 
   <td colname="col3"> 域連接失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3356 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoEncorpedRoot  </span> </td> 
   <td colname="col3"> 找不到V3葉片許可證的根許可證。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三五七年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoValidEmbeddedLicense  </span> </td> 
   <td colname="col3"> 未找到有效的嵌入式許可證。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三五八年 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoACPProtectionAvail  </span> </td> 
   <td colname="col3"> 由於連接的模擬設備沒有ACP保護，因此無法回放。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3359 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoCGMSAProtectionAvail  </span> </td> 
   <td colname="col3"> 由於連接的模擬設備沒有CGMS-A保護，因此無法播放。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三六零 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainRegistrationRequired  </span> </td> 
   <td colname="col3"> 內容需要網域註冊。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3361 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NotRegisteredToDomain  </span> </td> 
   <td colname="col3"> 電腦未註冊到指定元資料的域。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3362 </td> 
   <td colname="col2"><span class="codeph"> AAXS_OperationTimeoutError  </span> </td> 
   <td colname="col3"> 非同步操作所花費的時間超過<span class="codeph"> maxOperationTimeout</span>。 僅由iOS DRMNative Framework傳回。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3363 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnsupportedIOSPlaylistError  </span> </td> 
   <td colname="col3"> 傳入的M3U8播放清單含有不支援的內容。 僅由iOS DRMNative Framework傳回。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3364 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDeviceId  </span> </td> 
   <td colname="col3"> <p>框架請求設備ID，但返回的值為空。 </p> <p>使用者不應在Chrome設定中選取「允許保護內容的識別碼</span>」核取方塊。<span class="uicontrol"> </span></p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3365 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncognitoModeNotAllowed  </span> </td> 
   <td colname="col3"> <p>此瀏覽器／平台組合不允許在Incognito模式下播放受DRM保護的內容。 </p> <p>配銷商的軟體應建議使用者退出Incognito模式或使用不同的瀏覽器。 如需詳細資訊，請參閱<a href="https://forums.adobe.com/thread/1266622" format="https" scope="external"> DRM錯誤3365原因與解析度</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3366 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadParameter  </span> </td> 
   <td colname="col3"> <p>主機執行時期會以錯誤的參數呼叫存取程式庫。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3367 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadSignature  </span> </td> 
   <td colname="col3"> m3u8資訊清單簽署失敗。 僅由iOS DRMNative Framework或AVE傳回。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3368 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UserSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>用戶取消了操作或輸入了不允許訪問系統的設定。 </p> <p>只有當SWF版本為19或更新版本時，才會擲回此錯誤。 為了向後相容，當SWF為18版或更舊版本時，會擲出3321。 </p> <p>配銷商的軟體應引導使用者說明如何允許無沙盒外掛程式存取。 如需詳細資訊，請參閱Chrome中<a href="https://helpx.adobe.com/adobe-access/kb/error-3321.html" format="html" scope="external"> Google Chrome的無沙盒存取被拒絕</a>和<a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> DRM錯誤3322/3346/3368（資訊列問題）</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3369 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InterfaceNotAvailable</span> </td> 
   <td colname="col3"> <p>不提供所需的瀏覽器介面。 此問題僅發生在Pepper上。 Flash外掛程式和瀏覽器版本可能不相符。 </p> <p>散發者的軟體應引導使用者確保已安裝最新版本的瀏覽器。 </p> <p> 如果此錯誤的發生率增加，且與已發佈的瀏覽器更新相對應，則呈報為Adobe。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 三三七零 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentIdSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>用戶已禁用<span class="uicontrol">允許受保護內容的標識符設定。</span> </p> <p>提示： Pepper 13.0.0.x版或更新版本會出現此錯誤。 </p> <p>配銷商的軟體應引導使用者啟用「允許保護內容識別碼</span>」設定。<span class="uicontrol"> </span></p> <p>配銷商的營運團隊應引導使用者啟用「允許保護內容識別碼</span>」設定。<span class="uicontrol"> </span></p> <p>如需詳細資訊，請參閱<a href="https://forums.adobe.com/message/6518323#6518323" format="https" scope="external"> https://forums.adobe.com/message/6518323#6518323</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3371 </td> 
   <td colname="col2"><span class="codeph"> AAXS_</span><span class="codeph"> NoOPConstraintInPixelConstraints</span> </td> 
   <td colname="col3"> <p>基於許可證中輸出保護約束的格式錯誤的解析。 </p> <p>配銷商的軟體應顯示錯誤訊息。 要求使用者以內容標題向配銷商報告問題。 </p> <p>配銷商應以有效政策重新封裝內容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3372 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ResolutionLagerThanMaxResolution</span> </td> 
   <td colname="col3"> <p>內容的解析度大於輸出保護約束中指定的最大解析度。 </p> <p>如果授權代理商的營運團隊在記錄中發現此錯誤，則應檢閱以解析度為基礎的輸出保護政策，並視需要重新封裝內容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3373 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_DisplayResolutionLagerThanConstrain</span> </td> 
   <td colname="col3"> <p>內容的解析度大於當前活動的輸出保護約束所指定的解析度。 </p> <p>如果授權代理商的營運團隊在記錄中發現此錯誤，則應檢閱以解析度為基礎的輸出保護政策，並視需要重新封裝內容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 郵編：3374 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_ClientCommProcessFailed</span> </td> 
   <td colname="col3"> <p>在用戶端通訊處理期間失敗，例如請求產生、回應處理、錯誤驗證Token等。 </p> <p>如果授權代理商的營運團隊在記錄中發現此錯誤，則應檢閱以解析度為基礎的輸出保護政策，並視需要重新封裝內容。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR:視訊播放值{#section_7079501250C2487499639F92EC774525}

AVE的Video Encoder介面會在`NATIVE_ERROR`中繼資料物件中傳回這些視訊播放通知。

<table id="table_5EEB1F60E5854452A8B0BABBE9B32651"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>NATIVE_ERROR_CODE元資料鍵的值</b></th> 
   <th colname="col2" class="entry"><b>NATIVE_ERROR_NAME元資料鍵的值</b></th> 
   <th colname="col3" class="entry"><b>說明</b></th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> -1 </td> 
   <td colname="col2"><span class="codeph"> END_OF_PERIOD</span> </td> 
   <td colname="col3"> 句號結束。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 0 </td> 
   <td colname="col2"><span class="codeph"> 成功</span> </td> 
   <td colname="col3"> 操作成功。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 1 </td> 
   <td colname="col2"> <span class="codeph"> ASYNC_OPERATION_IN_PROGRESS</span> </td> 
   <td colname="col3"> 非同步操作。 已發出操作請求。 成功／失敗資訊將於稍後提供。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 2 </td> 
   <td colname="col2"><span class="codeph"> EOF</span> </td> 
   <td colname="col3"> 由於檔案結束(EOF)條件，無法操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3 </td> 
   <td colname="col2"><span class="codeph"> 解碼器失敗</span> </td> 
   <td colname="col3"> 解碼器在執行時期失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 4 </td> 
   <td colname="col2"><span class="codeph"> DEVICE_OPEN_ERROR</span> </td> 
   <td colname="col3"> 無法開啟硬體解碼器。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 5 </td> 
   <td colname="col2"><span class="codeph"> FILE_NOT_FOUND  </span> </td> 
   <td colname="col3"> 找不到資源。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 6 </td> 
   <td colname="col2"><span class="codeph"> GENERIC_ERROR  </span> </td> 
   <td colname="col3"> 一般錯誤。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 7 </td> 
   <td colname="col2"><span class="codeph"> 不可恢復錯誤  </span> </td> 
   <td colname="col3"> 視訊引擎無法從中復原的錯誤狀況。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 8 </td> 
   <td colname="col2"><span class="codeph"> LOST_CONNECTION_RESCOVERABLE  </span> </td> 
   <td colname="col3"> 網路錯誤，正在嘗試恢復。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 9 </td> 
   <td colname="col2"><span class="codeph"> NO_FIXED_SIZE  </span> </td> 
   <td colname="col3"> 無法確定資源的大小。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 10 </td> 
   <td colname="col2"><span class="codeph"> NOT_IMPLEMENTED  </span> </td> 
   <td colname="col3"> 功能未實作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 11 </td> 
   <td colname="col2"><span class="codeph"> 記憶體不足  </span> </td> 
   <td colname="col3"> 記憶體不足。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 12 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR  </span> </td> 
   <td colname="col3"> 解析媒體檔案時出錯。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 13 </td> 
   <td colname="col2"><span class="codeph"> SIZE_UNKNOWN  </span> </td> 
   <td colname="col3"> 資源有大小，但未知。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 14 </td> 
   <td colname="col2"><span class="codeph"> UNDER_FLOW  </span> </td> 
   <td colname="col3"> 底流。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 15 </td> 
   <td colname="col2"><span class="codeph"> 不支援的組態  </span> </td> 
   <td colname="col3"> 不支援設定。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 16 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_OPERATION  </span> </td> 
   <td colname="col3"> 不支援操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 17 </td> 
   <td colname="col2"><span class="codeph"> WAITING_FOR_INIT  </span> </td> 
   <td colname="col3"> 尚未初始化。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 18 </td> 
   <td colname="col2"><span class="codeph"> INVALID_PARAMETER  </span> </td> 
   <td colname="col3"> 參數無效。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 19 </td> 
   <td colname="col2"><span class="codeph"> INVALID_OPERATION</span> </td> 
   <td colname="col3"> 不允許操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 20 </td> 
   <td colname="col2"><span class="codeph"> OP_ONLY_ALLOWED_IN_PAUSED_STATE</span> </td> 
   <td colname="col3"> 只有暫停時，才允許該操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 21 </td> 
   <td colname="col2"><span class="codeph"> OP_INVALID_WITH_AUDIO_ONLY_FILE</span> </td> 
   <td colname="col3"> 操作不能用於僅音頻檔案。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 22 </td> 
   <td colname="col2"><span class="codeph"> PREVIOUS_STEP_SEEK_IN_PROGRESS</span> </td> 
   <td colname="col3"> 以前的搜索操作仍在進行中。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 23 </td> 
   <td colname="col2"><span class="codeph"> SOURCE_NOT_SPECIFIED  </span> </td> 
   <td colname="col3"> 未指定資源。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 24 </td> 
   <td colname="col2"><span class="codeph"> RANGE_ERROR</span> </td> 
   <td colname="col3"> 指定的值超出範圍。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 25 </td> 
   <td colname="col2"><span class="codeph"> INVALID_SEEK_TIME</span> </td> 
   <td colname="col3"> 無效的尋道時間。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 26 </td> 
   <td colname="col2"><span class="codeph"> FILE_STRUCTURE_INVALID</span> </td> 
   <td colname="col3"> 指定的檔案不符合預期語法。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 27 </td> 
   <td colname="col2"><span class="codeph"> COMPONENT_CREATION_FAILURE</span> </td> 
   <td colname="col3"> 無法建立基本元件。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 28 </td> 
   <td colname="col2"><span class="codeph"> DRM_INIT_ERROR</span> </td> 
   <td colname="col3"> 無法建立DRM上下文。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 29 </td> 
   <td colname="col2"><span class="codeph"> CONTAINER_NOT_SUPPORTED  </span> </td> 
   <td colname="col3"> 不支援容器類型。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 30 </td> 
   <td colname="col2"><span class="codeph"> SEEK_FAILED</span> </td> 
   <td colname="col3"> 搜索失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 31 </td> 
   <td colname="col2"><span class="codeph"> CODEC_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> 不支援的轉碼器。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 32 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_UNAVAILABLE</span> </td> 
   <td colname="col3"> 網路不可用。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 33 </td> 
   <td colname="col2"><span class="codeph"> 網路錯誤</span> </td> 
   <td colname="col3"> 從網路獲取資料時出錯。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 34 </td> 
   <td colname="col2"><span class="codeph"> 溢位</span> </td> 
   <td colname="col3"> 溢位。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 35 </td> 
   <td colname="col2"><span class="codeph"> VIDEO_PROFILE_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> 不支援的視訊設定檔。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 36 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_NOT_LOADED</span> </td> 
   <td colname="col3"> 嘗試對HOLD期間或尚未載入的期間執行操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 37 </td> 
   <td colname="col2"><span class="codeph"> INVALID_REPLACE_DURATION</span> </td> 
   <td colname="col3"> 指定的替換持續時間無效或延長到串流結尾。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 38 </td> 
   <td colname="col2"><span class="codeph"> 調用自錯誤線程</span> </td> 
   <td colname="col3"> 無法從錯誤的執行緒呼叫API。 主要是應從主執行緒呼叫的API元素。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 39 </td> 
   <td colname="col2"><span class="codeph"> FRAGMENT_READ_ERROR</span> </td> 
   <td colname="col3"> 片段讀取錯誤。 沒有故障切換。 引擎將嘗試讀取下一個片段。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 40 </td> 
   <td colname="col2"><span class="codeph"> 中止</span> </td> 
   <td colname="col3"> 此操作由明確的中止或銷毀調用中止。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 41 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_HLS_VERSION</span> </td> 
   <td colname="col3"> 無法播放此版本的HLS介質。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 42 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_FAIL_OVER</span> </td> 
   <td colname="col3"> 不能故障切換。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 43 </td> 
   <td colname="col2"><span class="codeph"> HTTP_TIME_OUT</span> </td> 
   <td colname="col3"> HTTP下載已逾時。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 44 </td> 
   <td colname="col2"><span class="codeph"> 網路關閉  </span> </td> 
   <td colname="col3"> 用戶的網路連接已關閉。 播放可能隨時停止，並會在連接可用時繼續。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 45 </td> 
   <td colname="col2"><span class="codeph"> NO_USABLE_BITRATE_PROFILE</span> </td> 
   <td colname="col3"> 在串流中找不到可用位速率描述檔。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 46 </td> 
   <td colname="col2"><span class="codeph"> BAD_MANIFEST_SIGNATURE</span> </td> 
   <td colname="col3"> 資訊清單的簽名不好。 它未通過資訊清單簽署測試。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 47 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_LOAD_PLAYLIST</span> </td> 
   <td colname="col3"> 無法載入播放清單。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 48 </td> 
   <td colname="col2"><span class="codeph"> REPLACEMENT_FAILED</span> </td> 
   <td colname="col3"> 無法成功取代在「插入API」中指定的項目。 這表示插入成功，但替換未成功。 如果要更換的資訊清單已從時間軸移除，則更換可能會失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 49 </td> 
   <td colname="col2"><span class="codeph"> SWITCH_TO_ANSYMETRIC_PROFILE</span> </td> 
   <td colname="col3"> DRM正在切換到非對稱配置檔案。 所有描述檔都預期會在持續時間內對齊。 如果沒有，則會擲出此警告，且播放中可能會出現跳轉。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 50 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_BACKWARD</span> </td> 
   <td colname="col3"> 即時視窗只會向前移動。 否則，將拋出此警告，並且不會讀取窗口。 因此，播放中可能會出現跳轉（或停止／長暫停）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 51 </td> 
   <td colname="col2"><span class="codeph"> CURRENT_PERIOD_EXPIRED</span> </td> 
   <td colname="col3"> 即時視窗會移至目前時段以外的位置。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 52 </td> 
   <td colname="col2"><span class="codeph"> CONTENT_LENGTH_MISMATCH</span> </td> 
   <td colname="col3"> HTTP伺服器報告的內容長度不符合實際的媒體大小。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 53 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_HOLD</span> </td> 
   <td colname="col3"> 媒體讀取器無法進一步讀取，因為它已達到setHoldAt API設定的時間。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 54 </td> 
   <td colname="col2"><span class="codeph"> LIVE_HOLD  </span> </td> 
   <td colname="col3">媒體閱讀器無法載入區段，因為它已到達即時視窗的尾端。 當伺服器將新媒體廣告至即時視窗時，區段載入將會繼續。 在下列情況下，通常會到達此狀態： 
    <ul id="ul_FCFF658EDA4144E59970B317D6DEB624"> 
     <li id="li_2F6EEEB782D54CD999BC7CC7C0B78B48"><span class="codeph"> bufferTime</span>太高（等於或高於即時窗口持續時間）。 </li> 
     <li id="li_25CE97115ED64E44AA89977FB5F0DCF7">一個或多個插入／擦除API的組合取代了添加的多個介質。 </li> 
     <li id="li_1B14716B2157492AB1859306D1250523">下一時段是有待更換媒體的即時時段（由於InsertBy API呼叫） </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 55 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_INTERLANG  </span> </td> 
   <td colname="col3"> 媒體中的音訊和視訊交錯無法正確執行。 這是封裝錯誤。 當差異超過兩秒時，就會發出警告。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 56 </td> 
   <td colname="col2"><span class="codeph"> DRM_NOT_AVAILABLE</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 57 </td> 
   <td colname="col2"><span class="codeph"> PLAYBACK_NOT_AUTHORIZED</span> </td> 
   <td colname="col3"> 未在Flash Player中啟用HLS回放。 請參閱AuthorizedFeatures.enableHLSPlayback。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 58 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_SAMPLE_FOUND</span> </td> 
   <td colname="col3"> 解碼器接收到不能解碼的壞樣本。 這通常不是致命錯誤，但表示音訊／視訊中可能有故障。 此錯誤的例項過多表示編碼錯誤或檔案錯誤。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 59 </td> 
   <td colname="col2"><span class="codeph"> RANGE_SPANS_READ_HEAD</span> </td> 
   <td colname="col3"> 開始播放後，「插入／取代」範圍不應包含讀取頭。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 60 </td> 
   <td colname="col2"><span class="codeph"> POSTROLL_WITH_LIVE_NOT_ALLOWED</span> </td> 
   <td colname="col3"> 即時媒體上不允許插入滾動後內容。 但是，當伺服器將介質標籤為完整後，才允許使用。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 61 </td> 
   <td colname="col2"><span class="codeph"> 內部錯誤</span> </td> 
   <td colname="col3"> 這是一個非常罕見的問題，永遠不會發生。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 62 </td> 
   <td colname="col2"><span class="codeph"> SPS_PPS_FOUND_OUTSIDE_AVCC</span> </td> 
   <td colname="col3"> 此串流不遵循一律將H264 SPS/PPS放入AVCC的封裝建議。 可能會看到搜尋／播放問題。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 63 </td> 
   <td colname="col2"><span class="codeph"> PARTIAL_REPLACEMENT</span> </td> 
   <td colname="col3"> 在「插入API」中指定的取代僅完成部分。 當replaceDuration跨越時間軸持續時間時，就會發生此情況。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 64 </td> 
   <td colname="col2"><span class="codeph"> RENDITION_M3U8_ERROR</span> </td> 
   <td colname="col3"> 轉譯播放清單載入時發生錯誤。 這僅適用於AVE，不適用於FlashPlayer。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 65 </td> 
   <td colname="col2"><span class="codeph"> NULL_OPERATION</span> </td> 
   <td colname="col3"> 操作不執行任何操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 66 </td> 
   <td colname="col2"><span class="codeph"> SEGMENT_KLIPPED_ON_FAILURE</span> </td> 
   <td colname="col3"> 區段無法播放，且會在失敗時略過。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 67 </td> 
   <td colname="col2"><span class="codeph"> INCOMPLATED_RENDER_MODE</span> </td> 
   <td colname="col3"> 不相容的演算模式。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 68 </td> 
   <td colname="col2"><span class="codeph"> PROTOCOL_NOT_SUPPORTED  </span> </td> 
   <td colname="col3"> 不支援URL中使用的Web通訊協定。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 69 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR_INCOMPLATIVE_VERSION</span> </td> 
   <td colname="col3"> 解析媒體檔案時出錯。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 70 </td> 
   <td colname="col2"><span class="codeph"> MANIFEST_FILE_UPPORTED_CHANGED</span> </td> 
   <td colname="col3"> 資訊清單檔案以非預期的方式變更。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 71 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_SPLIT_TIMELINE</span> </td> 
   <td colname="col3"> 無法對時間軸執行拆分操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 72 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_ERASE_TIMELINE</span> </td> 
   <td colname="col3"> 無法對時間軸執行拭除操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 73 </td> 
   <td colname="col2"><span class="codeph"> DID_NOT_GET_NEXT_FRAGMENT</span> </td> 
   <td colname="col3"> 沒有找到下一個片段。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 74 </td> 
   <td colname="col2"><span class="codeph"> NO_TIMELINE</span> </td> 
   <td colname="col3"> 內部資料結構中沒有時間軸。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 75 </td> 
   <td colname="col2"><span class="codeph"> LISTENER_NOT_FOUND</span> </td> 
   <td colname="col3"> 在內部資料結構中未找到偵聽器。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 76 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_START_ERROR</span> </td> 
   <td colname="col3"> 無法啟動音頻。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 77 </td> 
   <td colname="col2"><span class="codeph"> NO_AUDIO_SINK</span> </td> 
   <td colname="col3"> 內部資料結構中沒有音頻接收器。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 58 </td> 
   <td colname="col2"><span class="codeph"> FILE_OPEN_ERROR</span> </td> 
   <td colname="col3"> 無法開啟檔案。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 79 </td> 
   <td colname="col2"><span class="codeph"> FILE_WRITE_ERROR</span> </td> 
   <td colname="col3"> 無法寫入檔案。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 80 </td> 
   <td colname="col2"><span class="codeph"> FILE_READ_ERROR</span> </td> 
   <td colname="col3"> 無法從檔案讀取。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 61 </td> 
   <td colname="col2"><span class="codeph"> ID3PARSE_ERROR</span> </td> 
   <td colname="col3"> 剖析ID3資料時發生錯誤。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 82 </td> 
   <td colname="col2"><span class="codeph"> SECURITY_ERROR  </span> </td> 
   <td colname="col3"> 由於安全性限制，載入內容失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 83 </td> 
   <td colname="col2"><span class="codeph"> 時間軸——太短</span> </td> 
   <td colname="col3"> 時間軸持續時間太短。 如果這是即時串流，則可能會發生頻繁的緩衝。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 84 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_START</span> </td> 
   <td colname="col3"> 該串流已切換為僅限音訊的串流。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 85 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_END</span> </td> 
   <td colname="col3"> 該串流已從純音效切換為含視訊的串流。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 87 </td> 
   <td colname="col2"><span class="codeph"> KEY_NOT_FOUND  </span> </td> 
   <td colname="col3"> 找不到密鑰。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 88 </td> 
   <td colname="col2"><span class="codeph"> INVALID_KEY</span> </td> 
   <td colname="col3"> 密鑰無效。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 89 </td> 
   <td colname="col2"> <span class="codeph"> KEY_SERVER_NOT_FOUND</span> </td> 
   <td colname="col3"> 密鑰伺服器不返回密鑰。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 90 </td> 
   <td colname="col2"> <span class="codeph"> MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</span> </td> 
   <td colname="col3"> 無法處理主資訊清單更新。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 91 </td> 
   <td colname="col2"> <span class="codeph"> UNJERVED_TIME_DINSTRUCTION_FOUND</span> </td> 
   <td colname="col3"> 發現未報告的時間不連續性。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 92 </td> 
   <td colname="col2"> <span class="codeph"> UNMATCHED_AV_DINSTRUCTION_FOUND</span> </td> 
   <td colname="col3"> 發現音訊和視訊不連續。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 93 </td> 
   <td colname="col2"><span class="codeph"> TRICKPLAY_ENDED_DUE_TO_ERROR</span> </td> 
   <td colname="col3">在<i>特技播放</i>模式中播放媒體時發生錯誤。 特技播放模式已結束，而串流已暫停。 呼叫<span class="codeph"> Play()</span>以正常模式播放媒體。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 95 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_AHEAD</span> </td> 
   <td colname="col3"> 玩家已離開即時視窗，必須向前追趕。 </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR:加密值{#section_39365E545CAC49B9A4D4678657BB2155}

Adobe視頻引擎的加密模組在`NATIVE_ERROR`元資料對象中返回這些通知。

| **NATIVE_ERROR_CODE元資料鍵的值** | **NATIVE_ERROR_NAME元資料鍵的值** | **意義** |
|---|---|---|
| 300 | `CRYPTO_ALGORITHM_NOT_SUPPORTED` | 不支援使用的演算法。 |
| 301 | `CRYPTO_ERROR_CORRUPTED_DATA` | 資料已損毀。 |
| 302 | `CRYPTO_ERROR_BUFFER_TOO_SMALL` | 緩衝區太小。 |
| 303 | `CRYPTO_ERROR_BAD_CERTIFICATE` | 憑證錯誤。 |
| 304 | `CRYPTO_ERROR_DIGEST_UPDATE` | 摘要更新。 |
| 305 | `CRYPTO_ERROR_DIGEST_FINISH` | 摘要完成。 |
| 306 | `CRYPTO_ERROR_BAD_PARAMETER` | 參數錯誤。 |
