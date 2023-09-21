---
title: NATIVE_ERROR通知的詳細資料
description: NATIVE_ERROR通知的詳細資料
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '6868'
ht-degree: 2%

---

# NATIVE_ERROR通知的詳細資料 {#details-for-the-native-error-notification}

TVSDK處理原生錯誤時，會以字串形式傳回部分或全部下列中繼資料索引鍵值。

<table id="table_7F713B7A56024D8DA3C84E449D09CC91"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 中繼資料金鑰名稱 </th> 
   <th colname="col2" class="entry"> 中繼資料值 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR_CODE</span> </td> 
   <td colname="col2"> <p>來自AVE的原生錯誤代碼。 </p> <p>這些程式碼代表下列專案： 
     <ul id="ul_1F33D523DDFE4CE8B4F0DC279FF7E4F8"> 
      <li id="li_07A2D9BEE6364935A61EF3BD4AB6DE27">DRM錯誤（代碼3300至3367）。 這些與同等的Flash Player錯誤碼相同 </li> 
      <li id="li_433BA22DE3504AEEB623598BB4F939FA">視訊播放錯誤（–1到89） </li> 
      <li id="li_B347CB151DB94DE0A1DDEB1B33D2DABA">加密錯誤（300到307） </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR</span> </td> 
   <td colname="col2">通知的簡短說明(例如， <span class="codeph"> AAXS_InvalidVoucher</span> 或 <span class="codeph"> 解碼器失敗</span>)。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 說明</span> </td> 
   <td colname="col2"> 通知的完整說明（例如，廣告解析作業已失敗）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR_CODE</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.PSDKErrorCode</span> 字串形式的數值（例如「13」）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.PSDKErrorCode</span> 作為字串(例如， <span class="codeph"> kECNetworkError</span>)。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 警告</span> </td> 
   <td colname="col2"> 警告的說明。 </td> 
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
   <td colname="col2"> 來自DRM模組的次要錯誤。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> drm_ERROR_STRING</span> </td> 
   <td colname="col2"> 錯誤說明。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DRM_ERROR_SERVER_URL</span> </td> 
   <td colname="col2"> TVSDK嘗試連線之DRM伺服器的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>廣告資訊清單載入失敗</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_URL</span> </td> 
   <td colname="col2"> 無法載入的內容的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_TYPE</span> </td> 
   <td colname="col2">廣告型別（來自的常數） <span class="codeph"> MediaResource.Type</span> 列舉)。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_DURATION</span> </td> 
   <td colname="col2"> 廣告持續時間（毫秒）。 </td> 
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
   <td colname="col2"> 正在下載的檔案URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> MANIFEST_ERROR</span> </td> 
   <td colname="col2"> 資訊清單檔案下載期間的錯誤說明。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> CONTENT_ERROR</span> </td> 
   <td colname="col2">片段期間的錯誤說明(例如， <span class="codeph"> ts</span>)下載。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>音訊曲目錯誤</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 音訊曲目名稱</span> </td> 
   <td colname="col2"> 無法載入的音訊曲目的名稱，如資訊清單中所指定。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_LANGUAGE</span> </td> 
   <td colname="col2"> 資訊清單中指定的音訊曲目的語言。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>搜尋錯誤</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_PERIOD</span> </td> 
   <td colname="col2"> 期間的ID （整數）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_POSITION</span> </td> 
   <td colname="col2"> <p>尋找的位置（以毫秒為單位） （兩次）。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>其他</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> Auditude_錯誤碼</span> </td> 
   <td colname="col2"> 錯誤碼（數字）Auditude。 </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR： DRM值 {#section_D240082B93D34902A18C3923C1C717B3}

Adobe視訊引擎的Video Encoder介面會傳回這些DRM通知 `NATIVE_ERROR` 中繼資料物件。

在向Adobe報告DRM錯誤時，請務必包含 `NATIVE_SUBERROR_CODE` 和 `DRM_ERROR_STRING` 以取得疑難排解協助。

>[!TIP]
>
>此清單提供有關錯誤的TVSDK特定資訊。 如需完整說明，請參閱 [Adobe Flash Platform的ActionScript執行階段錯誤ActionScript參考](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html#3300).

<table id="table_CD59A859865F4FFDBAA249C89C74770A"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> NATIVE_- ERROR_CODE中繼資料索引鍵的值 </th> 
   <th colname="col2" class="entry"> NATIVE_ERROR_NAME中繼資料索引鍵的值 </th> 
   <th colname="col3" class="entry"> 含義 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 3300 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidVoucher</span> </td> 
   <td colname="col3"> 
    <ul id="ul_516E4CB32D624B22892DDB9266CB04CA"> 
     <li id="li_348FC0F38B11417994119B61C9244076">散發者的軟體應該做什麼： 
      <ul id="ul_7AFD45CF92454BA4927783FAA628FBC4"> 
       <li id="li_0D9CCE61612643648C12DCDDD252E52A">如果您使用Google Chrome，且處於無痕模式，但您的Flash Player版本低於11.6，則可能會發生此錯誤。 <p>我們建議播放器檢查瀏覽器的版本號碼，並建議使用者退出無痕模式。 </p> </li> 
       <li id="li_1DC6B755BD0840D48BEC92568FD330BA">再次要求授權。 <p>如果請求成功，您就不需要記錄或呈報。 如果要求不成功，請記錄導致錯誤的內容。 <span class="codeph"> subErrorId</span> 包含行錯誤（如果存在）。 </p> </li> 
      </ul> </li> 
     <li id="li_060B5D60C9BB419CBFA7B062FBCF2632">散發者應該做什麼： 
      <ul id="ul_FADB29DBF0DA4A0E8E54134AEB7DCD8A"> 
       <li id="li_FC5B1C04D21E4AECB0EBD9ADD3198504">如果Flash低於11.6版的Chrome以外的組態重試失敗，封裝中可能會發生失敗。 </li> 
       <li id="li_A720ECE591254021879B335B81B1F76D">檢查該問題是否特定於某些內容並重新封裝。 </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3301 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthenticationFailed</span> </td> 
   <td colname="col3"> <p>伺服器無法驗證或授權使用者端。 </p> 
    <ul id="ul_BE77AC1848FB4C09B6318359ACF1B8EE"> 
     <li id="li_6FB37D317D174E8488C5070D20CD241C">散發者的軟體應採取一切必要動作，以重新建立使用者的認證，或引導使用者取得內容的存取權。 </li> 
     <li id="li_BE071D59805B42D38E3E7650BC936417">散發者應確認散發者的授權和驗證機制正常運作。 <p>如果發行者不打算使用驗證或授權功能，他們應該檢查違規內容的原則是否需要驗證，並參閱診斷原則/授權差異。 </p> </li> 
    </ul> <p>如需此錯誤碼的詳細資訊，請參閱 <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> DRM錯誤3301的原因和解決方法</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3302 </td> 
   <td colname="col2"><span class="codeph"> AAXS_RequireSSL</span> </td> 
   <td colname="col3"> <p>在Access 4.0和更新版本上，當遠端金鑰URL未使用HTTPS做為配置時，iOS會擲回此錯誤。 需要HTTPS。 </p> 
    <ul id="ul_3D47777BBCA14B67B107FBBE3E37E40C"> 
     <li id="li_7F7BBB27AE754CC39ABAAF9269739C49">如果散發者使用的版本比Access v4舊，或版本至少為4，但平台不是iOS，散發者的軟體應記錄錯誤。 <p>僅在iOS上擲回錯誤。 </p> </li> 
     <li id="li_D83C427D2A0D47408F723EF7195070B6">如果散發者的軟體至少是Adobe存取版本4，而且平台是iOS，散發者必須將其使用的遠端金鑰伺服器URL變更為HTTPS。 <p>如果他們只使用HTTP，經銷商可能必須設定HTTPS伺服器。 否則，分銷商需要提交記錄的資訊以Adobe和升級問題。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3303 </td> 
   <td colname="col2"><span class="codeph"> aaxs_ContentExpired</span> </td> 
   <td colname="col3"> <p>根據內容提供者設定的規則，您正在檢視的內容已過期。 subErrorId包含使用者端特有的錯誤或行錯誤。 </p> <p> 
     <ul id="ul_1E4B3B8AE87A4E79997553BB2A0E52B9"> 
      <li id="li_EE3F2EEBF73743B9A38E4FCB7531E275">散發者的軟體應嘗試從伺服器重新取得授權一次，以判斷是否有新的未到期授權可用。 <p>如果沒有可用的授權或授權已過期，請允許使用者取得新的授權，或通知使用者無法觀看內容。如果內容已封裝包含過期/結束日期已過期的原則，授權伺服器會記錄報告 <span class="codeph"> PolicyEvaluationException</span> 和指出原則結束日期已過期（伺服器錯誤碼303）。 檢查伺服器的記錄檔以進行驗證。 </p> <p>如果可能的話，客戶應該檢查他們在封裝期間使用的原則，看看它是否已經過期。 Java命令列工具是： 
        <code>
         java&nbsp;-jar&nbsp;libs/AdobePolicyManager.jar&nbsp;&nbsp;&nbsp;detail&nbsp;demo.pol
        </code> </p> </li> 
      <li id="li_50DBE680D8F04E7DA3E29C65A93188E7">分銷商應確認授權到期日是否按預期設定。 </li> 
     </ul> </p> <p>如需此錯誤碼的詳細資訊，請參閱 <a href="https://forums.adobe.com/thread/1300813" format="https" scope="external"> 使用Live Stream的AMS/FMS為3303 （內容已過期）？</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3304 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthorizationFailed</span> </td> 
   <td colname="col3">如需此錯誤碼的詳細資訊，請參閱 <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> DRM錯誤3301的原因和解決方法</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3305 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerConnectionFailed</span> </td> 
   <td colname="col3"> <p>由於網路延遲或使用者端離線，與授權或網域伺服器的連線逾時。 通常subErrorId包含HTTP傳回碼。 </p> 
    <ul id="ul_938C7D8F07F64B4FA71A09DDF37E2E64"> 
     <li id="li_6648EA0049094E369BD9AE9CCA6B148D">散發者的軟體應該嘗試網路連線到已知正常的伺服器。 <p>如果嘗試失敗，則提示使用者重新連線到網路。 如果嘗試成功，則將其記錄。 </p> </li> 
     <li id="li_2ECA2C04BA08449DA3AD79A52EFAA229">散發者應確認任何使用中的授權和網域伺服器已上線，且可從使用者端的網路中看到。 </li> 
    </ul> <p>如需此錯誤碼的詳細資訊，請參閱 <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> DRM 3305 [ServerConnectionFailed]原因和解決方法</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3306 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClientUpdateRequire</span> </td> 
   <td colname="col3"> 使用較新版的Android版TVSDK。 <p>目前的使用者端無法完成要求的動作，但更新的使用者端可能能夠完成要求。 </p> <p>這可能有幾個原因： 
     <ul id="ul_2EC4D42D5273439FA1AFDA1A2578B3D6"> 
      <li id="li_FCA926F5FAED4E7190BE855545AB6ACF">使用的共用網域在此使用者端無法使用。 在Chrome上播放運作時，就很可能發生這種情況，但其他任何瀏覽器皆然，反之亦然。 <p> <p>提示： Chrome使用的PHDS/PHLS金鑰與其他瀏覽器使用的不同。 如需詳細資訊，請參閱 <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>. </p> </p> </li> 
      <li id="li_3B633FB699234DCEA136E9BE3CC3386D">應用程式正在嘗試在5.0之前的iOS版本上執行時新增多個DRMSession。 </li> 
      <li id="li_F7ED993AF0B941A7A27216B4D587A999">僅支援版本2時，中繼資料的版本為3或更高版本。 </li> 
     </ul> </p> 
    <ul id="ul_EE4AE6AD4F1745A5B5623E53B599DB62"> 
     <li id="li_7A83869D4262443DA35FA1DF8D3097DD">散發者的軟體應提醒使用者並中止作業。 <p>如果軟體有辦法判斷是否有升級可用，請以適當的平台方式將使用者導向該升級。 </p> </li> 
     <li id="li_AF9C2711FDE54DA196EB9D2864632000">如果問題是因為共用網域而發生，散發者將需要向Adobe檢查更新的執行階段或程式庫。 <p>對於Flash執行階段，散發者可以直接在其應用程式中強制升級。 若是程式庫，散發者需要取得更新的程式庫、重建其應用程式並將其部署給使用者。 </p> <p>如果問題因多個DRMSessions而發生，散發者將需要更新其應用程式以在新增多個DRMSessions之前檢查iOS版本號碼。 或者，他們也可以限制將其應用程式發佈到iOS v5及更高版本。 </p> <p>如果問題是因為中繼資料版本高於版本2而發生，則問題可能是中繼資料已損毀。 他們可以嘗試重建中繼資料並檢視結果。 如果他們持續看到問題，請記錄問題並升級至Adobe。 </p> </li> 
    </ul> <p>如需此錯誤碼的詳細資訊，請參閱 <a href="https://forums.adobe.com/thread/1266675" format="https" scope="external"> 如何修正3306 DRMErrorEvent錯誤碼</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3307 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InternalFailure</span> </td> 
   <td colname="col3"> <p>這通常表示Adobe存取程式碼中的錯誤，除非存在已知的錯誤，否則這是意外狀況，如下所述。 subErrorId包含使用者端特有的錯誤或行錯誤。 </p> 
    <ul id="ul_79F4A9655A2148519B1E9509C41F78C3"> 
     <li id="li_0E093AB4D6BD489B852279E6C1525A15">如果瀏覽器在Windows上為Chrome，而Flash版本為11.6 (SWF版本19或更高版本)，則發行者的軟體應假設使用者按下 <span class="uicontrol"> 拒絕</span> 在資訊列上，並將相同的視為一個3368。 </li> 
     <li id="li_0215D1089B344861A2C0A73E1067CFEF">如果瀏覽器不是Chrome或Flash版本不是11.6時發生3307，則分銷商應升級至Adobe。 </li> 
    </ul> <p>重要： <span class="codeph"> 3307：1107296344 (FailedToGetBrokerHandle)</span> Chrome瀏覽器24-28版可能會發生。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3308 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WrongLicenseKey</span> </td> 
   <td colname="col3"> <p>當使用的授權包含解密內容的錯誤金鑰時，就會擲回此錯誤。 subErrorId包含使用者端特有的錯誤或行錯誤。 </p> <p>產生此錯誤的方式似乎只有兩種： 
     <ul id="ul_1C955BD74C7843809D1B5A0CDCA5ED7B"> 
      <li id="li_18F0A7FDA6584887AD9DB3EDE54080D8">客戶已修改用於產生授權的標準Adobe工具（例如授權者伺服器Java架構）。 <p>在此情況下，授權包含可能未對應到任何內容的錯誤金鑰。 </p> </li> 
      <li id="li_21D04ED1F1FA464785BC297D385766FF">客戶已使用相同的授權ID核發多個授權。 <p>在此情況下，使用者端上有多個可用的授權符合內容中繼資料，而且存取代碼選擇了錯誤的授權來使用。 </p> </li> 
     </ul> </p> 
    <ul id="ul_64AEE62BE36946F290067CF475A36ECA"> 
     <li id="li_9EEB2B11A4DA41E78C5840D8FAA81F0D">散發者的軟體應該嘗試從伺服器重新取得授權。 
      <ul id="ul_ACADC5518B054D0A853AEED2B675DB23"> 
       <li id="li_394835C8731048A5BF7D9370AC12448C">如果沒有可用授權或授權已過期，請提供工作流程讓使用者取得新授權，或通知使用者無法觀看內容並記錄問題。 </li> 
       <li id="li_3FE50518BE53405F9563FA620F7EAD5F">如果這是網域繫結內容(適用於AIR)，請為使用者提供加入網域的方式。 </li> 
      </ul> </li> 
     <li id="li_C80B353C1AEA4E9398241420CB491E84">散發者應： 
      <ul id="ul_B5C50009374C4EED9B2B050B48F5F0F6"> 
       <li id="li_D5E6B760E0BC4B5C949ED1544B398838">確認他們尚未自訂Access License伺服器的授權發行部分。 </li> 
       <li id="li_AA8F4E4B6DDD40BA8807C0920A92186B">確認他們為所有授權核發唯一的授權ID。 </li> 
       <li id="li_A2C53FE779AC4FDDB65E00A2C4F43EC4">升級Adobe的問題。 </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3309 </td> 
   <td colname="col2"><span class="codeph"> aaxs_CorruptedAdditionalHeader </span> </td> 
   <td colname="col3"> <p>如果標題大於65536位元組，就會發生此狀況。 </p> 
    <ul id="ul_82C0F688519B4F43A764D59A891F1903"> 
     <li id="li_E66AC9149A0649E88A79C5289C12C395">散發者的軟體應該記錄導致錯誤的內容片段。 </li> 
     <li id="li_1C5916A33E7B4DC9968105B9BD20A727">散發者應確認錯誤可透過特定內容片段重現。 重新封裝損毀的內容。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3310 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppIDMismatch </span> </td> 
   <td colname="col3">Android應用程式與使用中的應用程式不符。 <p>未使用正確的AIR應用程式或FlashSWF。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3311 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppVersionMismatch </span> </td> 
   <td colname="col3"> 未使用。 AIR中的1.x版棧疊可能仍會產生此問題。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3312 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LicenseIntegrity </span> </td> 
   <td colname="col3"> 若要修正此問題，請從伺服器重新下載授權。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3313 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WriteMicrosafeFailed </span> </td> 
   <td colname="col3"> <p>當系統無法寫入檔案系統時，就會發生此問題。 <span class="codeph"> subErrorId</span> 包含使用者端特有的錯誤或行錯誤。 </p> <p>在Microsoft Windows上，當加密的內容具有licenseID或policyID太長時，Active X或NPAPI外掛程式flash player可能會擲回錯誤3313。 這是因為Windows中的路徑長度上限。 （Pepper外掛程式沒有這個問題。） </p> <p>請參閱watson 3549660 </p> 
    <ul id="ul_DFD527D1E1224A439766DF7BED878E3B"> 
     <li id="li_FAF8FD98A4E8478CA7A92F770676ADFC">散發者的軟體應提示使用者確認其使用者目錄未鎖定，或位於已滿或已鎖定的磁碟區上。 </li> 
     <li id="li_6D1136EA750A459BBECEEE5F73F527BB">如果散發者使用AIR而非Flash，問題可能是由於路徑長度限制所造成。 <p>經銷商應將其AIR應用程式的名稱縮短為合理名稱。 此外，以較短的時段再次發佈內容 <span class="codeph"> licenseID</span> 和 <span class="codeph"> policyID</span>. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3314 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptedDRMMetadata </span> </td> 
   <td colname="col3"> <p>此錯誤通常表示內容已封裝測試PKI憑證，而播放器是透過生產PKI建置，反之亦然。 subErrorId包含使用者端特有的錯誤或行錯誤。 </p> 
    <ul id="ul_A122EF304CAF48A8B4DA1E3F4413E29B"> 
     <li id="li_A9A1A5B23E884C22A71E2DE7535FEB3B">散發者的軟體應該記錄導致錯誤的內容片段。 </li> 
     <li id="li_7AD7F13A4B1B4998A7E49664E7645815">散發者應確認此錯誤可透過特定內容片段重現。 <p>您可能必須重新封裝損毀的內容。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3315 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PermissionDenied </span> </td> 
   <td colname="col3"> <p>已知的Bug會在預期3305時擲回此錯誤碼。 如需詳細資訊，請參閱 <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> DRM 3305 [ServerConnectionFailed]原因和解決方法</a>. </p> <p>AIR載入的遠端SWF無法存取Flash Access功能。 如果在網路存取期間發生安全性錯誤，也會擲回此錯誤碼。 例如，目的地伺服器不是使用crossdomain.xml連線的使用者端，或無法連線crossdomain.xml。 </p> <p>如需詳細資訊，請參閱 <a href="https://forums.adobe.com/thread/1266592" format="https" scope="external"> DRM錯誤3315可能的根本原因和解決方法</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3316 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NOTUSED_MOVED </span> </td> 
   <td colname="col3"> 為 <span class="codeph"> ADOBECPSHIM_MinorErr_MissingAdobeCPModule</span>. 已移動到3344，因為與Flash錯誤代碼衝突。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3317 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LoadAdobeCPFailed </span> </td> 
   <td colname="col3"> <p>重要：這是罕見的錯誤，通常不會發生在生產環境中。 </p> <p>如果發生錯誤，您可以執行下列任一項作業： 
     <ul id="ul_BC435E61623444BB98A86216531DC892"> 
      <li id="li_FA433D0758B642D2AFDCF04906B3FE18">如果您正在使用AIR，請重新安裝它。 </li> 
      <li id="li_F08D9AAFF46244F8842DEE5FD9CBBE0A">如果您正在使用Flash Player，請下載 <span class="codeph"> adobecp</span> 再次顯示模組。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3318 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncompatibleAdobeCPVersion </span> </td> 
   <td colname="col3"> 不適用於Android。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3319 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MissingAdobeCPGetAPI </span> </td> 
   <td colname="col3"> 不適用於Android。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3320 </td> 
   <td colname="col2"><span class="codeph"> AAXS_HostAuthenticateFailed </span> </td> 
   <td colname="col3"> 不適用於Android。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3321 </td> 
   <td colname="col2"><span class="codeph"> AAXS_I15n失敗 </span> </td> 
   <td colname="col3"> <p>提供金鑰給使用者端的程式失敗。 subErrorId包含使用者端特有、伺服器特有或行錯誤。 </p> 
    <ul id="ul_98D919B9060A441AACB6106F6D8E8DA7"> 
     <li id="li_DCAB00A8AC4A426CBBD377374B3F71AE">散發者的軟體應至少重試一次作業。 <p>如果您在Windows上使用Google Chrome，請說明如何允許不在沙箱中的外掛程式存取。 Google Chrome的沙箱存取遭拒</a>. </p> </li> 
     <li id="li_7FB7681FE32D444BB1BDBA3E5953A2C3">散發者應該完成下列其中一項工作： 
      <ul id="ul_486B64F187C44AE3B4775953A6142836"> 
       <li id="li_095B1D4CD051427CB2BFA7082B454056">如果錯誤在各平台間是一致的，您應使用Adobe將問題升級。 </li> 
       <li id="li_0C6EB7B912FA41E59657216498DA3515">如果錯誤僅限於Windows上的Chrome，請引導使用者允許無沙箱外掛程式存取。 </li> 
      </ul> <p>經銷商應將其SWF更新至版本19或更新版本，且擲回Chrome特有的3321錯誤和3368錯誤。 錯誤3368可由散發者的軟體更具體處理。 此變更已在Chrome穩定通道26.0.1410.43版中引入。 </p> <p>提示：錯誤 <span class="codeph"> 3321：1090519056</span> Flash Player版本11.1到11.6可能會發生。建議您升級至最新的Flash Player版本。 </p> </li> 
    </ul> <p>如需詳細資訊，請參閱 <a href="https://forums.adobe.com/thread/1277138" format="https" scope="external"> DRM錯誤3321原因與解決方法</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>全域存放區損毀錯誤</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3322 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DeviceBindingFailed </span> </td> 
   <td colname="col3"> <p>裝置似乎不符合初始化時存在的設定。 subErrorId包含使用者端特有的錯誤或行錯誤。 </p> <p>散發者的軟體應完成下列其中一項作業： 
     <ul id="ul_444401051A2E407B95BC44491E9BB71C"> 
      <li id="li_93493EA05DB44CB1AEC368663F1ABA8D"> <p>如果裝置未使用Flash Player，而是使用AIR、iOS等，請呼叫 <span class="codeph"> DRMManager.resetDRMVouchers()</span>. </p> <p>如果iOS在開發階段發生問題，請要求開發人員確認在從協力廠商發行前發佈系統（例如HockeyApp）下載的組建與從Xcode下載的本機組建之間切換時，是否發現問題。 在從HockeyApp分發的組建和從Xcode分發的組建之間切換時，不會完全覆寫先前安裝的屬性。 此情況可能會觸發3322錯誤。 </p> <p>若要解決此問題，開發人員應先從裝置移除舊組建，然後再安裝新組建。 </p> </li> 
      <li id="li_A5C9633F11584C788A2D9A23CC18FA6D">如果裝置正在使用Flash Player，並且因3322或3346錯誤代碼而無法使用，請參閱Adobe中有關如何以程式設計方式重設您的DRM授權存放區的指示，網址為 <a href="https://forums.adobe.com/message/5535907#5535907" format="https" scope="external"> Chrome中的DRM錯誤3322/3346/3368 （資訊列問題）</a>. </li> 
     </ul> </p> <p>此錯誤預計不會頻繁發生。 在使用漫遊設定檔的公司環境中，如果使用者檢視受DRM保護的內容，則當使用者從不同電腦登入時，發生錯誤3322的機會會增加。 如果可能的話，散發者應該嘗試從使用者取得此資訊。 </p> <p>如果錯誤經常發生，請升級至Adobe。 您必須通知Adobe重設授權存放區是否解決此問題，並告知Adobe在哪些瀏覽器上發生錯誤。 </p> <p>如需詳細資訊，請參閱下列文章： 
     <ul id="ul_C468409D1EA046178CA7F54DCDCB84EA"> 
      <li id="li_20C8CA3853574CE486F21E7A3667DAB9"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> https://forums.adobe.com/message/5520902</a> </li> 
      <li id="li_6E6F1BD6FE7843449B3E2F06F342EFF7"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> https://forums.adobe.com/message/5535911</a> </li> 
      <li id="li_2BE40E513A0C4BAD900C7B69FEF5D690"><a href="https://forums.adobe.com/message/5748618" format="https" scope="external"> https://forums.adobe.com/message/5748618</a> </li> 
      <li id="li_9C2BD122E3874E2893DD43E082A877E0"><a href="https://forums.adobe.com/message/6061165" format="https" scope="external"> https://forums.adobe.com/message/6061165</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3323 </td> 
   <td colname="col2"><span class="codeph"> aaxs_CorruptGlobalStateStore </span> </td> 
   <td colname="col3"> <p>DRM使用者端使用的檔案已意外修改。 subErrorId包含使用者端特有的錯誤或行錯誤。 </p> 
    <ul id="ul_96EA771046CA4B2B9FAE24D493F43FF2"> 
     <li id="li_D2693CD8EFEF46108828BA17E3F54FF6">散發者的軟體應該會以與3322相同的方式，引導使用者重設。 </li> 
     <li id="li_0149B82436B64E28AC2B8C9B0EB09898">如果GlobalStore的故障率高於使用者群硬碟的預期故障率，請將問題升級至Adobe。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3324 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MachineTokenInvalid </span> </td> 
   <td colname="col3"> 重設此應用程式的DRM本機儲存體。 呼叫DRMManager.resetDRM。 <p>授權伺服器可能無法連線到憑證撤銷清單(CRL)伺服器來重新整理其CRL檔案，或是使用者端電腦正在要求由授權伺服器撤銷的授權/驗證。 </p> <p>在伺服器記錄中，錯誤碼111為MachineTokenInvalid。 然而，在使用者端層級，錯誤碼111被轉換為錯誤碼3324。 </p> <p>DRM授權伺服器管理員應檢查客戶的授權伺服器是否曾經能夠擷取AdobeCRL檔案。 如果客戶正在使用Tomcat，則客戶可以檢查<span class="filepath"> tomcat/temp/</span> 目錄以檢視是否有4個CRL檔案。 </p> 
    <ul id="ul_23B7F1A104AF49E79EA87DB8E15E337E"> 
     <li id="li_855D87F251184FE688A8D5FA0F6C9EF5">如果檔案在此目錄中，請在Windows檔案總管和CRL檢視器應用程式中連按兩下檔案，判斷是否有任何檔案已過期。 </li> 
     <li id="li_58EC4EDA2B5146188A0FF7B33C91E2FD">如果tomcat/temp/中沒有任何檔案，則可以假設由於防火牆/路由問題，此授權伺服器從未能夠連線到AdobeCRL伺服器。 </li> 
    </ul> <p>如需詳細資訊，請參閱 <a href="https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_secure_deployment_guidelines.pdf" format="http" scope="external"> 防火牆規則</a>. </p> <p>如果CRL檔案無法使用或已過期，您必須確認是否可以連線到授權伺服器。 在客戶的授權伺服器上開啟網路Sniffer，重新啟動伺服器，並讓使用者端嘗試從伺服器要求授權。 您可以觀察網路流量，以檢視對以下URL端點的呼叫是否成功： <p>提示：您也可以在瀏覽器中輸入下列CRL URL，以檢視是否可以手動下載每個檔案。 </p> 
     <ul id="ul_9B65C7ABBDEC4AC9BF3755FFD3587971"> 
      <li id="li_6867A9050E8D421C9138AC853D1784C9"><a href="https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl</a> </li> 
      <li id="li_6431689260554EAFAFDA2EC31798DCB5"><a href="https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl</a> </li> 
      <li id="li_2939674D0F854ADEB67E45FD216288A2"><a href="https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessRootCA.crl</a> </li> 
      <li id="li_96386E00BE9D4CB99D100057A5F7C6DD">crl3.adobe.com/AdobeSystemsIncorporated FlashAccessRuntime/LatestCRL.crl</li> 
     </ul> </p> <p>如果防火牆規則是開啟的，而且目前沒有任何3324錯誤，則可能是暫時性的網路問題。 檢查客戶的伺服器記錄，這些記錄可能位於 <span class="codeph"> /tomcat/logs/</span> 目錄，以判斷授權伺服器嘗試擷取「憑證撤銷清單」時是否發生錯誤。 <p>重要：續約CRL檔案時，如果大量使用者端報告3324錯誤至暫時性的網路問題，可能會發生錯誤。 當網路問題解決時，3324問題也解決了。 </p> </p> <p>如果所有4個CRL檔案都存在於 <span class="filepath"> tomcat/temp/</span> 目錄，而使用者端仍收到3324錯誤碼，則可能對CRL檔案造成檔案存取問題。 若要解決此問題，您可能想要檢閱記錄檔並清除現有的CRL檔案。 </p> <p>如果沒有伺服器問題，請提示使用者在中重設，如3322所述。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>伺服器存放區損毀錯誤</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3325 </td> 
   <td colname="col2"><span class="codeph"> aaxs_CorruptServerStateStore </span> </td> 
   <td colname="col3"> <p>DRM使用者端使用的檔案已意外修改。 <span class="codeph"> subErrorId</span> 包含使用者端特有的錯誤或行錯誤。 </p> 
    <ul id="ul_860D2402DA61460AB0D938F1116F6D64"> 
     <li id="li_CF368C43452B4265B62ADA3E223894BA">散發者的軟體應再次重試操作，因為AdobeCP已在內部刪除違反規定的伺服器存放區，重試應該會成功。 如果重試失敗，請記錄問題。 </li> 
     <li id="li_51A5803A1F754970BB4EBD6494F5DC96">如果重試失敗率高於使用者基礎硬碟的預期失敗率，請將問題升級至Adobe。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3326 </td> 
   <td colname="col2"><span class="codeph"> AAXS_StoreTamperingDetected </span> </td> 
   <td colname="col3"> 呼叫 <span class="codeph"> DRMManager.resetDRM</span>. <p>授權存放區已遭竄改/損毀，無法再使用。 </p> <p>散發者的軟體應該會以3322中說明的相同方式引導使用者重設。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3327 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClockTamperingDetected </span> </td> 
   <td colname="col3"> 固定時鐘或取得 <span class="codeph"> 授權/授權/網域</span> 再次授權。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>驗證/授權/網域伺服器錯誤</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3328 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerErrorTryReagate </span> </td> 
   <td colname="col3"> <p>這是伺服器端錯誤，伺服器無法完成來自使用者端的要求。 例如，當伺服器忙碌中、HTTP/500、伺服器沒有解密要求所需的金鑰等時，就會發生此錯誤。 </p> <p>在使用者端上，無法判斷哪裡發生錯誤。 客戶必須檢閱Adobe存取伺服器記錄檔(通常稱為 <span class="codeph"> AdobeFlashAccess.log</span>，以判斷哪裡出了問題。 記錄中總是有描述性棧疊追蹤來指示問題。 <span class="codeph"> subErrorId</span> 包含伺服器特定錯誤或行錯誤。 </p> <p>散發者應檢視伺服器記錄檔，以識別傳送此錯誤的伺服器。 對於具有子錯誤代碼101的3328錯誤，伺服器無法解密請求。 客戶必須驗證安裝在授權伺服器上的授權/傳輸伺服器憑證是否相符，並與封裝期間使用的憑證相對應。 </p> <p>此外，如果客戶使用參考實作，他們必須確保 <span class="codeph"> flashaccess-refimpl.properties</span> 在其中指定主要和其他憑證的檔案。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3329 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ApplicationSpecificError </span> </td> 
   <td colname="col3"> <p>Flash Access不知道應用程式專屬的子錯誤碼。 <span class="codeph"> subErrorId</span> 包含來自發行者自訂授權伺服器的伺服器特定錯誤。 伺服器在應用程式專屬的名稱空間中傳回錯誤。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3330 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NeedAuthentication </span> </td> 
   <td colname="col3"> <p>當內容設定為要求使用者端在取得授權前進行驗證時，就會發生此錯誤。 </p> 
    <ul id="ul_712D29B8B5A6401FB014C4A283918E32"> 
     <li id="li_2D56905EB50D4FDEAD69CA8EAE38AD1A">散發者的軟體應該驗證使用者，然後再次取得授權。 <p>如果您的服務不打算使用驗證，請記錄造成此錯誤之內容的識別碼。 </p> </li> 
     <li id="li_B3BCF899B8BE41C7A4F7CF84B0503483">除非內容不應設定為需要驗證，否則此錯誤不應要求呈報。 <p>在這種情況下，請使用適當的原則重新封裝違規內容。 如果內容已正確封裝，請參閱診斷原則/授權差異。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>上面未涵蓋的授權執行錯誤</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3331 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentNotYetValid </span> </td> 
   <td colname="col3"> <p>取得的授權尚未生效。 若要解決此問題，請檢查使用者端時鐘是否設定不正確。 若要設定使用者端時鐘，請重新封裝內容或修改許可證伺服器設定。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3332 </td> 
   <td colname="col2"><span class="codeph"> aaxs_CachedLicenseExpired </span> </td> 
   <td colname="col3"> 從伺服器重新取得授權。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3333 </td> 
   <td colname="col2"><span class="codeph"> aaxs_PlaybackWindowExpired </span> </td> 
   <td colname="col3"> <p>您必須通知使用者，在原則到期之前，他們無法播放此內容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3334 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMPlatform </span> </td> 
   <td colname="col3"> <p>此平台不允許播放內容，例如，因為內容提供者已設定Adobe存取以拒絕內容在平台上的Adobe存取，或共用網域繫結的授權繫結至專用於其他分割的共用網域權杖。 </p> <p>如果未使用適當的（CDM功能閘道式）封裝器憑證來封裝內容，CDM可能會擲回此錯誤。 </p> <p>如果內容使用不正確的PHDS/PHLS憑證封裝，內容可能會在Chrome中運作，但不能在其他瀏覽器中運作（反之亦然）。 <p>提示：這是因為Chrome使用不同的PHDS/PHLS憑證。 </p>若要確認正在使用哪個憑證，請傾印內容中繼資料的詳細資訊並尋找 <i>收件者憑證</i>. 如需詳細資訊，請參閱 <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3335 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMVersion </span> </td> 
   <td colname="col3"> 升級至Android適用的最新版TVSDK。 <p>若要解決此問題，請完成下列其中一項作業： 
     <ul id="ul_BF1742948BC9461CB8686DE70124D3CD"> 
      <li id="li_690D440C94CC45A0AE55EC319B1C4C23">升級AIR </li> 
      <li id="li_CDD20251C881466E88BE7BBB53D61EBC">如需Flash Player，請升級AdobeCP模組並重試播放。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3336 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidRuntimePlatform </span> </td> 
   <td colname="col3"> <p>此平台不允許播放內容，因為內容提供者已設定「存取」以拒絕平台上的FP/AIR內容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3337 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidRuntimeVersion </span> </td> 
   <td colname="col3"> 升級至Android適用的最新版TVSDK。 <p>如果內容或伺服器設定為拒絕播放特定版本的Flash或AIR執行階段，就會發生此狀況。 </p> 
    <ul id="ul_B0732D941256483CABBDD30C9BF43249"> 
     <li id="li_72782B1D638F48C0B87084689FB9C798">如果使用者在可升級Flash的作業系統上，散發者的軟體應提示使用者升級Flash並再試一次。 否則，建議使用者使用不同的電腦。 </li> 
     <li id="li_1E3FD93CE39E43F2B7D961299B1211DA">如果懷疑錯誤3337s，請確定它是否發生在特定內容中，並重新封裝該內容。 如果內容已正確封裝，請參閱診斷原則/授權差異 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3338 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnknownConnectionType </span> </td> 
   <td colname="col3"> <p>無法偵測連線型別，原則要求您開啟輸出保護。 僅當封裝的內容需要數位或類比輸出保護時，才會出現此問題。 </p> <p>在11.8.800.168版以前的Flash Player版本中，原則指出內容保護為的內容偶爾會發生錯誤3338 <span class="codeph"> 使用可用時</span>. 此問題已在11.8.800.168版及更新版本中修正。 </p> 
    <ul id="ul_4B6CA26A53F84838B5B95400925464D4"> 
     <li id="li_CBD890F467E449EBB5116E1561252058">散發者的軟體會選取不需要輸出保護的內容變體（例如HD資料流的SD變體）。 <p>如果發生錯誤3338 <span class="codeph"> USE_IF_AVAILABLE </span> 內容，檢查播放器版本號碼。 如果播放器版本低於11.8.800.168，建議使用者升級Flash Player。 如果11.8.800.168以上的版本發生錯誤3338，請記錄導致錯誤的內容。 </p> </li> 
     <li id="li_62886C1D96264B129928A7E29E6C70E1">散發者應檢查造成此錯誤的內容，並驗證內容的原則是否正在設定 <span class="codeph"> 無保護(_P)</span> 或 <span class="codeph"> USE_IF_AVAILABLE</span> 適用於類比與數位輸出。 <p>如果內容無意中封裝了 <span class="codeph"> NO_OUTPUT</span> 或 <span class="codeph"> 必填</span>，重新封裝內容。 如果內容已正確封裝，請參閱診斷原則/授權差異。 否則呈報至Adobe。 </p> </li> 
    </ul> <p>如需詳細資訊，請參閱 <a href="https://forums.adobe.com/message/5518688" format="https" scope="external"> 當您的DRM原則設定為USE_IF_AVAILABLE時，是否發生未預期的3338錯誤？</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3339 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogPlaybackAllowed </span> </td> 
   <td colname="col3"> 無法在類比裝置上播放。 若要解決此問題，請連線數位裝置。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3340 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogProtectionAvail </span> </td> 
   <td colname="col3"> 無法播放內容，因為連線的類比外部顯示裝置（顯示器/電視）沒有正確的功能（例如，裝置沒有Macrovision或ACP）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3341 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalPlaybackAllowed </span> </td> 
   <td colname="col3"> 無法在數位裝置上播放內容。 <p>重要：此問題不應發生在生產環境中，因為內容發佈者不應禁止數位播放。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3342 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalProtectionAvails </span> </td> 
   <td colname="col3"> 連線的數位外接顯示裝置（顯示器/電視）沒有正確的功能。 例如，裝置沒有HDCP。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3343 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IntegrityVerificationFailed </span> </td> 
   <td colname="col3"> <p>不適用於Android。 </p> <p>目前已知此錯誤最初會在新版Flash發行後發生。 發生此狀況是因為Flash在Flash開啟時升級，而使Flash在瀏覽器重新啟動之前處於不良狀態。 </p> 
    <ul id="ul_A0AC4A77550E40409A04BD33748EA987"> 
     <li id="li_F41C1ABD838D41ABB0DF65093E664A29">散發者的軟體應該完成下列工作： 
      <ul id="ul_79B2AB1372074D448F129851AA24F985"> 
       <li id="li_B93EDD263D78434FAF198A01938D3508">建議使用者關閉或結束所有瀏覽器，然後重新開啟。 </li> 
       <li id="li_ADFBCFA66AD849E18DB390455458528E">檢查Flash的版本是否為最新版本。 <p>如果版本不是最新版本，建議客戶升級、關閉其瀏覽器中的所有索引標籤，然後重新開啟。 </p> </li> 
      </ul> </li> 
     <li id="li_281B54582B5949AEA7D166246917EE41">如果在成功重新啟動瀏覽器後發生錯誤，請升級至Adobe。 <p>新版本發行時，我們建議您聯絡Adobe支援，檢視背景更新問題是否已修正。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3344 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MissingAdobeCPModule </span> </td> 
   <td colname="col3"> 不適用於Android。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3345 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DRMNoAccessError </span> </td> 
   <td colname="col3"> <p>不適用於Android。 </p> <p>當部分Flash或AIR未正確安裝時，就會發生此錯誤。 </p> <p>散發者的軟體應該執行下列其中一項作業： 
     <ul id="ul_D1188E2D4FDF4BD89A04F5629D75D981"> 
      <li id="li_B33FBCA5D4534D668B86A5E93DB3A809">要求使用者解除安裝並重新安裝AIR。 </li> 
      <li id="li_B7D2388E9FA84C26AF1C87B48AF9EF16">如需Flash Player，請呼叫 <span class="codeph"> 系統更新</span>. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3346 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MigrationFailed </span> </td> 
   <td colname="col3"> 
    <ul id="ul_518AD4931CC64EB3A962DD451E6C5067"> 
     <li id="li_3C44F0740B08490E9C62D89C40B57DC2">散發者的軟體應該執行下列其中一項作業： 
      <ul id="ul_7D90526684BF4EB2BBADCF598AA13086"> 
       <li id="li_D15B4BEDAF7340F6B9BC886DF6E346EC">如果AIR，請呼叫 <span class="codeph"> DRMManager.resetDRMVouchers()</span> </li> 
       <li id="li_40A51D35408249CFA28DBC49FDA3408B">如果Flash因錯誤3322或3346錯誤代碼而無法使用，使用者應前往 <a href="https://forums.adobe.com/message/5535907#5535907" format="http" scope="external"> https://forums.adobe.com/message/5535907#5535907</a> 並遵循Adobe文章的指示，以程式設計方式重設其DRM授權存放區。 </li> 
      </ul> </li> 
     <li id="li_0464471E4A094C80BF2986694341921A">如果這個錯誤經常發生，散發者應該提供頻率播放器版本的詳細資料，以及要Adobe的瀏覽器版本。 </li> 
    </ul> <p>如需詳細資訊，請參閱下列論壇文章： 
     <ul id="ul_44E0077FEAA749CC9549BF3846065304"> 
      <li id="li_2BE3B2443380415DA73B7AA3B6547B31"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> Chrome中的DRM錯誤3322/3346/3368 （資訊列問題）</a> </li> 
      <li id="li_4E5C7414756644E1AB78BE7B8112228C"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> 硬體變更後出現3322或3346錯誤</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3347 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnffectedDeviceCapabilites </span> </td> 
   <td colname="col3"> <p>此錯誤的主要含義是授權具有限制，使用者端的DRM憑證指出它無法滿足。 發行使用者端DRM憑證時，會定義下列「硬體功能」： 
     <ul id="ul_1EB6F1469C244CF0BA52C212495C053D"> 
      <li id="li_646043CE045C4DE2BBC939E1F4963DFE"><b>非使用者可存取的匯流排</b>. 如果 <b>true</b>，解密的媒體絕不會流經匯流排或進入應用程式可存取的主記憶體。 <p>如果 <b>false</b>，應用程式在解密後可能會存取內容。 </p> </li> 
      <li id="li_02AAECAF4D35447BA10554541B46DE67"><b>信任的硬體根目錄</b>. 如果 <b>true</b>，所有在裝置上開機時載入的軟體，都會根據硬體提供的金鑰或摘要進行驗證。 <p>當針對使用者端的DRM憑證開啟許可證時，使用者端會檢查這兩個限制，並且會立即失敗。 在發行許可證之前，也可以在伺服器端檢查這些限制。 </p> </li> 
     </ul> </p> <p>此錯誤的次要含義是授權已設定「Jailbreak Enforcement」原則，且在裝置上偵測到越獄。 這項檢查定期在使用者端完成，無法在伺服器端進行檢查。 </p> <p>經銷商可以更新原則並移除限制。 針對裝置功能原則，使用發出原則更新命令 <span class="codeph"> -devCapabilitiesV1</span> 標幟且沒有引數。 對於越獄執行，設定 <span class="codeph"> policy.enforceJailbreak=false</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3348 </td> 
   <td colname="col2"><span class="codeph"> aaxs_HardStopIntervalExpired </span> </td> 
   <td colname="col3"> 硬停止間隔已過期。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3349 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionTooHigh </span> </td> 
   <td colname="col3"> 伺服器的執行版本高於使用者端支援的最高版本。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3350 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionTooLow </span> </td> 
   <td colname="col3"> 伺服器的執行版本低於使用者端支援的最低版本。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3351 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenInvalid </span> </td> 
   <td colname="col3"> 網域權杖無效。 若要解決此問題，請再次向網域註冊。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3352 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenTooOld </span> </td> 
   <td colname="col3"> 網域權杖比授權所需的權杖還要舊。 若要解決此問題，請再次向網域註冊。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3353 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenTooNew </span> </td> 
   <td colname="col3"> 網域權杖比授權所需的權杖新。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3354 </td> 
   <td colname="col2"><span class="codeph"> aaxs_DomainTokenExpired </span> </td> 
   <td colname="col3"> 網域權杖已過期。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3355 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainJoinFailed </span> </td> 
   <td colname="col3"> 網域加入失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3356 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoActivatedRoot </span> </td> 
   <td colname="col3"> 找不到V3分葉授權的根授權。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3357 </td> 
   <td colname="col2"><span class="codeph"> aaxs_NoValidEmbeddedLicense </span> </td> 
   <td colname="col3"> 找不到有效的內嵌授權。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3358 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoACPProtectionAvail </span> </td> 
   <td colname="col3"> 無法播放，因為連線的類比裝置沒有ACP保護。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3359 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoCGMSAProtectionAvail </span> </td> 
   <td colname="col3"> 無法播放，因為連線的類比裝置沒有CGMS-A保護。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3360 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainRegistrationRequired </span> </td> 
   <td colname="col3"> 內容需要網域註冊。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3361 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NotRegisteredToDomain </span> </td> 
   <td colname="col3"> 電腦未針對指定的中繼資料登入網域。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3362 </td> 
   <td colname="col2"><span class="codeph"> AAXS_OperationTimeoutError </span> </td> 
   <td colname="col3"> 非同步操作花費的時間超過 <span class="codeph"> maxOperationTimeout</span>. 僅由iOS DRMNative Framework傳回。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3363 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnsupportedIOSPlaylistError </span> </td> 
   <td colname="col3"> 傳入的M3U8播放清單包含不支援的內容。 僅由iOS DRMNative Framework傳回。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3364 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDeviceId </span> </td> 
   <td colname="col3"> <p>框架要求裝置ID，但傳回的值是空的。 </p> <p>使用者不應選取 <span class="uicontrol"> 允許受保護內容的識別碼</span> 核取方塊。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3365 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncognitoModeNotAllowed </span> </td> 
   <td colname="col3"> <p>此瀏覽器/平台組合不允許無痕模式下受DRM保護的播放。 </p> <p>散發者的軟體應建議使用者結束無痕模式或使用不同的瀏覽器。 如需詳細資訊，請參閱 <a href="https://forums.adobe.com/thread/1266622" format="https" scope="external"> DRM錯誤3365原因和解決方法</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3366 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadParameter </span> </td> 
   <td colname="col3"> <p>主機執行階段使用錯誤的引數呼叫存取程式庫。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3367 </td> 
   <td colname="col2"><span class="codeph"> aaxs_BadSignature </span> </td> 
   <td colname="col3"> m3u8資訊清單簽署失敗。 僅由iOS DRMNative Framework或AVE傳回。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3368 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UserSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>使用者已取消操作，或已輸入不允許存取系統的設定。 </p> <p>只有在SWF版本是19或更新版本時，才會擲回此錯誤。 為了回溯相容性，SWF版本為18或更舊版本時會擲回3321。 </p> <p>分銷商的軟體應引導使用者說明如何允許無沙箱外掛程式存取。 Google Chrome的沙箱存取遭拒</a> 和 <a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> Chrome中的DRM錯誤3322/3346/3368 （資訊列問題）</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3369 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InterfaceNotAvailable</span> </td> 
   <td colname="col3"> <p>必要的瀏覽器介面無法使用。 此問題僅發生在Pepper上。 Flash外掛程式和瀏覽器版本之間可能會不相符。 </p> <p>散發者的軟體應該會引導使用者，確保他們已安裝最新版本的瀏覽器。 </p> <p> 如果此錯誤的發生次數增加，且與已發佈的瀏覽器更新相對應，請升級至Adobe。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3370 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentIdSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>使用者已停用 <span class="uicontrol"> 允許受保護內容的識別碼</span> 設定。 </p> <p>提示：此錯誤出現在Pepper 13.0.0.x或更新版本中。 </p> <p>散發者的軟體應該引導使用者啟用 <span class="uicontrol"> 允許受保護內容的識別碼</span> 設定。 </p> <p>散發者的作業團隊應引導使用者啟用 <span class="uicontrol"> 允許受保護內容的識別碼</span> 設定。 </p> <p>如需詳細資訊，請參閱 <a href="https://forums.adobe.com/message/6518323#6518323" format="https" scope="external"> https://forums.adobe.com/message/6518323#6518323</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3371 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoOPConstraintInPixel</span><span class="codeph"> 限制</span> </td> 
   <td colname="col3"> <p>根據授權中的輸出保護限制，解析格式錯誤。 </p> <p>散發者的軟體應該會顯示錯誤訊息。 要求使用者以內容標題將問題報告給散發者。 </p> <p>散發者應使用有效原則重新封裝內容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3372 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ResolutionLargerThanMaxResolution</span> </td> 
   <td colname="col3"> <p>內容的解析度大於輸出保護限制中指定的最大解析度。 </p> <p>如果散發者的作業團隊在記錄中看到此錯誤，他們應該檢閱以解析度為基礎的輸出保護原則，並在必要時重新封裝內容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3373 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_DisplayResolutionLargerThanConstrain</span> </td> 
   <td colname="col3"> <p>內容的解析度大於目前作用中的輸出保護限制所指定的解析度。 </p> <p>如果散發者的作業團隊在記錄中看到此錯誤，他們應該檢閱以解析度為基礎的輸出保護原則，並在必要時重新封裝內容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3374 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_ClientCommProcessFailed</span> </td> 
   <td colname="col3"> <p>在使用者端通訊處理期間失敗，例如要求產生、回應處理、錯誤的驗證權杖等。 </p> <p>如果散發者的作業團隊在記錄中看到此錯誤，他們應該檢閱以解析度為基礎的輸出保護原則，並在必要時重新封裝內容。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR：視訊播放值 {#section_7079501250C2487499639F92EC774525}

AVE的視訊編碼器介面會在以下位置傳回這些視訊播放通知： `NATIVE_ERROR` 中繼資料物件。

<table id="table_5EEB1F60E5854452A8B0BABBE9B32651"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> NATIVE_ERROR_CODE中繼資料索引鍵的值 </th> 
   <th colname="col2" class="entry"> NATIVE_ERROR_NAME中繼資料索引鍵的值 </th> 
   <th colname="col3" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> -1 </td> 
   <td colname="col2"><span class="codeph"> END_OF_PERIOD</span> </td> 
   <td colname="col3"> 期間結束。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 0 </td> 
   <td colname="col2"><span class="codeph"> 成功</span> </td> 
   <td colname="col3"> 作業成功。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 1 </td> 
   <td colname="col2"> <span class="codeph"> ASYNC_OPERATION_IN_PROGRESS</span> </td> 
   <td colname="col3"> 非同步操作。 已提出作業要求。 成功/失敗資訊將於稍後提供。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 2 </td> 
   <td colname="col2"><span class="codeph"> EOF</span> </td> 
   <td colname="col3"> 因為檔案結束(EOF)狀況而無法執行作業。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3 </td> 
   <td colname="col2"><span class="codeph"> 解碼器失敗</span> </td> 
   <td colname="col3"> 解碼器在執行階段失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 4 </td> 
   <td colname="col2"><span class="codeph"> DEVICE_OPEN_ERROR</span> </td> 
   <td colname="col3"> 無法開啟硬體解碼器。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 5 </td> 
   <td colname="col2"><span class="codeph"> FILE_NOT_FOUND </span> </td> 
   <td colname="col3"> 找不到資源。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 6 </td> 
   <td colname="col2"><span class="codeph"> GENERIC_ERROR </span> </td> 
   <td colname="col3"> 一般錯誤。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 7 </td> 
   <td colname="col2"><span class="codeph"> IRRECOVERABLE_ERROR </span> </td> 
   <td colname="col3"> 視訊引擎無法復原的錯誤狀況。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 8 </td> 
   <td colname="col2"><span class="codeph"> LOST_CONNECTION_RECOVERABLE </span> </td> 
   <td colname="col3"> 網路錯誤，正在嘗試復原。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 9 </td> 
   <td colname="col2"><span class="codeph"> NO_FIXED_SIZE </span> </td> 
   <td colname="col3"> 無法判斷資源的大小。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 10 </td> 
   <td colname="col2"><span class="codeph"> 未實作 </span> </td> 
   <td colname="col3"> 功能未實作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 11 </td> 
   <td colname="col2"><span class="codeph"> 記憶體不足 </span> </td> 
   <td colname="col3"> 記憶體不足。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 12 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR </span> </td> 
   <td colname="col3"> 剖析媒體檔案時發生錯誤。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 13 </td> 
   <td colname="col2"><span class="codeph"> SIZE_UNKNOWN </span> </td> 
   <td colname="col3"> 資源有大小，但未知。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 14 </td> 
   <td colname="col2"><span class="codeph"> UNDER_FLOW </span> </td> 
   <td colname="col3"> 底流條件。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 15 </td> 
   <td colname="col2"><span class="codeph"> 不支援的_CONFIG </span> </td> 
   <td colname="col3"> 不支援設定。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 16 </td> 
   <td colname="col2"><span class="codeph"> 不支援的操作 </span> </td> 
   <td colname="col3"> 不支援此操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 17 </td> 
   <td colname="col2"><span class="codeph"> WAITING_FOR_INIT </span> </td> 
   <td colname="col3"> 尚未初始化。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 18 </td> 
   <td colname="col2"><span class="codeph"> INVALID_PARAMETER </span> </td> 
   <td colname="col3"> 無效的引數。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 19 </td> 
   <td colname="col2"><span class="codeph"> INVALID_OPERATION</span> </td> 
   <td colname="col3"> 不允許作業。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 20 </td> 
   <td colname="col2"><span class="codeph"> OP_ONLY_ALLOWED_IN_PAUSED_STATE</span> </td> 
   <td colname="col3"> 只有在暫停時才允許此操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 21 </td> 
   <td colname="col2"><span class="codeph"> OP_INVALID_WITH_AUDIO_ONLY_FILE</span> </td> 
   <td colname="col3"> 無法在僅限音訊的檔案上使用作業。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 22 </td> 
   <td colname="col2"><span class="codeph"> 上一步_步驟_搜尋_進行中</span> </td> 
   <td colname="col3"> 上一個搜尋作業仍在進行中。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 23 </td> 
   <td colname="col2"><span class="codeph"> SOURCE_NOT_SPECIFIED </span> </td> 
   <td colname="col3"> 未指定資源。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 24 </td> 
   <td colname="col2"><span class="codeph"> RANGE_ERROR</span> </td> 
   <td colname="col3"> 指定的值超出範圍。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 25 </td> 
   <td colname="col2"><span class="codeph"> 無效的SEEK_TIME</span> </td> 
   <td colname="col3"> 無效的搜尋時間。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 26 </td> 
   <td colname="col2"><span class="codeph"> FILE_STRUCTURE_INVALID</span> </td> 
   <td colname="col3"> 指定的檔案不符合預期的語法。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 27 </td> 
   <td colname="col2"><span class="codeph"> COMPONENT_CREATION_FAILED</span> </td> 
   <td colname="col3"> 無法建立必要元件。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 28 </td> 
   <td colname="col2"><span class="codeph"> DRM_INIT_ERROR</span> </td> 
   <td colname="col3"> 無法建立DRM內容。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 29 </td> 
   <td colname="col2"><span class="codeph"> CONTAINER_NOT_SUPPORT </span> </td> 
   <td colname="col3"> 不支援容器型別。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 30 </td> 
   <td colname="col2"><span class="codeph"> 搜尋失敗</span> </td> 
   <td colname="col3"> 搜尋失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 31 </td> 
   <td colname="col2"><span class="codeph"> CODEC_NOT_SUPPORT</span> </td> 
   <td colname="col3"> 不支援的轉碼器。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 32 </td> 
   <td colname="col2"><span class="codeph"> 網路無法使用</span> </td> 
   <td colname="col3"> 網路無法使用。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 33 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_ERROR</span> </td> 
   <td colname="col3"> 從網路取得資料時發生錯誤。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 34 </td> 
   <td colname="col2"><span class="codeph"> 溢位</span> </td> 
   <td colname="col3"> 溢位。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 35 </td> 
   <td colname="col2"><span class="codeph"> 視訊設定檔不支援</span> </td> 
   <td colname="col3"> 不支援的視訊設定檔。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 36 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_NOT_LOADED</span> </td> 
   <td colname="col3"> 嘗試在HOLD期間或尚未載入的期間執行作業。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 37 </td> 
   <td colname="col2"><span class="codeph"> INVALID_REPLACE_DURATION</span> </td> 
   <td colname="col3"> 指定的取代持續時間無效或延伸超過資料流結尾。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 38 </td> 
   <td colname="col2"><span class="codeph"> CALLED_FROM_WRONG_THREAD</span> </td> 
   <td colname="col3"> 無法從錯誤的執行緒呼叫API。 通常，只適用於應從主執行緒呼叫的API元素。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 39 </td> 
   <td colname="col2"><span class="codeph"> FRAGMENT_READ_ERROR</span> </td> 
   <td colname="col3"> 片段讀取錯誤。 不存在容錯移轉。 引擎將嘗試讀取下一個片段。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 40 </td> 
   <td colname="col2"><span class="codeph"> 已中止</span> </td> 
   <td colname="col3"> 作業被明確的Abort或Destroy呼叫中止。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 41 </td> 
   <td colname="col2"><span class="codeph"> 不支援的_HLS_VERSION</span> </td> 
   <td colname="col3"> 無法播放此版本的HLS媒體。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 42 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_FAIL_OVER</span> </td> 
   <td colname="col3"> 無法容錯移轉。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 43 </td> 
   <td colname="col2"><span class="codeph"> HTTP_TIME_OUT</span> </td> 
   <td colname="col3"> HTTP下載已逾時。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 44 </td> 
   <td colname="col2"><span class="codeph"> 網路關閉 </span> </td> 
   <td colname="col3"> 使用者的網路連線已中斷。 播放可能會隨時停止，並在連線可用時繼續。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 45 </td> 
   <td colname="col2"><span class="codeph"> NO_USABLE_BITRATE_PROFILE</span> </td> 
   <td colname="col3"> 在資料流中找不到可用的位元速率設定檔。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 46 </td> 
   <td colname="col2"><span class="codeph"> BAD_MANIFEST_SIGNATURE</span> </td> 
   <td colname="col3"> 資訊清單的簽章錯誤。 資訊清單簽署測試失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 47 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_LOAD_PLAYLIST</span> </td> 
   <td colname="col3"> 無法載入播放清單。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 48 </td> 
   <td colname="col2"><span class="codeph"> REPLACEMENT_FAILED</span> </td> 
   <td colname="col3"> 插入API中指定的取代無法成功。 這表示插入成功但取代失敗。 如果要取代的資訊清單已從時間軸移除，取代可能會失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 49 </td> 
   <td colname="col2"><span class="codeph"> SWITCH_TO_ASYMETRIC_PROFILE</span> </td> 
   <td colname="col3"> DRM正在切換至非對稱輪廓。 所有設定檔預計都會在期間內對齊。 如果沒有，系統會擲回此警告，而且播放時可能會有跳躍。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 50 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_BACKWARD</span> </td> 
   <td colname="col3"> 即時視窗預期只會向前移動。 如果不會，系統會擲回此警告，且不會讀取視窗。 因此，播放中可能會出現跳躍（或停止/長時間暫停）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 51 </td> 
   <td colname="col2"><span class="codeph"> CURRENT_PERIOD_EXPIRED</span> </td> 
   <td colname="col3"> 即時視窗已移至目前期間以外。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 52 </td> 
   <td colname="col2"><span class="codeph"> CONTENT_LENGTH_MISMATCH</span> </td> 
   <td colname="col3"> HTTP伺服器報告的內容長度與實際媒體大小不符。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 53 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_HOLD</span> </td> 
   <td colname="col3"> 媒體讀取器無法進一步讀取，因為它已經達到setHoldAt API設定的時間。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 54 </td> 
   <td colname="col2"><span class="codeph"> LIVE_HOLD </span> </td> 
   <td colname="col3">媒體讀取器無法載入區段，因為它已經到達即時視窗的結尾。 伺服器向即時視窗新增媒體時，將會繼續載入區段。 達到此狀態通常發生於： 
    <ul id="ul_FCFF658EDA4144E59970B317D6DEB624"> 
     <li id="li_2F6EEEB782D54CD999BC7CC7C0B78B48">此 <span class="codeph"> bufferTime</span> 太高（等於或高於即時視窗持續時間）。 </li> 
     <li id="li_25CE97115ED64E44AA89977FB5F0DCF7">一或多個插入/清除API的組合取代的媒體多於新增的媒體。 </li> 
     <li id="li_1B14716B2157492AB1859306D1250523">下一個期間是有待處理媒體取代的即時期間（由於InsertBy API呼叫） </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 55 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_INTERLEAVING </span> </td> 
   <td colname="col3"> 媒體中的音訊和視訊交錯處理不正確。 這是封裝錯誤。 當差異超過兩秒時會傳送警告。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 56 </td> 
   <td colname="col2"><span class="codeph"> DRM_NOT_AVAILABLE</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 57 </td> 
   <td colname="col2"><span class="codeph"> PLAYBACK_NOT_AUTHORIZED</span> </td> 
   <td colname="col3"> Flash Player中尚未啟用HLS播放。 請參閱AuthorizedFeatures.enableHLSPlayback。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 58 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_SAMPLE_FOUND</span> </td> 
   <td colname="col3"> 解碼器收到無法解碼的錯誤樣本。 這通常不是嚴重錯誤，但表示音訊/視訊可能有問題。 此錯誤的例項太多，表示編碼錯誤或檔案錯誤。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 59 </td> 
   <td colname="col2"><span class="codeph"> RANGE_SPANS_READ_HEAD</span> </td> 
   <td colname="col3"> 開始播放後，插入/取代範圍不應包含讀取標頭。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 60 </td> 
   <td colname="col2"><span class="codeph"> POSTROLL_WITH_LIVE_NOT_ALLOWED</span> </td> 
   <td colname="col3"> 即時媒體上不允許後置滾動插入。 但是，在伺服器將媒體標示為完成之後，就允許這些動作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 61 </td> 
   <td colname="col2"><span class="codeph"> INTERNAL_ERROR</span> </td> 
   <td colname="col3"> 這是一個絕不應該發生的問題。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 62 </td> 
   <td colname="col2"><span class="codeph"> SPS_PPS_FOUND_OUTSIDE_AVCC</span> </td> 
   <td colname="col3"> 資料流未遵循總是將H264 SPS/PPS放入AVCC的封裝建議。 可能會出現搜尋/播放問題。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 63 </td> 
   <td colname="col2"><span class="codeph"> PARTIAL_REPLACEMENT</span> </td> 
   <td colname="col3"> 插入API中指定的取代僅部分完成。 當replaceDuration跨越時間線持續時間時會發生這種情況。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 64 </td> 
   <td colname="col2"><span class="codeph"> RENDITION_M3U8_ERROR</span> </td> 
   <td colname="col3"> 載入轉譯播放清單時發生錯誤。 這僅適用於AVE，不適用於FlashPlayer。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 65 </td> 
   <td colname="col2"><span class="codeph"> NULL_OPERATION</span> </td> 
   <td colname="col3"> 操作沒有執行任何動作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 66 </td> 
   <td colname="col2"><span class="codeph"> SEGMENT_SKIPPED_ON_FAILURE</span> </td> 
   <td colname="col3"> 區段無法播放，因失敗已略過。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 67 </td> 
   <td colname="col2"><span class="codeph"> 不相容的_RENDER_MODE</span> </td> 
   <td colname="col3"> 不相容的轉譯模式。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 68 </td> 
   <td colname="col2"><span class="codeph"> PROTOCOL_NOT_SUPPORT </span> </td> 
   <td colname="col3"> 不支援URL中使用的Web通訊協定。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 69 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR_INCOMPATIBLE_VERSION</span> </td> 
   <td colname="col3"> 剖析媒體檔案時發生錯誤。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 70 </td> 
   <td colname="col2"><span class="codeph"> MANIFEST_FILE_UNEXPECTLY_CHANGED</span> </td> 
   <td colname="col3"> 資訊清單檔案以非預期的方式變更。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 71 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_SPLIT_TIMELINE</span> </td> 
   <td colname="col3"> 無法在時間表上執行分割作業。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 72 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_ERASE_TIMELINE</span> </td> 
   <td colname="col3"> 無法在時間表上執行清除操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 73 </td> 
   <td colname="col2"><span class="codeph"> DID_NOT_GET_NEXT_FRAGMENT</span> </td> 
   <td colname="col3"> 未取得下一個片段。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 74 </td> 
   <td colname="col2"><span class="codeph"> NO_TIMELINE</span> </td> 
   <td colname="col3"> 內部資料結構中不存在時間軸。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 75 </td> 
   <td colname="col2"><span class="codeph"> LISTENER_NOT_FOUND</span> </td> 
   <td colname="col3"> 在內部資料結構中找不到接聽程式。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 76 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_START_ERROR</span> </td> 
   <td colname="col3"> 無法啟動音訊。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 77 </td> 
   <td colname="col2"><span class="codeph"> NO_AUDIO_SINK</span> </td> 
   <td colname="col3"> 內部資料結構中不存在音訊接收器。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 78 </td> 
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
   <td colname="col1"> 81 </td> 
   <td colname="col2"><span class="codeph"> ID3PARSE_ERROR</span> </td> 
   <td colname="col3"> 剖析ID3資料時發生錯誤。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 82 </td> 
   <td colname="col2"><span class="codeph"> 安全性_錯誤 </span> </td> 
   <td colname="col3"> 由於安全性限制，載入內容失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 83 </td> 
   <td colname="col2"><span class="codeph"> 時間軸_TOO_SHORT</span> </td> 
   <td colname="col3"> 時間表持續時間太短。 如果這是即時資料流，可能會發生頻繁的緩衝。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 84 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_START</span> </td> 
   <td colname="col3"> 串流已切換為僅限音訊的串流。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 85 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_END</span> </td> 
   <td colname="col3"> 串流已從純音訊切換為含有視訊的串流。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 87 </td> 
   <td colname="col2"><span class="codeph"> KEY_NOT_FOUND </span> </td> 
   <td colname="col3"> 找不到金鑰。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 88 </td> 
   <td colname="col2"><span class="codeph"> INVALID_KEY</span> </td> 
   <td colname="col3"> 金鑰無效。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 89 </td> 
   <td colname="col2"> <span class="codeph"> KEY_SERVER_NOT_FOUND</span> </td> 
   <td colname="col3"> 金鑰伺服器未傳回金鑰。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 90 </td> 
   <td colname="col2"> <span class="codeph"> MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</span> </td> 
   <td colname="col3"> 無法處理主要資訊清單更新。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 91 </td> 
   <td colname="col2"> <span class="codeph"> 未報告_時間_中斷_已找到</span> </td> 
   <td colname="col3"> 發現未回報的時間(PTS)中斷。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 92 </td> 
   <td colname="col2"> <span class="codeph"> UNMATCHED_AV_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> 找到不相符的音訊和視訊中斷情形。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 93 </td> 
   <td colname="col2"><span class="codeph"> TRICKPLAY_ENDED_DUE_TO_ERROR</span> </td> 
   <td colname="col3">在中播放媒體時發生錯誤 <i>特技播放</i> 模式。 特技播放模式結束，資料流暫停。 呼叫 <span class="codeph"> Play()</span> 以正常模式播放媒體。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 95 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_AHEAD</span> </td> 
   <td colname="col3"> 播放器已離開即時視窗，必須往前搜尋才能趕上進度。 </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR：加密值 {#section_39365E545CAC49B9A4D4678657BB2155}

Adobe視訊引擎的加密模組會在以下位置傳回這些通知： `NATIVE_ERROR` 中繼資料物件。

| NATIVE_ERROR_CODE中繼資料索引鍵的值 | NATIVE_ERROR_NAME中繼資料索引鍵的值 | 含義 |
|---|---|---|
| 300 | `CRYPTO_ALGORITHM_NOT_SUPPORTED` | 不支援正在使用的演演算法。 |
| 301 | `CRYPTO_ERROR_CORRUPTED_DATA` | 資料已損毀。 |
| 302 | `CRYPTO_ERROR_BUFFER_TOO_SMALL` | 緩衝區太小。 |
| 303 | `CRYPTO_ERROR_BAD_CERTIFICATE` | 錯誤的憑證。 |
| 304 | `CRYPTO_ERROR_DIGEST_UPDATE` | 摘要更新。 |
| 305 | `CRYPTO_ERROR_DIGEST_FINISH` | 摘要完成。 |
| 306 | `CRYPTO_ERROR_BAD_PARAMETER` | 引數錯誤。 |
