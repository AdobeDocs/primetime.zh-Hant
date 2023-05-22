---
title: NATIVE_ERROR通知的詳細資訊
description: NATIVE_ERROR通知的詳細資訊
copied-description: true
exl-id: 08121879-d5a6-4224-b08d-9e66fe4d185a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '6888'
ht-degree: 2%

---

# NATIVE_ERROR通知的詳細資訊 {#details-for-the-native-error-notification}

當TVSDK處理本機錯誤時，它將返回以下部分或全部元資料鍵值作為字串。

<table id="table_7F713B7A56024D8DA3C84E449D09CC91"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>元資料密鑰名稱</b></th> 
   <th colname="col2" class="entry"><b>元資料值</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> 本機錯誤代碼</span> </td> 
   <td colname="col2"> <p>來自AVE的本機錯誤代碼。 </p> <p>這些代碼表示以下內容： 
     <ul id="ul_1F33D523DDFE4CE8B4F0DC279FF7E4F8"> 
      <li id="li_07A2D9BEE6364935A61EF3BD4AB6DE27">DRM錯誤（代碼3300到3367）。 這些與等效Flash Player錯誤代碼相同 </li> 
      <li id="li_433BA22DE3504AEEB623598BB4F939FA">視頻播放錯誤（–1到89） </li> 
      <li id="li_B347CB151DB94DE0A1DDEB1B33D2DABA">密碼錯誤（300到307） </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 本機錯誤</span> </td> 
   <td colname="col2">通知的簡短說明(例如， <span class="codeph"> AAXS_InvalidVoucher</span> 或 <span class="codeph"> 解碼器失敗</span>)。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 說明</span> </td> 
   <td colname="col2"> 通知的長描述（例如，廣告解析操作失敗）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR_CODE</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.PSDKErrorCode</span> 數字值（例如「13」）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.PSDKErrorCode</span> 字串(例如， <span class="codeph"> kECNetworkError</span>)。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 警告</span> </td> 
   <td colname="col2"> 警告的說明。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 錯誤</span> </td> 
   <td colname="col2"> 錯誤描述。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>DRM</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_SUBERROR_CODE</span> </td> 
   <td colname="col2"> DRM模組中的次要錯誤。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DRM_ERROR_STRING</span> </td> 
   <td colname="col2"> 錯誤描述。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DRM_ERROR_SERVER_URL</span> </td> 
   <td colname="col2"> TVSDK嘗試與之對話的DRM伺服器的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>廣告清單載入失敗</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_URL</span> </td> 
   <td colname="col2"> 無法載入的內容的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_TYPE</span> </td> 
   <td colname="col2">廣告類型(來自 <span class="codeph"> MediaResource.Type</span> 枚舉)。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_DURATION</span> </td> 
   <td colname="col2"> 廣告持續時間（毫秒）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_ID</span> </td> 
   <td colname="col2"> 分配給廣告的ID。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>檔案錯誤</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 下載錯誤</span> </td> 
   <td colname="col2"> 媒體檔案下載過程中的錯誤描述。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> URL</span> </td> 
   <td colname="col2"> 正在下載的檔案的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 清單_錯誤</span> </td> 
   <td colname="col2"> 清單檔案下載過程中出錯的說明。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 內容錯誤</span> </td> 
   <td colname="col2">片段期間錯誤的描述(例如， <span class="codeph"> ts</span>)下載。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>音頻跟蹤錯誤</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 音頻軌道名稱</span> </td> 
   <td colname="col2"> 無法載入的音頻軌道的名稱，如清單中指定的。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_LANGUAGE</span> </td> 
   <td colname="col2"> 音頻軌道的語言，如清單中指定。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>查找錯誤</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 所需_尋道_週期</span> </td> 
   <td colname="col2"> 期間（整數）的ID。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 所需_尋道_位置</span> </td> 
   <td colname="col2"> <p>尋找位置（毫秒）（雙）。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>雜項</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDITUDE_ERROR_CODE</span> </td> 
   <td colname="col2"> 審核錯誤代碼（數字）。 </td> 
  </tr> 
 </tbody> 
</table>

## 本機錯誤(_E):DRM值 {#section_D240082B93D34902A18C3923C1C717B3}

Adobe視頻引擎的視頻編碼器介面在 `NATIVE_ERROR` 元資料對象。

將DRM錯誤報告給Adobe時，請確保包含 `NATIVE_SUBERROR_CODE` 和 `DRM_ERROR_STRING` 以獲取疑難解答幫助。

>[!TIP]
>
>此清單提供有關錯誤的TVSDK特定資訊。 有關完整說明，請參見 [ActionScript運行時錯誤ActionScriptAdobe Flash Platform參考](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html#3300)。

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
     <li id="li_348FC0F38B11417994119B61C9244076">分銷商的軟體應該做什麼： 
      <ul id="ul_7AFD45CF92454BA4927783FAA628FBC4"> 
       <li id="li_0D9CCE61612643648C12DCDDD252E52A">如果您使用的是GoogleChrome，並且您處於Incognito模式，且Flash Player版本低於11.6，則可能會發生此錯誤。 <p>我們建議播放器檢查瀏覽器的版本號，並建議用戶退出Incognito模式。 </p> </li> 
       <li id="li_1DC6B755BD0840D48BEC92568FD330BA">再次請求許可證。 <p>如果請求成功，則無需記錄或升級。 如果請求不成功，請記錄導致錯誤的內容。 <span class="codeph"> subErrorId</span> 包含行錯誤（如果存在）。 </p> </li> 
      </ul> </li> 
     <li id="li_060B5D60C9BB419CBFA7B062FBCF2632">分銷商應該做的： 
      <ul id="ul_FADB29DBF0DA4A0E8E54134AEB7DCD8A"> 
       <li id="li_FC5B1C04D21E4AECB0EBD9ADD3198504">如果對Flash低於11.6版的Chrome以外的配置重試失敗，則打包中可能出現故障。 </li> 
       <li id="li_A720ECE591254021879B335B81B1F76D">檢查問題是否特定於某些內容並重新打包。 </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3301 </td> 
   <td colname="col2"><span class="codeph"> AAXS_Authentication失敗</span> </td> 
   <td colname="col3"> <p>伺服器無法驗證或授權客戶端。 </p> 
    <ul id="ul_BE77AC1848FB4C09B6318359ACF1B8EE"> 
     <li id="li_6FB37D317D174E8488C5070D20CD241C">分銷商的軟體應採取重新建立用戶憑據所需的任何操作，或指導用戶獲取對內容的訪問權。 </li> 
     <li id="li_BE071D59805B42D38E3E7650BC936417">分發伺服器應確認分發伺服器的授權和身份驗證機制工作正常。 <p>如果分銷商不計畫使用身份驗證或授權功能，他們應檢查違規內容的策略是否需要身份驗證，並參閱診斷策略/許可證差異。 </p> </li> 
    </ul> <p>有關此錯誤代碼的詳細資訊，請參見 <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> DRM錯誤3301的原因和解決方法</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3302 </td> 
   <td colname="col2"><span class="codeph"> AAXS_RequireSSL</span> </td> 
   <td colname="col3"> <p>在Access 4.0及更高版本上，當遠程密鑰URL未使用HTTPS作為方案時，在iOS上引發此錯誤。 需要HTTPS。 </p> 
    <ul id="ul_3D47777BBCA14B67B107FBBE3E37E40C"> 
     <li id="li_7F7BBB27AE754CC39ABAAF9269739C49">如果分發伺服器使用的版本早於Access v4，或版本至少為4但平台不是iOS，則分發伺服器的軟體應記錄該錯誤。 <p>錯誤僅在iOS引發。 </p> </li> 
     <li id="li_D83C427D2A0D47408F723EF7195070B6">如果分發伺服器的軟體至少是Adobe訪問版本4，並且平台是iOS，則分發伺服器必須將他們使用的遠程密鑰伺服器URL更改為HTTPS。 <p>如果它們只使用HTTP，則分發伺服器可能必須設定HTTPS伺服器。 否則，分銷商需要將記錄的資訊提交到Adobe並上報問題。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3303 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentExpired</span> </td> 
   <td colname="col3"> <p>您正在查看的內容已根據內容提供程式設定的規則過期。 subErrorId包含客戶端特定的錯誤或行錯誤。 </p> <p> 
     <ul id="ul_1E4B3B8AE87A4E79997553BB2A0E52B9"> 
      <li id="li_EE3F2EEBF73743B9A38E4FCB7531E275">分發伺服器的軟體應嘗試從伺服器重新獲取一次許可證，以確定是否有新的未過期許可證可用。 <p>如果沒有可用的許可證或許可證已過期，允許用戶獲取新的許可證，或通知用戶內容無法被監視。如果內容已與具有過期/結束日期的策略打包，則許可證伺服器日誌將報告 <span class="codeph"> PolicyEvaluationException</span> 並聲明策略結束日期已失效（伺服器錯誤代碼303）。 檢查伺服器的日誌檔案以驗證。 </p> <p>如果可能，客戶應檢查他們在打包期間使用的策略，以查看該策略是否已過期。 Java命令行工具是： <code> java&nbsp;-jar&nbsp;libs/AdobePolicyManager.jar&nbsp;&nbsp;&nbsp;detail&nbsp;demo.pol</code> </p> </li> 
      <li id="li_50DBE680D8F04E7DA3E29C65A93188E7">分發伺服器應確認許可證到期日期是否按預期配置。 </li> 
     </ul> </p> <p>有關此錯誤代碼的詳細資訊，請參見 <a href="https://forums.adobe.com/thread/1300813" format="https" scope="external"> AMS/FMS使用即時流時3303（內容已過期）?</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3304 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthorizationFailed</span> </td> 
   <td colname="col3">有關此錯誤代碼的詳細資訊，請參見 <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> DRM錯誤3301的原因和解決方法</a>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3305 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerConnection失敗</span> </td> 
   <td colname="col3"> <p>由於網路延遲或客戶端離線，與許可證或域伺服器的連接超時。 通常，subErrorId包含HTTP返回代碼。 </p> 
    <ul id="ul_938C7D8F07F64B4FA71A09DDF37E2E64"> 
     <li id="li_6648EA0049094E369BD9AE9CCA6B148D">分發伺服器的軟體應嘗試連接到已知良好的伺服器。 <p>如果嘗試失敗，則提示用戶重新連接到網路。 如果嘗試成功，請記錄。 </p> </li> 
     <li id="li_2ECA2C04BA08449DA3AD79A52EFAA229">分發伺服器應驗證正在使用的任何許可證和域伺服器是否聯機且可從客戶端網路中看到。 </li> 
    </ul> <p>有關此錯誤代碼的詳細資訊，請參見 <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> DRM 3305 [ServerConnectionFailed]導致和解決問題</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3306 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClientUpdateRequire</span> </td> 
   <td colname="col3"> 使用Android的TVSDK的更新版本。 <p>當前客戶端無法完成請求的操作，但更新的客戶端可能能夠完成請求。 </p> <p>這可能有幾個原因： 
     <ul id="ul_2EC4D42D5273439FA1AFDA1A2578B3D6"> 
      <li id="li_FCA926F5FAED4E7190BE855545AB6ACF">使用的共用域在此客戶端上不可用。 在Chrome上播放時可能會出現這種情況，但不會出現其他瀏覽器，反之亦然。 <p> <p>提示：Chrome使用的PHDS/PHLS密鑰與其他瀏覽器使用的密鑰不同。 有關詳細資訊，請參見 <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>。 </p> </p> </li> 
      <li id="li_3B633FB699234DCEA136E9BE3CC3386D">當在5.0之前的iOS版本上運行時，應用程式正嘗試添加多個DRMSassion。 </li> 
      <li id="li_F7ED993AF0B941A7A27216B4D587A999">只支援版本2時，元資料的版本為3或更高。 </li> 
     </ul> </p> 
     <ul id="ul_EE4AE6AD4F1745A5B5623E53B599DB62"> 
      <li id="li_7A83869D4262443DA35FA1DF8D3097DD">分發伺服器的軟體應提醒用戶並中止操作。 <p>如果軟體有確定升級是否可用的方法，請以適當的方式引導用戶進行升級。 </p> </li> 
      <li id="li_AF9C2711FDE54DA196EB9D2864632000">如果由於共用域而出現此問題，則分發伺服器需要使用Adobe檢查更新的運行時或庫。 <p>對於Flash運行時，分發伺服器可以直接在其應用程式中強制升級。 對於庫，分發伺服器需要獲取更新的庫，重建其應用程式並將其部署到其用戶。 </p> <p>如果由於多個DRMSassion而出現問題，則分銷商需要更新其應用程式以在添加多個DRMSassion之前檢查iOS版本號。 或者，他們可以限制將其申請分發到iOS5及更高版本。 </p> <p>如果由於元資料版本高於版本2而出現問題，則問題可能是元資料損壞。 他們可以嘗試重建元資料並查看結果。 如果他們繼續看到問題，請記錄問題並升級為Adobe。 </p> </li> 
     </ul> <p>有關此錯誤代碼的詳細資訊，請參見 <a href="https://forums.adobe.com/thread/1266675" format="https" scope="external"> 如何修復3306 DRMErrorEvent錯誤代碼</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3307 </td> 
   <td colname="col2"><span class="codeph"> AAXS_內部故障</span> </td> 
   <td colname="col3"> <p>這通常表示Adobe訪問代碼中的錯誤，並且是意外的，除非有已知的錯誤，如下所述。 subErrorId包含客戶端特定的錯誤或行錯誤。 </p> 
    <ul id="ul_79F4A9655A2148519B1E9509C41F78C3"> 
     <li id="li_0E093AB4D6BD489B852279E6C1525A15">如果Flash器是Windows上的Chrome,SWF版本是11.6（版本19或更高版本），則分銷商的軟體應假定用戶按下 <span class="uicontrol"> 拒絕</span> 在資訊欄上，將其視為3368。 </li> 
     <li id="li_0215D1089B344861A2C0A73E1067CFEF">如果3307在瀏覽器不是Chrome或Flash版本不是11.6時發生，則分銷商應升級為Adobe。 </li> 
    </ul> <p>重要提示： <span class="codeph"> 3307:1107296344(FailedToGetBrokerHandle)</span> Chrome瀏覽器版本24-28可能會發生。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3308 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WrongLicenseKey</span> </td> 
   <td colname="col3"> <p>當使用的許可證包含解密內容的錯誤密鑰時，將引發此錯誤。 subErrorId包含客戶端特定的錯誤或行錯誤。 </p> <p>產生此錯誤的方法似乎只有兩種： 
    <ul id="ul_1C955BD74C7843809D1B5A0CDCA5ED7B"> 
     <li id="li_18F0A7FDA6584887AD9DB3EDE54080D8">客戶修改了用於生成許可證的標準Adobe工具（例如許可證伺服器Java框架）。 <p>在這種情況下，許可證包含的密鑰可能與任何內容不對應。 </p> </li> 
     <li id="li_21D04ED1F1FA464785BC297D385766FF">客戶已使用相同的許可證ID頒發多個許可證。 <p>在這種情況下，客戶端上有多個可用的許可證，這些許可證與內容元資料匹配，並且訪問代碼選擇了錯誤的許可證以供使用。 </p> </li> 
    </ul> </p> 
    <ul id="ul_64AEE62BE36946F290067CF475A36ECA"> 
     <li id="li_9EEB2B11A4DA41E78C5840D8FAA81F0D">分發伺服器的軟體應嘗試從伺服器重新獲取許可證。 
      <ul id="ul_ACADC5518B054D0A853AEED2B675DB23"> 
       <li id="li_394835C8731048A5BF7D9370AC12448C">如果沒有可用的許可證或許可證已過期，請為用戶提供獲取新許可證的工作流，或通知用戶無法監視內容並記錄問題。 </li> 
       <li id="li_3FE50518BE53405F9563FA620F7EAD5F">如果這是域綁定內容(對於AIR)，請為用戶提供加入域的方法。 </li> 
      </ul> </li> 
     <li id="li_C80B353C1AEA4E9398241420CB491E84">分發商應： 
      <ul id="ul_B5C50009374C4EED9B2B050B48F5F0F6"> 
       <li id="li_D5E6B760E0BC4B5C949ED1544B398838">驗證他們是否尚未自定義訪問許可證伺服器的許可證頒發部分。 </li> 
       <li id="li_AA8F4E4B6DDD40BA8807C0920A92186B">驗證他們是否為所有許可證頒發唯一的許可證ID。 </li> 
       <li id="li_A2C53FE779AC4FDDB65E00A2C4F43EC4">將問題升級為Adobe。 </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3309 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptedAdditionalHeader </span> </td> 
   <td colname="col3"> <p>如果報頭大於65536位元組，則會發生這種情況。 </p> 
    <ul id="ul_82C0F688519B4F43A764D59A891F1903"> 
     <li id="li_E66AC9149A0649E88A79C5289C12C395">分發商的軟體應記錄導致錯誤的內容。 </li> 
     <li id="li_1C5916A33E7B4DC9968105B9BD20A727">分發商應確認該錯誤可通過特定內容再現。 重新打包損壞的內容。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3310 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppIDMismatch </span> </td> 
   <td colname="col3">Android應用程式與正在使用的應用程式不匹配。 <p>未使用正確的AIR應用程式或FlashSWF。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3311 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppVersionMismatch </span> </td> 
   <td colname="col3"> 沒有使用。 此問題仍可能由AIR的1.x版堆棧生成。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3312 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LicenseIntegrity </span> </td> 
   <td colname="col3"> 要解決此問題，請從伺服器重新下載許可證。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3313 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WriteMicrosafeFailed </span> </td> 
   <td colname="col3"> <p>當系統無法寫入檔案系統時，會出現此問題。 <span class="codeph"> subErrorId</span> 包含特定於客戶端的錯誤或行錯誤。 </p> <p>在MicrosoftWindows上，當加密內容的licenseID或policyID太長時，Active X或NPAPI插件快閃記憶體播放器可能會拋出錯誤3313。 這是因為Windows中的最大路徑長度。 （Pepper插件沒有此問題。） </p> <p>見華生3549660 </p> 
    <ul id="ul_DFD527D1E1224A439766DF7BED878E3B"> 
     <li id="li_FAF8FD98A4E8478CA7A92F770676ADFC">分發伺服器的軟體應提示用戶確認其用戶目錄未鎖定，或者卷已滿或已鎖定。 </li> 
     <li id="li_6D1136EA750A459BBECEEE5F73F527BB">如果分銷商使用的是AIR，而不是Flash，則問題可能由路徑長度限制引起。 <p>分銷商應將其AIR申請的名稱縮短到合理的程度。 另外，以較短的時間再次發佈內容 <span class="codeph"> 許可證ID</span> 和 <span class="codeph"> 策略ID</span>。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3314 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptedDRMetada </span> </td> 
   <td colname="col3"> <p>此錯誤通常表示內容已與testPKI證書打包，而播放器是使用生產PKI構建的，反之亦然。 subErrorId包含客戶端特定的錯誤或行錯誤。 </p> 
    <ul id="ul_A122EF304CAF48A8B4DA1E3F4413E29B"> 
     <li id="li_A9A1A5B23E884C22A71E2DE7535FEB3B">分發商的軟體應記錄導致錯誤的內容。 </li> 
     <li id="li_7AD7F13A4B1B4998A7E49664E7645815">分發者應確認該錯誤可通過特定內容再現。 <p>您可能必須重新打包損壞的內容。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3315 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PermissionDenied </span> </td> 
   <td colname="col3"> <p>當需要3305時，會引發此錯誤代碼的已知錯誤。 有關詳細資訊，請參見 <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> DRM 3305 [ServerConnectionFailed]導致和解決問題</a>。 </p> <p>不允許AIR載入的遠程SWF訪問Flash Access功能。 如果在網路訪問期間出現安全錯誤，也可以拋出此錯誤代碼。 例如，目標伺服器不能通過使用crossdomain.xml連接客戶端，或者無法訪問crossdomain.xml。 </p> <p>有關詳細資訊，請參見 <a href="https://forums.adobe.com/thread/1266592" format="https" scope="external"> DRM錯誤3315可能的根本原因和解決方法</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3316 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NOTUSED_MOVED </span> </td> 
   <td colname="col3"> 是 <span class="codeph"> ADOBECPSHIM_MinorErr_MissingAdobeCPModule</span>。 由於與Flash錯誤代碼衝突而移動到3344。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3317 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LoadAdobeCPF失敗 </span> </td> 
   <td colname="col3"> <p>重要提示：這是一個罕見的錯誤，通常不會在生產環境中出現。 </p> <p>如果確實發生錯誤，可以執行下列操作之一： 
     <ul id="ul_BC435E61623444BB98A86216531DC892"> 
      <li id="li_FA433D0758B642D2AFDCF04906B3FE18">如果使用AIR，請重新安裝。 </li> 
      <li id="li_F08D9AAFF46244F8842DEE5FD9CBBE0A">如果您使用Flash Player，請下載 <span class="codeph"> AdobeCP</span> 中。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3318 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncomplativeAdobeCPVersion </span> </td> 
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
   <td colname="col3"> <p>使用密鑰設定客戶端的過程失敗。 subErrorId包含客戶端特定、伺服器特定或行錯誤。 </p> 
    <ul id="ul_98D919B9060A441AACB6106F6D8E8DA7"> 
     <li id="li_DCAB00A8AC4A426CBBD377374B3F71AE">分發伺服器的軟體應至少重試一次該操作。 <p>如果您在Windows上使用GoogleChrome，請說明如何允許不在沙箱中的插件訪問。 有關詳細資訊，請參閱 <a href="https://helpx.adobe.com/adobe-access/kb/error-3321.html" format="html" scope="external"> GoogleChrome的無沙盒訪問被拒絕</a>。 </p> </li> 
     <li id="li_7FB7681FE32D444BB1BDBA3E5953A2C3">分發伺服器應完成以下任務之一： 
      <ul id="ul_486B64F187C44AE3B4775953A6142836"> 
       <li id="li_095B1D4CD051427CB2BFA7082B454056">如果錯誤跨平台一致，則應將問題升級為Adobe。 </li> 
       <li id="li_0C6EB7B912FA41E59657216498DA3515">如果錯誤僅限於Windows上的Chrome，請引導用戶允許無沙盒插件訪問。 </li> 
      </ul> <p>分銷商應將其SWF更新為版本19或更高版本，並且出現特定於Chrome的3321錯誤，將引發3368錯誤。 錯誤3368可以由分銷商的軟體更具體地處理。 此更改是在Chrome Stable通道26.0.1410.43版中引入的。 </p> <p>提示：錯誤 <span class="codeph"> 3321:1090519056</span> 11.1到11.6版的Flash Player。我們建議您升級到最新的Flash Player版。 </p> </li> 
    </ul> <p>有關詳細資訊，請參見 <a href="https://forums.adobe.com/thread/1277138" format="https" scope="external"> DRM錯誤3321原因和解決方法</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>全局儲存損壞錯誤</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3322 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DeviceBindingFailed </span> </td> 
   <td colname="col3"> <p>設備似乎與初始化時存在的配置不匹配。 subErrorId包含客戶端特定或行錯誤。 </p> <p>分銷商的軟體應完成以下任務之一： 
     <ul id="ul_444401051A2E407B95BC44491E9BB71C"> 
      <li id="li_93493EA05DB44CB1AEC368663F1ABA8D"> <p>如果設備未使用Flash Player，並且正在使用AIR、iOS等，請撥打 <span class="codeph"> DRMManager.resetDRMVouchers()</span>。 </p> <p>如果在開發階段的iOS出現此問題，請讓開發人員確認在從第三方預發行分發系統（例如，HockeyApp）下載的生成和從Xcode下載的本地生成之間切換時是否觀察到此問題。 在從HockeApp分發的生成和從Xcode分發的生成之間切換時，不會完全覆蓋以前安裝的屬性。 此情況可能觸發3322錯誤。 </p> <p>要解決此問題，開發人員應在安裝新生成之前從設備中刪除舊生成。 </p> </li> 
      <li id="li_A5C9633F11584C788A2D9A23CC18FA6D">如果設備正在使用Flash Player，並且3322或3346錯誤代碼無法使用，請參閱Adobe中有關如何以寫程式方式在上重置DRM許可證儲存的說明 <a href="https://forums.adobe.com/message/5535907#5535907" format="https" scope="external"> Chrome中的DRM錯3322/3346/3368（資訊欄問題）</a>。 </li> 
     </ul> </p> <p>此錯誤不應頻繁發生。 在使用漫遊配置檔案的企業環境中，如果用戶正在查看受DRM保護的內容，則當用戶從不同機器登錄時發生的概率錯誤3322增加。 如果可能，分發伺服器應嘗試從用戶獲取此資訊。 </p> <p>如果錯誤頻發，請升級為Adobe。 您必須通知Adobe重置許可證儲存是否解決了問題，並告知Adobe在哪些瀏覽器上發生錯誤。 </p> <p>有關詳細資訊，請參閱以下文章： 
     <ul id="ul_C468409D1EA046178CA7F54DCDCB84EA"> 
      <li id="li_20C8CA3853574CE486F21E7A3667DAB9"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> https://forums.adobe.com/message/5520902</a> </li> 
      <li id="li_6E6F1BD6FE7843449B3E2F06F342EFF7"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> https://forums.adobe.com/message/5535911</a> </li> 
      <li id="li_2BE40E513A0C4BAD900C7B69FEF5D690"><a href="https://forums.adobe.com/message/5748618" format="https" scope="external"> https://forums.adobe.com/message/5748618</a> </li> 
      <li id="li_9C2BD122E3874E2893DD43E082A877E0"><a href="https://forums.adobe.com/message/6061165" format="https" scope="external"> https://forums.adobe.com/message/6061165</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3323 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptGlobalStateStore </span> </td> 
   <td colname="col3"> <p>DRM客戶端使用的檔案已意外修改。 subErrorId包含客戶端特定或行錯誤。 </p> 
    <ul id="ul_96EA771046CA4B2B9FAE24D493F43FF2"> 
     <li id="li_D2693CD8EFEF46108828BA17E3F54FF6">分銷商的軟體應指導用戶以與3322相同的方式重置。 </li> 
     <li id="li_0149B82436B64E28AC2B8C9B0EB09898">如果GlobalStore的故障率高於用戶群硬碟的預期故障率，請將問題上報到Adobe。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3324 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MachineToken無效 </span> </td> 
   <td colname="col3"> 重置此應用程式的DRM本地儲存。 調用DRMManager.resetDRM。 <p>許可證伺服器可能無法連接到證書吊銷清單(CRL)伺服器以刷新其CRL檔案，或者客戶端電腦正在請求已被許可證伺服器吊銷的許可證/身份驗證。 </p> <p>在伺服器日誌中，錯誤代碼111為MachineTokenInvalid。 但是，在客戶端級別，錯誤代碼11被轉換為錯誤代碼3324。 </p> <p>DRM許可證伺服器管理員應檢查客戶的許可證伺服器是否能夠檢索AdobeCRL檔案。 如果客戶使用Tomcat，則客戶可以檢查<span class="filepath"> tomcat/temp/</span> 查看是否有4個CRL檔案的目錄。 </p> 
    <ul id="ul_23B7F1A104AF49E79EA87DB8E15E337E"> 
      <li id="li_855D87F251184FE688A8D5FA0F6C9EF5">如果檔案在此目錄中，請按兩下Windows資源管理器和CRL查看器應用程式中的檔案，確定是否有任何檔案已過期。 </li> 
      <li id="li_58EC4EDA2B5146188A0FF7B33C91E2FD">如果tomcat/temp/中沒有檔案，則可以假定此許可證伺服器由於防火牆/路由問題從未能夠訪問AdobeCRL伺服器。 有關詳細資訊，請參見 <a href="https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_secure_deployment_guidelines.pdf" format="http" scope="external"> 防火牆規則。</a></li>
    </ul> </p> <p>如果CRL檔案不可用或已過期，則必須確認是否可以訪問許可證伺服器。 在客戶的許可證伺服器上開啟網路嗅探器，重新啟動伺服器，並讓客戶端嘗試從伺服器請求許可證。 可以觀察網路通信量，以查看對以下URL端點的調用是否成功： <p>提示：您還可以在瀏覽器中輸入以下CRL URL，以查看是否可以手動下載每個檔案。 </p> 
    <ul id="ul_9B65C7ABBDEC4AC9BF3755FFD3587971"> 
      <li id="li_6867A9050E8D421C9138AC853D1784C9"><a href="https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl</a> </li> 
      <li id="li_6431689260554EAFAFDA2EC31798DCB5"><a href="https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl</a> </li> 
      <li id="li_2939674D0F854ADEB67E45FD216288A2"><a href="https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessRootCA.crl</a> </li> 
      <li id="li_96386E00BE9D4CB99D100057A5F7C6DD">crl3.adobe.com/AdobeSystemsIncorporated FlashAccessRuntime/LatestCRL.crl</li> 
    </ul> </p> <p>如果防火牆規則已開啟且當前沒有3324個錯誤，則可能存在臨時網路問題。 檢查客戶的伺服器日誌，這些日誌可能位於 <span class="codeph"> /tomcat/logs/</span> 目錄，以確定許可證伺服器嘗試獲取證書吊銷清單時是否出錯。 <p>重要提示：在更新CRL檔案時，當大量客戶端（或拆分）將3324錯誤報告到臨時網路問題時，可能會發生錯誤。 網路問題解決後，3324個問題也解決了。 </p> </p> <p>如果CRL檔案的全部4個都位於 <span class="filepath"> tomcat/temp/</span> 目錄，並且客戶端仍收到3324個錯誤代碼，則CRL檔案可能存在檔案訪問問題。 要解決此問題，您可能需要查看日誌並清除現有CRL檔案。 </p> <p>如果沒有伺服器問題，請提示用戶按3322中所述重置。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>伺服器儲存損壞錯誤</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
</tr> 
  <tr> 
   <td colname="col1"> 3325 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptServerStateStore </span> </td> 
   <td colname="col3"> <p>DRM客戶端使用的檔案已意外修改。 <span class="codeph"> subErrorId</span> 包含客戶端特定或行錯誤。 </p> 
    <ul id="ul_860D2402DA61460AB0D938F1116F6D64"> 
     <li id="li_CF368C43452B4265B62ADA3E223894BA">分發伺服器的軟體應再次重試該操作，因為AdobeCP已在內部刪除了違規伺服器儲存，重試應成功。 如果重試失敗，請記錄問題。 </li> 
     <li id="li_51A5803A1F754970BB4EBD6494F5DC96">如果重試失敗的速率大於用戶群硬碟的預期失敗速率，請將問題升級為Adobe。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3326 </td> 
   <td colname="col2"><span class="codeph"> 檢測到AAXS_StoreParketingDetected </span> </td> 
   <td colname="col3"> 呼叫 <span class="codeph"> DRManager.resetDRM</span>。 <p>許可證儲存已被篡改/損壞，無法再使用。 </p> <p>分銷商的軟體應指導用戶以與3322中所述的相同方式重置。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3327 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClockPampertingDetected </span> </td> 
   <td colname="col3"> 修復時鐘或獲取 <span class="codeph"> 授權/許可/域</span> 再次獲得許可。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>驗證/許可證/域伺服器錯誤</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3328 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerErrorTryAain </span> </td> 
   <td colname="col3"> <p>這是伺服器端錯誤，伺服器無法從客戶端完成請求。 例如，當伺服器忙、HTTP/500、伺服器沒有解密請求所需的密鑰等時，可能會發生此錯誤。 </p> <p>在客戶身上，無法確定出了什麼問題。 客戶必須查看Adobe訪問伺服器日誌，這些日誌通常被調用 <span class="codeph"> AdobeFlashAccess.log</span>，以確定出了什麼問題。 日誌中始終存在描述性堆棧跟蹤以指示問題。 <span class="codeph"> subErrorId</span> 包含特定於伺服器或線路錯誤。 </p> <p>分發伺服器應查看伺服器日誌以確定哪個伺服器正在發送此錯誤。 對於具有子錯誤代碼101的3328錯誤，伺服器無法解密該請求。 客戶必須驗證安裝在許可證伺服器上的許可證/傳輸伺服器證書是否匹配並與打包期間使用的證書對應。 </p> <p>此外，如果客戶正在使用「參考實施」，則必須確保 <span class="codeph"> flashaccess refimpl.properties</span> 指定主證書和附加證書的檔案。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3329 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ApplicationSpecificError </span> </td> 
   <td colname="col3"> <p>應用程式特定的子錯誤代碼未知，無法Flash Access。 <span class="codeph"> subErrorId</span> 包含發佈程式自定義許可證伺服器中的伺服器特定錯誤。 伺服器在特定於應用程式的命名空間中返回錯誤。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3330 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NeedAuthentication </span> </td> 
   <td colname="col3"> <p>當內容配置為要求客戶端在獲取許可證之前進行身份驗證時，會出現此錯誤。 </p> 
    <ul id="ul_712D29B8B5A6401FB014C4A283918E32"> 
     <li id="li_2D56905EB50D4FDEAD69CA8EAE38AD1A">分銷商的軟體應驗證用戶，然後再次獲取許可證。 <p>如果您的服務不打算使用身份驗證，請記錄導致此錯誤的內容的標識。 </p> </li> 
     <li id="li_B3BCF899B8BE41C7A4F7CF84B0503483">此錯誤不應要求升級，除非不應將內容配置為需要身份驗證。 <p>在這種情況下，使用適當的策略重新打包違規內容。 如果內容打包正確，請參閱診斷策略/許可證差異。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>上面未涵蓋的許可證實施錯誤</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
</tr> 
  <tr> 
   <td colname="col1"> 3331 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentNotYetValid </span> </td> 
   <td colname="col3"> <p>獲取的許可證尚未生效。 要解決此問題，請檢查客戶端時鐘是否設定不正確。 要設定客戶端時鐘，請重新打包內容或修改許可證伺服器配置。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3332 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CachedLicenseExpired </span> </td> 
   <td colname="col3"> 從伺服器重新獲取許可證。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3333 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PlaybackWindowExpired </span> </td> 
   <td colname="col3"> <p>您必須通知用戶在策略過期之前無法播放此內容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3334 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMPlatform </span> </td> 
   <td colname="col3"> <p>不允許此平台播放內容，因為例如，內容提供商已配置Adobe訪問以拒絕平台上的Adobe訪問內容，或者共用域綁定許可證綁定到用於不同分區的共用域令牌。 </p> <p>如果內容未通過使用適當（CDM功能選通）打包器證書打包，CDM可能會引發此錯誤。 </p> <p>如果內容與不正確的PHDS/PHLS證書打包，則內容可能在Chrome中工作，但不能在其他瀏覽器中工作（反之亦然）。 <p>提示：這是因為Chrome使用不同的PHDS/PHLS證書。 </p>要確認正在使用哪個證書，請轉儲內容元資料的詳細資訊並查找 <i>收件人證書</i>。 有關詳細資訊，請參見 <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3335 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMVersion </span> </td> 
   <td colname="col3"> 升級到適用於Android的TVSDK的最新版本。 <p>要解決此問題，請完成以下任務之一： 
     <ul id="ul_BF1742948BC9461CB8686DE70124D3CD"> 
      <li id="li_690D440C94CC45A0AE55EC319B1C4C23">升級AIR </li> 
      <li id="li_CDD20251C881466E88BE7BBB53D61EBC">對於Flash Player，請升級AdobeCP模組並重試播放。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3336 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidRuntimePlatform </span> </td> 
   <td colname="col3"> <p>不允許此平台播放內容，因為例如，內容提供商已配置「訪問」以拒絕平台上的FP/AIR內容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3337 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidRuntimeVersion </span> </td> 
   <td colname="col3"> 升級到Android的TVSDK的最新版本。 <p>如果內容或伺服器配置為拒絕播放特定版本的Flash或AIR運行時，則會發生這種情況。 </p> 
    <ul id="ul_B0732D941256483CABBDD30C9BF43249"> 
     <li id="li_72782B1D638F48C0B87084689FB9C798">如果用戶在可升級Flash的作業系統上，分發伺服器的軟體應提示用戶升級Flash，然後重試。 否則建議用戶使用其他電腦。 </li> 
     <li id="li_1E3FD93CE39E43F2B7D961299B1211DA">如果懷疑出現錯誤3337s，請確定是否針對特定內容發生錯誤並重新打包該內容。 如果內容打包正確，請參閱診斷策略/許可證差異 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3338 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnknownConnectionType </span> </td> 
   <td colname="col3"> <p>無法檢測連接類型，並且策略要求您開啟「輸出保護」。 只有在內容打包以需要數字或模擬輸出保護時，才會出現此問題。 </p> <p>11.8.800.168版以前的Flash Player版本中出現問題，導致錯誤338偶爾出現在策略指示內容保護為 <span class="codeph"> 使用（如果可用）</span>。 此問題已在11.8.800.168版和更高版本中解決。 </p> 
    <ul id="ul_4B6CA26A53F84838B5B95400925464D4"> 
     <li id="li_CBD890F467E449EBB5116E1561252058">分銷商的軟體選擇不需要輸出保護的內容的變體（例如HD流的SD變體）。 <p>如果錯誤3338發生在 <span class="codeph"> 使用_IF_AVAILABLE </span> 內容，檢查播放器版本號。 如果播放器版本小於11.8.800.168，建議用戶升級Flash Player。 如果11.8.800.168以上版本發生錯誤338，請記錄導致錯誤的內容。 </p> </li> 
     <li id="li_62886C1D96264B129928A7E29E6C70E1">分發伺服器應檢查導致此錯誤的內容，並驗證內容的策略是否正在設定 <span class="codeph"> 無保護</span> 或 <span class="codeph"> 使用_IF_AVAILABLE</span> 模擬和數字輸出。 <p>如果內容不經意地與 <span class="codeph"> 無輸出(_O)</span> 或 <span class="codeph"> 必需</span>，重新打包內容。 如果內容打包正確，請參閱診斷策略/許可證差異。 否則，請升級為Adobe。 </p> </li> 
    </ul> <p>有關詳細資訊，請參見 <a href="https://forums.adobe.com/message/5518688" format="https" scope="external"> 當DRM策略設定為USE_IF_AVAILABLE時，會遇到意外的3338錯誤？</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3339 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogPlaybackAllowed </span> </td> 
   <td colname="col3"> 無法在模擬設備上回放。 要解決此問題，請連接數字設備。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3340 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogProtectionAvail </span> </td> 
   <td colname="col3"> 無法回放內容，因為連接的模擬外部顯示設備（監視器/電視）沒有正確的功能（例如，設備沒有Macrovision或ACP）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3341 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalPlaybackAllowed </span> </td> 
   <td colname="col3"> 無法在數字設備上回放內容。 <p>重要提示：此問題不應在生產環境中發生，因為內容發佈者不應禁止數字回放。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3342 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalProtectionAvail </span> </td> 
   <td colname="col3"> 連接的數字外部顯示設備（顯示器/電視）沒有正確的功能。 例如，設備沒有HDCP。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3343 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IntegrityVerification失敗 </span> </td> 
   <td colname="col3"> <p>不適用於Android。 </p> <p>當前已知在發佈新版本的Flash後，此錯誤最初會發生。 出現此情況是因為Flash在Flash開啟時升級，這會使Flash處於一個錯誤狀態，直到瀏覽器重新啟動。 </p> 
    <ul id="ul_A0AC4A77550E40409A04BD33748EA987"> 
     <li id="li_F41C1ABD838D41ABB0DF65093E664A29">分銷商的軟體應完成以下任務： 
      <ul id="ul_79B2AB1372074D448F129851AA24F985"> 
       <li id="li_B93EDD263D78434FAF198A01938D3508">建議用戶關閉或退出所有瀏覽器，然後重新開啟。 </li> 
       <li id="li_ADFBCFA66AD849E18DB390455458528E">檢查Flash的版本是否為當前版本。 <p>如果版本不是最新版本，建議客戶升級，關閉其瀏覽器中的所有頁籤，然後重新開啟。 </p> </li> 
      </ul> </li> 
     <li id="li_281B54582B5949AEA7D166246917EE41">如果瀏覽器成功重新啟動後出現錯誤，請升級到Adobe。 <p>發佈新版本時，我們建議您與Adobe支援部門聯繫，以查看後台更新問題是否已解決。 </p> </li> 
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
   <td colname="col3"> <p>不適用於Android。 </p> <p>當部分Flash或AIR未正確安裝時，將發生此錯誤。 </p> <p>分銷商的軟體應執行以下操作之一： 
     <ul id="ul_D1188E2D4FDF4BD89A04F5629D75D981"> 
      <li id="li_B33FBCA5D4534D668B86A5E93DB3A809">要求用戶卸載並重新安裝AIR。 </li> 
      <li id="li_B7D2388E9FA84C26AF1C87B48AF9EF16">對於Flash Player，呼叫 <span class="codeph"> System.update</span>。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3346 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MigrationFailed </span> </td> 
   <td colname="col3"> 
    <ul id="ul_518AD4931CC64EB3A962DD451E6C5067"> 
     <li id="li_3C44F0740B08490E9C62D89C40B57DC2">分銷商的軟體應執行以下操作之一： 
      <ul id="ul_7D90526684BF4EB2BBADCF598AA13086"> 
       <li id="li_D15B4BEDAF7340F6B9BC886DF6E346EC">如果AIR，打電話 <span class="codeph"> DRMManager.resetDRMVouchers()</span> </li> 
       <li id="li_40A51D35408249CFA28DBC49FDA3408B">如果Flash因錯誤3322或3346錯誤代碼而不可用，則用戶應轉到 <a href="https://forums.adobe.com/message/5535907#5535907" format="http" scope="external"> https://forums.adobe.com/message/5535907#5535907</a> 並按照Adobe文章的說明以寫程式方式重置其DRM許可證儲存。 </li> 
      </ul> </li> 
     <li id="li_0464471E4A094C80BF2986694341921A">如果此錯誤經常發生，分發伺服器應提供有關頻率播放器版本和要Adobe的瀏覽器版本的詳細資訊。 </li> 
    </ul> <p>有關詳細資訊，請參閱以下論壇文章： 
     <ul id="ul_44E0077FEAA749CC9549BF3846065304"> 
      <li id="li_2BE3B2443380415DA73B7AA3B6547B31"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> Chrome中的DRM錯3322/3346/3368（資訊欄問題）</a> </li> 
      <li id="li_4E5C7414756644E1AB78BE7B8112228C"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> 硬體更改後出現3322或3346錯誤</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3347 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InfedDeviceCapability </span> </td> 
   <td colname="col3"> <p>此錯誤的主要含義是許可證具有客戶端的DRM證書表示它不能滿足的約束。 下列「硬體功能」是在發出客戶端DRM證書時定義的： 
     <ul id="ul_1EB6F1469C244CF0BA52C212495C053D"> 
      <li id="li_646043CE045C4DE2BBC939E1F4963DFE"><b>非用戶可訪問匯流排</b>。 如果 <b>真</b>，解密的媒體從不流經匯流排或進入主儲存器，應用程式可以訪問該主儲存器。 <p>如果 <b>假</b>，解密後，應用程式可以訪問內容。 </p> </li> 
      <li id="li_02AAECAF4D35447BA10554541B46DE67"><b>硬體信任根</b>。 如果 <b>真</b>，啟動時在設備上載入的所有軟體都通過僅在硬體中可用的密鑰或摘要進行驗證。 <p>當針對客戶機的DRM證書開啟許可證時，在客戶端上檢查這兩個約束，並且立即失敗。 在發放許可證之前，還可以在伺服器端檢查這些約束。 </p> </li> 
     </ul> </p> <p>此錯誤的次要含義是許可證已設定「Jailbreak Enforcement」策略，並且在設備上檢測到了越獄。 此檢查在客戶端定期完成，在伺服器端無法檢查。 </p> <p>分銷商可以更新策略並取消限制。 對於設備功能策略，使用 <span class="codeph"> -devCapabilitiesV1</span> 標籤，沒有參數。 對於越獄執行，設定 <span class="codeph"> policy.enforceJailbreak=false</span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3348 </td> 
   <td colname="col2"><span class="codeph"> AAXS_HardStopIntervalExpired </span> </td> 
   <td colname="col3"> 硬停止間隔已過期。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3349 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionTooHigh </span> </td> 
   <td colname="col3"> 伺服器運行的版本高於客戶端支援的最高版本。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3350 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionTooLow </span> </td> 
   <td colname="col3"> 伺服器運行的版本低於客戶端支援的最低版本。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3351 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainToken無效 </span> </td> 
   <td colname="col3"> 域令牌無效。 要解決此問題，請再次向域註冊。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3352 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenTooOld </span> </td> 
   <td colname="col3"> 域令牌早於許可證所需的令牌。 要解決此問題，請再次向域註冊。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3353 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenTooNew </span> </td> 
   <td colname="col3"> 域令牌比許可證所需的令牌新。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3354 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenExpired </span> </td> 
   <td colname="col3"> 域令牌已過期。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3355 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainJoinFailed </span> </td> 
   <td colname="col3"> 域加入失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3356 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoEquotRoot </span> </td> 
   <td colname="col3"> 找不到V3葉許可證的根許可證。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3357 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoValidEmbeddedLicense </span> </td> 
   <td colname="col3"> 找不到有效的嵌入式許可證。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3358 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoACPProtectionAvail </span> </td> 
   <td colname="col3"> 無法回放，因為連接的模擬設備沒有ACP保護。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3359 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoCGMSAProtectionAvail </span> </td> 
   <td colname="col3"> 無法回放，因為連接的模擬設備沒有CGMS-A保護。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3360 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainRegistrationRequired </span> </td> 
   <td colname="col3"> 內容需要域註冊。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3361 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NotRegisteredToDomain </span> </td> 
   <td colname="col3"> 電腦未註冊到指定元資料的域。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3362 </td> 
   <td colname="col2"><span class="codeph"> AAXS_OperationTimeoutError </span> </td> 
   <td colname="col3"> 非同步操作所花費的時間超過 <span class="codeph"> maxOperationTimeout</span>。 僅由iOSDRMNative Framework返回。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3363 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnsupportedIOSPlaylistError </span> </td> 
   <td colname="col3"> 傳入的M3U8播放清單包含不受支援的內容。 僅由iOSDRMNative Framework返回。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3364 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDeviceId </span> </td> 
   <td colname="col3"> <p>框架請求了設備ID，但返回的值為空。 </p> <p>用戶不應選擇 <span class="uicontrol"> 允許受保護內容的標識符</span> 複選框。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3365 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncognitoModeNotAllowed </span> </td> 
   <td colname="col3"> <p>此瀏覽器/平台組合不允許在Incognito模式下播放受DRM保護的內容。 </p> <p>分發伺服器的軟體應建議用戶退出Incognito模式或使用其他瀏覽器。 有關詳細資訊，請參見 <a href="https://forums.adobe.com/thread/1266622" format="https" scope="external"> DRM錯誤3365原因和解決方法</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3366 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadParameter </span> </td> 
   <td colname="col3"> <p>主機運行時使用錯誤的參數調用了Access庫。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3367 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadSignature </span> </td> 
   <td colname="col3"> m3u8清單簽名失敗。 僅由iOSDRMNative Framework或AVE返回。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3368 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UserSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>用戶取消了操作或輸入了不允許訪問系統的設定。 </p> <p>僅當SWF版本為19或更高版本時，才會引發此錯誤。 為了向後相容，當SWF為版本18或更早版本時，會拋出3321。 </p> <p>分銷商的軟體應指導用戶解釋如何允許無沙盒插件訪問。 有關詳細資訊，請參見 <a href="https://helpx.adobe.com/adobe-access/kb/error-3321.html" format="html" scope="external"> GoogleChrome的無沙盒訪問被拒絕</a> 和 <a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> Chrome中的DRM錯3322/3346/3368（資訊欄問題）</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3369 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InterfaceNotAvailable</span> </td> 
   <td colname="col3"> <p>所需的瀏覽器介面不可用。 此問題僅發生在Pepper上。 Flash插件和瀏覽器版本之間可能不匹配。 </p> <p>分發程式的軟體應指導用戶確保安裝了最新版本的瀏覽器。 </p> <p> 如果此錯誤的發生率在增加，並且對應於正在發佈的瀏覽器更新，則升級為Adobe。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3370 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentIdSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>用戶已禁用 <span class="uicontrol"> 允許受保護內容的標識符</span> 的子菜單。 </p> <p>提示：Pepper 13.0.0.x或更高版本出現此錯誤。 </p> <p>分銷商的軟體應引導用戶啟用 <span class="uicontrol"> 允許受保護內容的標識符</span> 的子菜單。 </p> <p>分銷商的操作團隊應指導用戶啟用 <span class="uicontrol"> 允許受保護內容的標識符</span> 的子菜單。 </p> <p>有關詳細資訊，請參見 <a href="https://forums.adobe.com/message/6518323#6518323" format="https" scope="external"> https://forums.adobe.com/message/6518323#6518323</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3371 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoOPConstraintInPixel</span><span class="codeph"> 約束</span> </td> 
   <td colname="col3"> <p>基於許可證中的輸出保護約束的解析格式不正確。 </p> <p>分發伺服器的軟體應顯示錯誤消息。 要求用戶向具有內容標題的分銷商報告問題。 </p> <p>分發伺服器應使用有效的策略重新打包內容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3372 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ResolutionLagerThanMaxResolution</span> </td> 
   <td colname="col3"> <p>內容的解析度大於輸出保護約束中指定的最大解析度。 </p> <p>如果分發商的操作團隊在日誌中看到此錯誤，則他們應檢查基於解析度的輸出保護策略，並在必要時重新打包內容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3373 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_DisplayResolutionLagerThanConstrain</span> </td> 
   <td colname="col3"> <p>內容的解析度大於當前活動的輸出保護約束所指定的解析度。 </p> <p>如果分發商的操作團隊在日誌中看到此錯誤，則他們應檢查基於解析度的輸出保護策略，並在必要時重新打包內容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3374 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_ClientCommProcessFailed</span> </td> 
   <td colname="col3"> <p>在客戶端通信處理期間失敗，例如請求生成、響應處理、錯誤的身份驗證令牌等。 </p> <p>如果分發商的操作團隊在日誌中看到此錯誤，他們應檢查基於解析度的輸出保護策略，並在必要時重新打包內容。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 本機錯誤(_E):視頻播放值 {#section_7079501250C2487499639F92EC774525}

AVE的Video Encoder介面將返回以下視頻播放通知 `NATIVE_ERROR` 元資料對象。

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
   <td colname="col2"><span class="codeph"> 期末</span> </td> 
   <td colname="col3"> 期末。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 0 </td> 
   <td colname="col2"><span class="codeph"> 成功</span> </td> 
   <td colname="col3"> 操作成功。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 1 </td> 
   <td colname="col2"> <span class="codeph"> ASYNC_OPERATION_IN_PROGRESS</span> </td> 
   <td colname="col3"> 非同步操作。 已發出操作請求。 以後將提供成功/失敗資訊。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 2 </td> 
   <td colname="col2"><span class="codeph"> EOF</span> </td> 
   <td colname="col3"> 由於檔案結束(EOF)條件，無法執行操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3 </td> 
   <td colname="col2"><span class="codeph"> 解碼器失敗</span> </td> 
   <td colname="col3"> 解碼器在運行時失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 4 </td> 
   <td colname="col2"><span class="codeph"> 設備開啟錯誤</span> </td> 
   <td colname="col3"> 無法開啟硬體解碼器。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 5 </td> 
   <td colname="col2"><span class="codeph"> 找不到檔案 </span> </td> 
   <td colname="col3"> 找不到資源。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 6 </td> 
   <td colname="col2"><span class="codeph"> 泛型_錯誤 </span> </td> 
   <td colname="col3"> 一般錯誤。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 7 </td> 
   <td colname="col2"><span class="codeph"> 不可恢復_錯誤 </span> </td> 
   <td colname="col3"> 視頻引擎無法從中恢復的錯誤條件。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 8 </td> 
   <td colname="col2"><span class="codeph"> LOST_CONNECTION_RECOVERABLE </span> </td> 
   <td colname="col3"> 網路錯誤，正在嘗試恢復。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 9 </td> 
   <td colname="col2"><span class="codeph"> 無固定大小 </span> </td> 
   <td colname="col3"> 無法確定資源的大小。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 10 </td> 
   <td colname="col2"><span class="codeph"> 未實現(_I) </span> </td> 
   <td colname="col3"> 功能未實現。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 11 </td> 
   <td colname="col2"><span class="codeph"> 記憶體不足 </span> </td> 
   <td colname="col3"> 記憶體不足。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 12 </td> 
   <td colname="col2"><span class="codeph"> 分析錯誤 </span> </td> 
   <td colname="col3"> 分析媒體檔案時出錯。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 13 </td> 
   <td colname="col2"><span class="codeph"> 大小未知 </span> </td> 
   <td colname="col3"> 資源有大小，但未知。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 14 </td> 
   <td colname="col2"><span class="codeph"> 下(_F) </span> </td> 
   <td colname="col3"> 下流情況。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 15 </td> 
   <td colname="col2"><span class="codeph"> 不支援的_配置 </span> </td> 
   <td colname="col3"> 不支援配置。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 16 </td> 
   <td colname="col2"><span class="codeph"> 不支援的_OPERATION </span> </td> 
   <td colname="col3"> 不支援操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 17 </td> 
   <td colname="col2"><span class="codeph"> 等待初始化 </span> </td> 
   <td colname="col3"> 尚未初始化。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 18 </td> 
   <td colname="col2"><span class="codeph"> 無效參數 </span> </td> 
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
   <td colname="col3"> 僅在暫停時允許該操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 21 </td> 
   <td colname="col2"><span class="codeph"> OP_INVALID_WITH_AUDIO_ONLY_FILE</span> </td> 
   <td colname="col3"> 操作不能僅用於音頻檔案。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 22 </td> 
   <td colname="col2"><span class="codeph"> PREVIOUS_STEP_SEEK_IN_PROGRESS</span> </td> 
   <td colname="col3"> 上一尋道操作仍在進行中。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 23 </td> 
   <td colname="col2"><span class="codeph"> 未指定源 </span> </td> 
   <td colname="col3"> 未指定資源。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 24 </td> 
   <td colname="col2"><span class="codeph"> 範圍_錯誤</span> </td> 
   <td colname="col3"> 指定的值超出範圍。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 25 </td> 
   <td colname="col2"><span class="codeph"> 無效_SEEK_TIME</span> </td> 
   <td colname="col3"> 無效的查找時間。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 26 </td> 
   <td colname="col2"><span class="codeph"> FILE_STRUCTURE_INVALID</span> </td> 
   <td colname="col3"> 指定的檔案不符合預期語法。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 27 </td> 
   <td colname="col2"><span class="codeph"> 元件建立失敗</span> </td> 
   <td colname="col3"> 無法建立基本元件。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 28 </td> 
   <td colname="col2"><span class="codeph"> DRM_INIT_ERROR</span> </td> 
   <td colname="col3"> 無法建立DRM上下文。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 29 </td> 
   <td colname="col2"><span class="codeph"> CONTAINER_NOT_SUPPORTED </span> </td> 
   <td colname="col3"> 不支援容器類型。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 30 </td> 
   <td colname="col2"><span class="codeph"> 查找失敗</span> </td> 
   <td colname="col3"> 查找失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 31 </td> 
   <td colname="col2"><span class="codeph"> CODEC_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> 不支援的編解碼器。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 32 </td> 
   <td colname="col2"><span class="codeph"> 網路不可用</span> </td> 
   <td colname="col3"> 網路不可用。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 33 </td> 
   <td colname="col2"><span class="codeph"> 網路錯誤</span> </td> 
   <td colname="col3"> 從網路獲取資料時出錯。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 34 </td> 
   <td colname="col2"><span class="codeph"> 溢出</span> </td> 
   <td colname="col3"> 溢出。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 35 </td> 
   <td colname="col2"><span class="codeph"> 支援VIDEO_PROFILE_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> 不支援的視頻配置檔案。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 36 </td> 
   <td colname="col2"><span class="codeph"> 期間未載入</span> </td> 
   <td colname="col3"> 嘗試在HOLD期間或尚未載入的期間執行操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 37 </td> 
   <td colname="col2"><span class="codeph"> 無效_REPLACE_DURATION</span> </td> 
   <td colname="col3"> 指定的替換持續時間無效或延伸到流的末尾。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 38 </td> 
   <td colname="col2"><span class="codeph"> 調用的_FROM_WRONG_THREAD</span> </td> 
   <td colname="col3"> 無法從錯誤的線程調用API。 大多數情況下，應僅從主線程調用的API元素。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 39 </td> 
   <td colname="col2"><span class="codeph"> FRAGMENT_READ_ERROR</span> </td> 
   <td colname="col3"> 片段讀取錯誤。 不存在故障轉移。 引擎將嘗試讀取下一個片段。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 40 </td> 
   <td colname="col2"><span class="codeph"> 中止</span> </td> 
   <td colname="col3"> 該操作被顯式中止或銷毀調用中止。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 41 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_HLS_VERSION</span> </td> 
   <td colname="col3"> 無法播放此版本的HLS媒體。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 42 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_FAIL_OVER</span> </td> 
   <td colname="col3"> 無法故障轉移。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 43 </td> 
   <td colname="col2"><span class="codeph"> HTTP_TIME_OUT</span> </td> 
   <td colname="col3"> HTTP下載超時。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 44 </td> 
   <td colname="col2"><span class="codeph"> 網路(_D) </span> </td> 
   <td colname="col3"> 用戶的網路連接已關閉。 播放可以隨時停止，並在連接可用時恢復。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 45 </td> 
   <td colname="col2"><span class="codeph"> NO_USABLE_BITRATE_PROFILE</span> </td> 
   <td colname="col3"> 在流中找不到可用比特率配置檔案。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 46 </td> 
   <td colname="col2"><span class="codeph"> BAD_MANIFEST_SIGNATURE</span> </td> 
   <td colname="col3"> 清單的簽名錯誤。 未通過清單簽名test。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 47 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_LOAD_PLAYLIST</span> </td> 
   <td colname="col3"> 無法載入播放清單。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 48 </td> 
   <td colname="col2"><span class="codeph"> 替換失敗</span> </td> 
   <td colname="col3"> 在插入API中指定的替換無法成功。 這意味著插入成功，但替換未成功。 如果要替換的清單已從時間線中刪除，則替換可能失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 49 </td> 
   <td colname="col2"><span class="codeph"> SWITCH_TO_ASYMMETRIC_PROFILE</span> </td> 
   <td colname="col3"> DRM正在切換到非對稱配置檔案。 所有配置檔案預計在持續時間內對齊。 否則，將引發此警告，並且回放中可能出現跳轉。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 50 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_BACKWARD</span> </td> 
   <td colname="col3"> 「即時」窗口只能向前移動。 否則，將引發此警告，並且不會讀取窗口。 因此，回放中可能會出現跳轉（或停止/長暫停）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 51 </td> 
   <td colname="col2"><span class="codeph"> 當前期間已到期</span> </td> 
   <td colname="col3"> 即時窗口已超出當前時段。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 52 </td> 
   <td colname="col2"><span class="codeph"> 內容長度不匹配</span> </td> 
   <td colname="col3"> HTTP伺服器報告的內容長度與實際媒體大小不匹配。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 53 </td> 
   <td colname="col2"><span class="codeph"> 期間_保持</span> </td> 
   <td colname="col3"> 媒體讀取器無法進一步讀取，因為它已達到setHoldAt API設定的時間。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 54 </td> 
   <td colname="col2"><span class="codeph"> 即時保留(_H) </span> </td> 
   <td colname="col3">介質讀取器無法載入段，因為它已到達即時窗口的末尾。 當伺服器將新媒體廣告到即時窗口時，將恢復段載入。 通常在以下情況下達到此狀態： 
    <ul id="ul_FCFF658EDA4144E59970B317D6DEB624"> 
     <li id="li_2F6EEEB782D54CD999BC7CC7C0B78B48">的 <span class="codeph"> 緩衝區時間</span> 過高（等於或高於即時窗口持續時間）。 </li> 
     <li id="li_25CE97115ED64E44AA89977FB5F0DCF7">一個或多個插入/擦除API的組合替換了比它添加的介質多的介質。 </li> 
     <li id="li_1B14716B2157492AB1859306D1250523">下一個時段是具有掛起的介質替換（由於InsertBy API調用）的即時時段 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 55 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_INTERLEARG </span> </td> 
   <td colname="col3"> 媒體中的音頻和視頻交織操作不正確。 這是打包錯誤。 當差值超過兩秒時，將發出警告。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 56 </td> 
   <td colname="col2"><span class="codeph"> DRM_NOT_AVAILABLE</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 57 </td> 
   <td colname="col2"><span class="codeph"> 播放_未授權</span> </td> 
   <td colname="col3"> 未在Flash Player中啟用HLS回放。 請參見AuthorizedFeatures.enableHLSPlayback。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 58 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_SAMPLE_FOUND</span> </td> 
   <td colname="col3"> 解碼器接收了無法解碼的壞樣本。 這通常不是致命錯誤，但表示音頻/視頻中可能出現故障。 此錯誤的實例過多表示編碼錯誤或檔案錯誤。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 59 </td> 
   <td colname="col2"><span class="codeph"> RANGE_SPANS_READ_HEAD</span> </td> 
   <td colname="col3"> 播放開始後，「插入/替換」範圍不應包含讀取頭。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 60 </td> 
   <td colname="col2"><span class="codeph"> POSTURL_WITH_LIVE_NOT_ALLOWED</span> </td> 
   <td colname="col3"> 在即時媒體上不允許插入卷後。 但是，在伺服器將介質標籤為完整後，才允許使用這些介質。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 61 </td> 
   <td colname="col2"><span class="codeph"> 內部錯誤</span> </td> 
   <td colname="col3"> 這是一個非常罕見的，不該發生的問題。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 62 </td> 
   <td colname="col2"><span class="codeph"> SPS_PPS_FOUND_OUTSIDE_AVCC</span> </td> 
   <td colname="col3"> 流不遵循始終將H264 SPS/PPS放入AVCC的打包建議。 可能發現查找/播放問題。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 63 </td> 
   <td colname="col2"><span class="codeph"> 部分替換</span> </td> 
   <td colname="col3"> 在插入API中指定的替換操作僅部分完成。 當replaceDuration跨越時間軸持續時間時會發生這種情況。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 64 </td> 
   <td colname="col2"><span class="codeph"> RENDITION_M3U8_ERROR</span> </td> 
   <td colname="col3"> 載入格式副本播放清單時出錯。 這隻適用於AVE，而不適用於FlashPlayer。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 65 </td> 
   <td colname="col2"><span class="codeph"> NULL_OPERATION</span> </td> 
   <td colname="col3"> 操作不執行任何操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 66 </td> 
   <td colname="col2"><span class="codeph"> SEGMENT_SKPIPED_ON_FAILURE</span> </td> 
   <td colname="col3"> 無法播放段，失敗時會跳過段。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 67 </td> 
   <td colname="col2"><span class="codeph"> 不相容的RENDER_MODE</span> </td> 
   <td colname="col3"> 不相容的呈現模式。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 68 </td> 
   <td colname="col2"><span class="codeph"> PROTOCOL_NOT_SUPPORTED </span> </td> 
   <td colname="col3"> 不支援URL中使用的Web協定。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 69 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR_INCOMPLATIVE_VERSION</span> </td> 
   <td colname="col3"> 分析媒體檔案時出錯。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 70 </td> 
   <td colname="col2"><span class="codeph"> 清單_檔案_意外_更改</span> </td> 
   <td colname="col3"> 清單檔案以意外方式更改。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 71 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_SPLIT_TIMELINE</span> </td> 
   <td colname="col3"> 無法對時間線執行拆分操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 72 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_ERASE_TIMELINE</span> </td> 
   <td colname="col3"> 無法對時間線執行擦除操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 73 </td> 
   <td colname="col2"><span class="codeph"> DID_NOT_NEXT_FRAGMENTGET</span> </td> 
   <td colname="col3"> 沒有找到下一個碎片。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 74 </td> 
   <td colname="col2"><span class="codeph"> 無時間軸</span> </td> 
   <td colname="col3"> 內部資料結構中不存在時間線。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 75 </td> 
   <td colname="col2"><span class="codeph"> 未找到監聽器</span> </td> 
   <td colname="col3"> 在內部資料結構中找不到偵聽器。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 76 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_START_ERROR</span> </td> 
   <td colname="col3"> 無法啟動音頻。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 77 </td> 
   <td colname="col2"><span class="codeph"> 無音頻接收器</span> </td> 
   <td colname="col3"> 內部資料結構中不存在音頻接收器。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 78 </td> 
   <td colname="col2"><span class="codeph"> 檔案_開啟_錯誤</span> </td> 
   <td colname="col3"> 無法開啟檔案。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 79 </td> 
   <td colname="col2"><span class="codeph"> 檔案寫入錯誤</span> </td> 
   <td colname="col3"> 無法寫入檔案。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 80 </td> 
   <td colname="col2"><span class="codeph"> 檔案讀取錯誤</span> </td> 
   <td colname="col3"> 無法從檔案讀取。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 81 </td> 
   <td colname="col2"><span class="codeph"> ID3PARSE_ERROR</span> </td> 
   <td colname="col3"> 分析ID3資料時出錯。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 82 </td> 
   <td colname="col2"><span class="codeph"> 安全性_錯誤 </span> </td> 
   <td colname="col3"> 由於安全限制，載入內容失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 83 </td> 
   <td colname="col2"><span class="codeph"> 時間軸太短</span> </td> 
   <td colname="col3"> 時間線持續時間太短。 如果這是即時流，則可能會發生頻繁的緩衝。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 84 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_START</span> </td> 
   <td colname="col3"> 該流已切換為僅音頻流。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 85 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_END</span> </td> 
   <td colname="col3"> 該流已從僅音頻切換到帶視頻的流。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 87 </td> 
   <td colname="col2"><span class="codeph"> 未找到鍵 </span> </td> 
   <td colname="col3"> 找不到密鑰。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 88 </td> 
   <td colname="col2"><span class="codeph"> 無效鍵</span> </td> 
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
   <td colname="col3"> 無法處理主清單更新。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 91 </td> 
   <td colname="col2"> <span class="codeph"> URCERTED_TIME_DISCUNTIATION_FOUND</span> </td> 
   <td colname="col3"> 發現未報告的時間中斷。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 92 </td> 
   <td colname="col2"> <span class="codeph"> 不匹配的AV_不連續性_找到</span> </td> 
   <td colname="col3"> 發現音頻和視頻不連續。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 93 </td> 
   <td colname="col2"><span class="codeph"> TRICKPLAY_ENDED_DUE_TO_ERROR</span> </td> 
   <td colname="col3">在中播放媒體時出錯 <i>戲法</i> 的子菜單。 特技播放模式已結束，流已暫停。 呼叫 <span class="codeph"> 播放()</span> 以正常模式播放媒體。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 95 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_AEW</span> </td> 
   <td colname="col3"> 玩家不在直播窗口，必須前進才能趕上。 </td> 
  </tr> 
 </tbody> 
</table>

## 本機錯誤(_E):加密值 {#section_39365E545CAC49B9A4D4678657BB2155}

Adobe視頻引擎的加密模組在 `NATIVE_ERROR` 元資料對象。

| **NATIVE_ERROR_CODE元資料鍵的值** | **NATIVE_ERROR_NAME元資料鍵的值** | **意義** |
|---|---|---|
| 300 | `CRYPTO_ALGORITHM_NOT_SUPPORTED` | 不支援使用的算法。 |
| 301 | `CRYPTO_ERROR_CORRUPTED_DATA` | 資料已損壞。 |
| 302 | `CRYPTO_ERROR_BUFFER_TOO_SMALL` | 緩衝區太小。 |
| 303 | `CRYPTO_ERROR_BAD_CERTIFICATE` | 證書錯誤。 |
| 304 | `CRYPTO_ERROR_DIGEST_UPDATE` | 摘要更新。 |
| 305 | `CRYPTO_ERROR_DIGEST_FINISH` | 摘要完成。 |
| 306 | `CRYPTO_ERROR_BAD_PARAMETER` | 參數錯誤。 |
