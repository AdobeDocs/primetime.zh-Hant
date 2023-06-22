---
title: iOS/tvOS API參考
description: iOS/tvOS API參考
exl-id: 017a55a8-0855-4c52-aad0-d3d597996fcb
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '7000'
ht-degree: 0%

---

# iOS/tvOS SDK API參考 {#iostvos-sdk-api-reference}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 簡介 {#intro}

本頁說明適用於Adobe Primetime驗證的iOS/tvOS原生使用者端所公開的方法和回呼函式。 此處說明的方法和回呼函式定義於 `AccessEnabler.h` 和 `EntitlementDelegate.h` 標題檔案；您可以在iOS AccessEnabler SDK的以下位置找到它們： `[SDK directory]/AccessEnabler/headers/api/`


相關檔案：

* 如需基本Primetime驗證許可權流程的說明，請參閱 [權益流程](/help/authentication/entitlement-flow.md).
* 如需如何使用此API實施Primetime驗證許可權流程的逐步解說，請參閱 [iOS整合逐步指南](/help/authentication/iostvos-sdk-cookbook.md).
* 如需最新的iOS AccessEnabler SDK，請參閱 [iOS Native Access Enabler程式庫](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library).

>[!NOTE]
>
>Adobe鼓勵您只使用Primetime驗證 *公共* API：
>
>* 公開API可供使用，並在所有支援的使用者端型別上經過充分測試。 對於任何公用功能，我們確定每個使用者端型別都有相關方法的對應版本。
>* 公開API必須儘可能穩定，以支援回溯相容性，並確保合作夥伴整合不會中斷。 但是，對於非公開API，我們保留在未來任何時候變更其簽名的權利。 如果您遇到無法透過目前公用Primetime驗證API呼叫的組合支援的特定流程，最好的方法就是讓我們知道。 根據您的需求，我們可以修改公用API，並提供未來穩定的解決方案。


</br>

## API參考 {#apis}

* [init](#initWithSoftwareStatement)：softwareStatement — 例項化AccessEnabler物件。

* **[已棄用]** [init](#init)  — 例項化AccessEnabler物件。

* [setOptions:options:](#setOptions)  — 設定全域SDK選項，例如設定檔或訪客ID。

* [setRequest：](#setReqV3)[請求者ID](#setReqV3)，[setRequestor:requestorID:服務提供者：](#setReqV3)  — 建立程式設計師的身分。

* **[已棄用]** [setRequestor:signedRequestorId:](#setReq)，[setRequestor:signedRequestorId:服務提供者：](#setReq)  — 建立程式設計師的身分。

* **[已棄用]** [setRequestor:signedRequestorId:secret：publicKey](#setReq_tvos)， [setRequestor:signedRequestorId:serviceProviders:secret:publicKey](#setReq_tvos) — 建立程式設計師的身分。

* [setRequestorComplete：](#setReqComplete)  — 通知您的應用程式設定階段已完成。

* [checkAuthentication](#checkAuthN)  — 檢查目前使用者的驗證狀態。

* [getAuthentication](#getAuthN)， [getAuthentication:withData:](#getAuthN)  — 啟動完整驗證工作流程。

* [getAuthentication：filter](#getAuthN_filter)，[getAuthentication:withData:](#getAuthN)[andFilter](#getAuthN_filter)  — 啟動完整驗證工作流程。

* [displayProviderDialog：](#dispProvDialog)  — 通知您的應用程式例項化適當的UI元素，以便使用者選取MVPD。

* [setSelectedProvider：](#setSelProv)  — 通知AccessEnabler使用者的MVPD選擇。

* [navigateToUrl：](#nav2url)  — 通知您的應用程式，使用者需要顯示MVPD登入頁面。

* [navigateToUrl:useSVC:](#nav2urlSVC)  — 使用SFSafariViewController通知您的應用程式使用者需要顯示MVPD登入頁面

* [handleExternalURL：url](#handleExternalURL)  — 完成驗證/登出流程。

* **[已棄用]** [getAuthenticationToken](#getAuthNToken)  — 向後端伺服器要求驗證Token。

* [setAuthenticationStatus:errorCode:](#setAuthNStatus)  — 通知您的應用程式驗證流程的狀態。

* [checkPreauthorizedResources：](#checkPreauth)  — 判斷使用者是否已獲授權檢視特定的受保護資源。

* [checkPreauthorizedResources:cache:](#checkPreauthCache)  — 判斷使用者是否已獲授權檢視特定的受保護資源。

* [preauthorizedResources：](#preauthResources)  — 提供使用者已獲授權檢視的資源清單。

* [checkAuthorization：](#checkAuthZ)， [checkAuthorization:withData:](#checkAuthZ)  — 檢查目前使用者的授權狀態。

* [getAuthorization：](#getAuthZ)， [getAuthorization:withData:](#getAuthZ)  — 起始授權流程。

* [setToken:forResource:](#setToken)  — 通知您的應用程式授權流程已成功完成。

* [tokenRequestFailed:errorCode:errorDescription：](#tokenReqFailed)  — 通知您的應用程式授權流程失敗。

* [登出](#logout)  — 起始登出流程。

* [getselectedprovider](#getSelProv)  — 決定目前選取的提供者。

* [selectedProvider：](#selProv)  — 將目前所選MVPD的相關資訊傳送至您的應用程式。

* [getMetadata：](#getMeta)  — 擷取AccessEnabler程式庫公開為中繼資料的資訊。

* [presentTvProviderDialog：](#presentTvDialog)  — 通知您的應用程式顯示Apple SSO對話方塊。

* [dissisTvProviderDialog：](#dismissTvDialog)  — 通知您的應用程式隱藏Apple SSO對話方塊。

* [setmetadataStatus:encrypted:forKey:andArguments:](#setMetaStatus)  — 傳遞要求的中繼資料 [getMetadata：](#getMeta) 呼叫。

* [sendTrackingData:forEventType:](#sendTracking)  — 傳遞追蹤資料資訊。

* [MVPD](#mvpd) - MVPD類別。 [包含有關MVPD的資訊]

### init：softwareStatement {#initWithSoftwareStatement}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 具現化AccessEnabler物件。 每個應用程式執行個體應該有一個AccessEnabler執行個體。

| **API呼叫： iOS AccessEnabler建構函式** |
| --- |
| `- (id) init:` <br> |
| `(NSString *)softwareStatement;` |


**可用性：** v3.0+

**引數：**

* **softwareStatement：** 識別Adobe系統中應用程式的字串。 瞭解如何取得軟體宣告。

[返回頁首……](#apis)



### 初始 —  [已棄用]{#init}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 具現化AccessEnabler物件。 每個應用程式執行個體應該有一個AccessEnabler執行個體。

| API呼叫： iOS AccessEnabler建構函式 |
| --- |
| ```- (id) init;``` |

**可用性：** v1.0+ **直到：** v3.0

**引數：** 無

[返回頁首……](#apis)

</br>

### setoptions：options {#setOptions}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 設定全域SDK選項。 它接受NSDictionary作為引數。 字典中的值會連同SDK發出的每個網路呼叫一起傳遞至伺服器。

**注意：** 這些值將會傳遞至伺服器，不受目前流量（驗證/授權）影響。 如果您想要變更值，可以隨時呼叫此方法。

| API呼叫： setOptions |
| --- |
| ```- (void) setOptions:(NSDictionary *)options;``` |

**可用性：** v2.3.0+

**引數：**

* *選項*：包含全域SDK選項的NSDictionary。 目前提供下列選項：
   * **applicationProfile**  — 可用於根據此值進行伺服器設定。
   * **visitorID** - visitorIDMarketing Cloud。 此值稍後可用於進階分析報表。
   * **handleSVC**  — 表示程式設計師是否會處理SFSafariViewControllers的布林值。 請參閱 [iOS SDK 3.2+上的SFSafariViewController支援](/help/authentication/sfsafariviewcontroller-support-on-ios-sdk-32.md) 以取得更多詳細資料。
      * 若設為 **false，** SDK會自動向一般使用者呈現SFSafariViewController。 SDK會進一步導覽至MVPD登入頁面URL。
      * 若設為 **true，** SDK會 **NOT** 自動向一般使用者呈現SFSafariViewController。 SDK會進一步觸發 **navigate(toUrl：{url}， useSVC：YES)**.
* **device\_info**  — 使用者端資訊，如所述 [傳遞使用者端資訊](/help/authentication/passing-client-information-device-connection-and-application.md).

[返回頁首……](#apis)


### setRequestor：requestorID， setRequestor:requestorID:服務提供者： {#setReqV3}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 建立程式設計師的身分。 每個程式設計師在為Primetime驗證系統註冊Adobe時，都會獲得一個唯一的ID。 處理SSO和遠端Token時，驗證狀態會在應用程式於背景時變更，當應用程式進入前景時可再次呼叫setRequestor，以便與系統狀態同步（如果SSO已啟用，請擷取遠端Token，如果同時發生登出，請刪除本機Token）。

伺服器回應包含MVPD清單，以及附加至程式設計師身分的某些設定資訊。 伺服器回應由AccessEnabler程式碼在內部使用。 只有操作的狀態（即SUCCESS/FAIL）會透過向您的應用程式顯示 `setRequestorComplete:` callback。

如果 `urls` 不會使用引數，因此產生的網路呼叫會鎖定預設服務提供者URL：Adobe發行/生產環境。


如果提供的值用於 `urls` 引數，產生的網路呼叫會鎖定中提供的所有URL `urls` 引數。 所有設定請求都在不同的執行緒中同時觸發。 第一個回應者在編譯MVPD清單時優先。 對於清單中的每個MVPD，AccessEnabler會記住相關服務提供者的URL。 所有後續的軟體權利檔案要求都會導向至與設定階段期間與目標MVPD配對的服務提供者相關聯的URL。

| API呼叫：要求者設定 |
| --- |
| ```- (void) setRequestor:(NSString *)requestorID``` |


**可用性：** v3.0+

| API呼叫：要求者設定 |
| --- |
| `- (void) setRequestor:(NSString *)requestorID serviceProviders:(NSArray *)urls;` |


**可用性：** v3.0+

**引數：**

* *請求者ID*：與程式設計師相關聯的唯一ID。 當您首次向Primetime驗證服務註冊時，請將Adobe指派的唯一ID傳遞至您的網站。
* *url*：選用引數；預設會使用Adobe服務提供者(http://sp.auth.adobe.com/)。 此陣列可讓您為Adobe提供的驗證和授權服務指定端點（不同的執行個體可用於偵錯）。 您可以使用此選項來指定多個Primetime驗證服務提供者執行個體。 如此一來，MVPD清單就會由所有服務提供者的端點組成。 每個MVPD都與最快的服務提供者相關聯，也就是首先回應並支援該MVPD的提供者。

>[!NOTE]
>
>如果呼叫時未使用 `serviceProviders` 引數，程式庫會從預設服務提供者(亦即 `https://sp.auth.adobe.com` 用於生產設定檔或 `https://sp.auth-staging.adobe.com` （適用於中繼設定檔）。 如果 `serviceProviders` 引數已提供，必須是URL的陣列。組態資訊會從所有指定的端點擷取並合併。 如果不同的服務提供者回應中存在重複的資訊，則衝突會以回應速度最快的伺服器來解決（亦即，以回應時間最短的伺服器優先）。

**觸發的回呼：** [`setRequestorComplete:`](#setReqComplete)

[返回頁首……](#apis)

</br>

### setRequestor:setSignedRequestorId:， setRequestor:setSignedRequestorId:服務提供者： - [已棄用] {#setReq}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 建立程式設計師的身分。 每個程式設計師在為Primetime驗證系統註冊Adobe時，都會獲得一個唯一的ID。 處理SSO和遠端Token時，驗證狀態會在應用程式於背景時變更，當應用程式進入前景時可再次呼叫setRequestor，以便與系統狀態同步（如果SSO已啟用，請擷取遠端Token，如果同時發生登出，請刪除本機Token）。

伺服器回應包含MVPD清單，以及附加至程式設計師身分的某些設定資訊。 伺服器回應由AccessEnabler程式碼在內部使用。 只有操作的狀態（即SUCCESS/FAIL）會透過向您的應用程式顯示 `setRequestorComplete:` callback。

如果 `urls` 不會使用引數，因此產生的網路呼叫會鎖定預設服務提供者URL：Adobe發行/生產環境。

如果提供的值用於 `urls` 引數，產生的網路呼叫會鎖定中提供的所有URL `urls` 引數。 所有設定請求都在不同的執行緒中同時觸發。 第一個回應者在編譯MVPD清單時優先。 對於清單中的每個MVPD，AccessEnabler會記住相關服務提供者的URL。 所有後續的軟體權利檔案要求都會導向至與設定階段期間與目標MVPD配對的服務提供者相關聯的URL。

| API呼叫：要求者設定 |
| --- |
| </br>`- (void) setRequestor:(NSString *)requestorID`</br>`signedRequestorID:(NSString *)signedRequestorID;` </br></br> |

**可用性：** v1.0+ **直到：** v3.0

| API呼叫：要求者設定 |
| --- |
| `- (void) setRequestor:(NSString *)requestorID ` <br> `       signedRequestorID:(NSString *)signedRequestorID` <br> `         serviceProviders:(NSArray *)urls;` |

**可用性：** v1.0+ **直到：** v3.0

**引數：**

* *請求者ID*：與程式設計師相關聯的唯一ID。 當您首次向Primetime驗證服務註冊時，請將Adobe指派的唯一ID傳遞至您的網站。
* *signedRequestorID*： **此引數存在於iOS AccessEnabler 1.2版和更新版本中。** 以私密金鑰進行數位簽章的請求者ID復本。 <!--For more details, see [Registering Native Clients](https://tve.helpdocsonline.com/registering-native-clients)-->.
* *url*：選用引數；預設會使用Adobe服務提供者(http://sp.auth.adobe.com/)。 此陣列可讓您為Adobe提供的驗證和授權服務指定端點（不同的執行個體可用於偵錯）。 您可以使用此選項來指定多個Primetime驗證服務提供者執行個體。 如此一來，MVPD清單就會由所有服務提供者的端點組成。 每個MVPD都與最快的服務提供者相關聯，也就是首先回應並支援該MVPD的提供者。

**附註：** 如果呼叫時未使用 `serviceProviders` 引數，程式庫會從預設服務提供者(亦即`https://sp.auth.adobe.com` 用於生產設定檔或 `https://sp.auth-staging.adobe.com` （適用於中繼設定檔）。 如果 `serviceProviders` 引數已提供，必須是URL的陣列。組態資訊會從所有指定的端點擷取並合併。 如果不同的服務提供者回應中存在重複的資訊，則衝突會以回應速度最快的伺服器來解決（亦即，以回應時間最短的伺服器優先）。

**觸發的回呼：** [`setRequestorComplete:`](#setReqComplete)


[返回頁首……](#apis)

### setRequestor:setSignedRequestorId:secret：publicKey， setRequestor:setSignedRequestorId:serviceProviders:secret:公開金鑰 —  [已棄用] {#setReq_tvos}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 建立程式設計師的身分。 每個程式設計師在為Primetime驗證系統註冊Adobe時，都會獲得一個唯一的ID。 此設定只應在應用程式的生命週期中執行一次。

伺服器回應包含MVPD清單，以及附加至程式設計師身分的某些設定資訊。 伺服器回應由AccessEnabler程式碼在內部使用。 只有操作的狀態（即SUCCESS/FAIL）會透過向您的應用程式顯示 `setRequestorComplete:` callback。

如果 `urls` 不會使用引數，因此產生的網路呼叫會鎖定預設服務提供者URL：Adobe發行/生產環境。

如果提供的值用於 `urls` 引數，產生的網路呼叫會鎖定中提供的所有URL `urls` 引數。 所有設定請求都在不同的執行緒中同時觸發。 第一個回應者在編譯MVPD清單時優先。 對於清單中的每個MVPD，AccessEnabler會記住相關服務提供者的URL。 所有後續的軟體權利檔案要求都會導向至與設定階段期間與目標MVPD配對的服務提供者相關聯的URL。



<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：要求者設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestor:(NSString *)requestorID 
    signedRequestorID:(NSString *)signedRequestorID
               secret:(NSString *)secret
            publicKey:(NSString *)publicKey;</code></pre></td>
</tr>
</tbody>
</table>


**可用性：** v2.0+ **直到：** v3.0

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：要求者設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestor:(NSString *)requestorID 
    signedRequestorID:(NSString *)signedRequestorID 
     serviceProviders:(NSArray *)urls</code></pre>
<p><code class="sourceCode objectivec">               secret:(NSString *)secret</code></p>
<p><code class="sourceCode objectivec">            publicKey:(NSString *)publicKey;</code></p></td>
</tr>
</tbody>
</table>

**可用性：** v2.0+ **直到：** v3.0

**引數：**

* *請求者ID*：與程式設計師相關聯的唯一ID。 當您首次向Primetime驗證服務註冊時，請將Adobe指派的唯一ID傳遞至您的網站。
* *signedRequestorID*： **此引數存在於iOS AccessEnabler 1.2版和更新版本中。** 以私密金鑰進行數位簽章的請求者ID復本。 <!--For more details, see [Registering Native Clients](https://tve.helpdocsonline.com/registering-native-clients)-->.
* *url*：選用引數；預設會使用Adobe服務提供者(http://sp.auth.adobe.com/)。 此陣列可讓您為Adobe提供的驗證和授權服務指定端點（不同的執行個體可用於偵錯）。 您可以使用此選項來指定多個Primetime驗證服務提供者執行個體。 如此一來，MVPD清單就會由所有服務提供者的端點組成。 每個MVPD都與最快的服務提供者相關聯，也就是首先回應並支援該MVPD的提供者。
* secret和publicKey：用來簽署第二個熒幕呼叫的秘密和公開金鑰。 如需詳細資訊，請參閱 [無使用者端檔案](#create_dev).

如果呼叫時未使用 `serviceProviders` 引數，程式庫會從預設服務提供者擷取設定(即 `https://sp.auth.adobe.com` (適用於生產設定檔，或https://sp.auth-staging.adobe.com （適用於中繼設定檔）。 如果 `serviceProviders` 引數已提供，必須是URL的陣列。組態資訊會從所有指定的端點擷取並合併。 如果不同的服務提供者回應中存在重複的資訊，則衝突會以回應速度最快的伺服器來解決（亦即，以回應時間最短的伺服器優先）。

**觸發的回呼：** [`setRequestorComplete:`](#setReqComplete)

[返回頁首……](#apis)

</br>

### setRequestorComplete： {#setReqComplete}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回呼，通知您的應用程式設定階段已完成。 這是應用程式可以開始發出權益要求的訊號。 在設定階段完成之前，應用程式無法發出任何權益請求。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回呼：要求者設定完成</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestorComplete:(int)status;</code></pre></td>
</tr>
</tbody>
</table>


**可用性：** v1.0+

**引數**：

* *狀態*：可以取下列其中一個值：
   * `ACCESS_ENABLER_STATUS_SUCCESS`  — 設定階段已成功完成
   * `ACCESS_ENABLER_STATUS_ERROR`  — 設定階段失敗

**觸發者：**
`setRequestor:setSignedRequestorId:, `[`setRequestor:setSignedRequestorId:serviceProviders:`](#setReq)

[返回頁首……](#apis)

</br>

### checkAuthentication {#checkAuthN}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 檢查目前使用者的驗證狀態。
其做法是在本機權杖儲存空間中搜尋有效的驗證權杖。 呼叫此方法不會執行任何網路呼叫。 應用程式會使用它來查詢使用者的驗證狀態並相應地更新UI （即更新登入/登出UI）。 驗證狀態會透過 [`setAuthenticationStatus:errorCode:`](#setAuthNStatus) callback。\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：檢查驗證狀態</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthentication;</code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**引數：** 無

**觸發的回呼：**
[`setAuthenticationStatus:errorCode:`](#setAuthNStatus)

[返回頁首……](#apis)

</br>

### getAuthentication， getAuthentication:withData: {#getAuthN}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 啟動完整驗證工作流程。 首先檢查驗證狀態。 如果尚未驗證，則會啟動驗證流程狀態機器：

* 如果上次驗證嘗試成功，則會略過MVPD選取階段，而且 [`navigateToUrl:`](#nav2url) 已觸發回呼。 應用程式會使用此回呼來例項化WebView控制項，該控制項會向使用者顯示MVPD的登入頁面。 **[注意：截至Access Enabler 1.5，由於SDK的限制，此功能無法使用].**
* 如果上次驗證嘗試不成功，或使用者明確登出，則 [`displayProviderDialog:`](#dispProvDialog) 已觸發回呼。 您的應用程式使用此回呼來顯示MVPD選擇UI。 此外，您的應用程式需要透過以下方式通知AccessEnabler程式庫，以繼續驗證流程： [`setSelectedProvider:`](#setSelProv) 方法。

在MVPD登入頁面上驗證使用者的認證時，您的應用程式必須監督使用者在MVPD登入頁面上驗證時發生的多個重新導向操作。 輸入正確的認證時，WebView控制項會重新導向至由定義的自訂URL。 `ADOBEPASS_REDIRECT_URL` 常數。 此URL不打算由WebView載入。 應用程式必須攔截此URL，並將此事件解譯為登入階段完成的訊號。 然後，它應該將控制權移交給AccessEnabler，以完成驗證流程(透過呼叫 [handleExternalURL](#handleExternalURL) 方法)。

最後，驗證狀態會透過 [setAuthenticationStatus:errorCode:](#setAuthNStatus) callback。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：起始驗證流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication;</code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：起始驗證流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**可用性：** v1.9+

**引數：**

* *forceAuthn*：指定是否應啟動驗證流程的旗標，無論使用者是否已驗證。
* *資料*：由要傳送至Pay-TV Pass服務的索引鍵值配對組成的字典。 Adobe可使用此資料來啟用未來的功能，而不需變更SDK。

**觸發的回呼：** ` setAuthenticationStatus:errorCode:, `[`displayProviderDialog:`](#dispProvDialog)`,`` sendTrackingData:forEventType:`


[返回頁首……](#apis)

</br>

### getAuthentication：filter， getAuthentication:withData:andFilter {#getAuthN_filter}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 啟動完整驗證工作流程。 首先檢查驗證狀態。 如果尚未驗證，則會啟動驗證流程狀態機器：

* [presentTvProviderDialog()](#presentTvDialog) 如果目前的要求者至少有一個支援SSO的MVPD，則會呼叫。 如果任何MVPD都不支援SSO，傳統驗證流程就會開始，而篩選引數會被忽略。
* 使用者完成Apple SSO流程後 [dissisTvProviderDialog()](#dismissTvDialog) 將會觸發，且驗證程式將會完成。

最後，驗證狀態會透過 [setAuthenticationStatus:errorCode:](#setAuthNStatus) callback。

**可用性：** v2.4+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：起始驗證流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(NSDictionary *)filter;</code></pre></td>
</tr>
</tbody>
</table>

 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：起始驗證流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data
                 andFilter:(NSDictionary *)filter;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**引數：**

* *forceAuthn*：指定是否應啟動驗證流程的旗標，無論使用者是否已驗證。
* *資料*：由要傳送至Pay-TV Pass服務的索引鍵值配對組成的字典。 Adobe可使用此資料來啟用未來的功能，而不需變更SDK。 
* 篩選：包含兩個MVPD ID清單的字典，應該會出現在Apple SSO對話方塊中。 任何不支援SSO的MVPD都將被忽略，但順序將被遵守。 字典必須有兩個索引鍵：
   * TV\_PROVIDERS：包含所有應該出現在選擇器中的MVPD的清單
   * FEATURED\_TV\_PROVIDERS：包含所有MVPD的清單，應該標示為選取器中的精選。 此清單中的MVPD也必須在TV\_PROVIDERS清單中指定。

**可用性：** v2.0 - v2.3.1


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：起始驗證流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(NSArray *)filter;</code></pre></td>
</tr>
</tbody>
</table>

 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：起始驗證流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data
                 andFilter:(NSArray *)filter;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**引數：**

* *forceAuthn*：指定是否應啟動驗證流程的旗標，無論使用者是否已驗證。
* *資料*：由要傳送至Pay-TV Pass服務的索引鍵值配對組成的字典。 Adobe可使用此資料來啟用未來的功能，而不需變更SDK。 
* filter：應顯示在Apple SSO對話方塊中的MVPD id清單。 任何不支援SSO的MVPD都將被忽略，但順序將被遵守。

**觸發的回呼：** `setAuthenticationStatus:errorCode:, presentTvProviderDialog, dismissTvProviderDialog`


[返回頁首……](#apis)

</br>

#### displayProviderDialog： {#dispProvDialog}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回呼，通知應用程式需要具現化適當的UI元素，以允許使用者選取所需的MVPD。 回呼會提供MVPD物件清單，內含其他資訊，可協助您正確建立選取專案UI面板（例如指向MVPD標誌的URL、好記的顯示名稱等）

一旦使用者選取了所需的MVPD，上層應用程式就需呼叫，以恢複驗證流程 `setSelectedProvider:` ，並向其傳遞與使用者選取專案相對應的MVPD ID。

**中止驗證流程**  — 使用者能夠按下「上一步」按鈕，這相當於中止驗證流程。 在該案例中，您的應用程式必須呼叫 [setSelectedProvider：](#setSelProv) 方法，傳遞null作為引數，讓AccessEnabler有機會重設其驗證狀態機器。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回呼：顯示MVPD選擇UI</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) displayProviderDialog:(NSArray *)mvpds;</code></pre></td>
</tr>
</tbody>
</table>


**可用性：** v1.0+

**引數**：

* *mvpds*：MVPD物件清單，內含MVPD相關資訊，應用程式可用來建置MVPD選取UI元素。

**觸發者：** ` getAuthentication, `[getAuthentication:withData:](#getAuthN)，` getAuthorization:, `[getAuthorization:withData:](#getAuthZ)


[返回頁首……](#apis)

</br>

#### setSelectedProvider： {#setSelProv}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 您的應用程式會呼叫此方法，通知Access Enabler使用者的MVPD選擇。 應用程式可以使用此方法來選取或變更用於驗證的服務提供者。

如果選取的MVPD是TempPass MVPD，它會自動透過該MVPD進行驗證，之後不需要呼叫getAuthentication()。

請注意，這不適用於促銷臨時傳遞，因為getAuthentication()方法會提供額外的引數。

傳遞時 *null* 作為引數， Access Enabler假設使用者已取消驗證流程（即按下「上一步」按鈕），並透過重設驗證狀態機器和呼叫 [setAuthenticationStatus:errorCode:](#setAuthNStatus) 回撥使用 `AccessEnabler.PROVIDER_NOT_SELECTED_ERROR` 錯誤代碼。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：設定目前選取的提供者</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setSelectedProvider:(NSString *)mvpdId;</code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**引數：** 無

**觸發的回呼：** ` setAuthenticationStatus:errorCode:,sendTrackingData:forEventType:,  `[`navigateToUrl:`](#nav2url)

[返回頁首……](#apis)

</br>

#### navigateToUrl： {#nav2url}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明：** 由AccessEnabler觸發的回呼，要求您的應用程式將UIWebView/WKWebView控制器具現化，並載入回呼中提供的URL **`url`** 引數。 回呼會傳遞 **`url`** 代表驗證端點的URL或登出端點的URL的引數。

作為UIWebView/WKWebView` `控制器經過數個重新導向，您的應用程式必須監控控制器的活動，並偵測載入由定義的特定自訂URL的時刻。 `ADOBEPASS_REDIRECT_URL `常數(即 `adobepass://ios.app`)。 請注意，這個特定自訂URL實際上無效，控制器並非打算實際載入此URL。 應用程式必須將其解譯為驗證或登出流程已完成，且關閉控制器是安全的訊號。 當控制器載入這個特定的自訂URL時，您的應用程式必須關閉UIWebView/WKWebView並呼叫AccessEnabler的 `handleExternalURL:url `api方法。

**注意：** 請注意，若是驗證流程，此時使用者可以按下「上一步」按鈕，這相當於驗證流程中止。 在這種情況下，您的應用程式必須呼叫 [setSelectedProvider：](#setSelProv) 方法傳遞 **`nil`** 做為引數，並授予AccessEnabler重設其驗證狀態機器的機會。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回呼：顯示MVPD登入頁面</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) navigateToUrl:(NSString *)url; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**引數**：

* *url*：指向MVPD登入頁面的URL

**觸發者：** [setSelectedProvider：](#setSelProv)

 

[返回頁首……](#apis)

</br>

#### navigateToUrl:useSVC: {#nav2urlSVC}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明：** AccessEnabler觸發的回呼，而非 `navigateToUrl:` 如果您的應用程式先前曾透過啟用手動Safari檢視控制器(SVC)處理， [setoptions(\[&quot;handleSVC&quot;：true&quot;\])](#setOptions) 呼叫，且僅適用於MVPD需要Safari檢視控制器(SVC)的情況。 對於所有其他MVPD， `navigateToUrl:` 將會呼叫callback。 請參閱[iOS SDK 3.2+上的SFSafariViewController支援](/help/authentication/sfsafariviewcontroller-support-on-ios-sdk-32.md) 以取得有關如何管理Safari檢視控制器(SVC)的詳細資訊。

類似於 `navigateToUrl:` 回撥 `navigateToUrl:useSVC:` 由AccessEnabler觸發，要求您的應用程式將 `SFSafariViewController` 和來載入回呼中提供的URL **`url`** 引數。 回呼會傳遞 **`url`** 代表驗證端點URL或登出端點URL的引數，以及 **`useSVC`** 指定應用程式必須使用的引數 `SFSafariViewController`.

作為 `SFSafariViewController` 控制器經過數個重新導向，您的應用程式必須監控控制器的活動，並偵測載入由您定義的特定自訂URL的瞬間 `application's custom scheme` (例如** **`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)。 請注意，這個特定自訂URL實際上無效，控制器並非打算實際載入此URL。 應用程式必須將其解譯為驗證或登出流程已完成，且關閉控制器是安全的訊號。 當控制器載入這個特定的自訂URL時，您的應用程式必須關閉 `SFSafariViewController` 並呼叫AccessEnabler的 `handleExternalURL:url `api方法。

**注意：** 請注意，若是驗證流程，此時使用者可以按下「上一步」按鈕，這相當於驗證流程中止。 在這種情況下，您的應用程式必須呼叫 [setSelectedProvider：](#setSelProv) 方法傳遞 **`nil`** 做為引數，並授予AccessEnabler重設其驗證狀態機器的機會。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回呼：在SFSafariViewController中顯示MVPD登入頁面</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>@optional
- (void) navigateToUrl:(NSString *)url useSVC:(BOOL)useSVC; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：**v 3.2+

**引數**：

* *url：* 指向MVPD登入頁面的URL
* *useSVC：* url是否應載入SFSafariViewController。

**觸發者：**[ setOptions：](#setOptions) 早於 [setSelectedProvider：](#setSelProv) 

[返回頁首……](#apis)

</br>

#### handleExternalURL：url {#handleExternalURL}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 您的應用程式會呼叫此方法，以完成驗證或登出流程。 當您的應用程式偵測到以下情況時，應立即呼叫此方法： `UIWebView/WKWebView or SFSafariViewController` 控制器會重新導向至特定的自訂URL。 如果您的應用程式需要使用 `SFSafariViewController `控制器特定的自訂URL由您設定的 `application's custom scheme` (例如：`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否則此特定自訂URL會由 `ADOBEPASS_REDIRECT_URL `常數(即 `adobepass://ios.app`)。

在驗證流程中，AccessEnabler會從後端伺服器擷取驗證Token，並將其儲存在本機的Token儲存體中，以完成流程。 AccessEnabler會呼叫 `setAuthenticationStatus()`<!--(http://tve.helpdocsonline.com/ios-technical-overview#setAuthNStatus)--> 狀態碼為1的callback，表示成功。 如果在執行這些步驟期間發生錯誤， `setAuthenticationStatus()`<!--(http://tve.helpdocsonline.com/ios-technical-overview#setAuthNStatus)--> 系統會以狀態碼0來觸發回呼，表示驗證失敗，以及對應的錯誤代碼。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：完成驗證或登出流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code> (void) handleExternalURL:(NSString *)url; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v3.0+

**引數：** 

* *url*：從以下網址攔截到的URL： ` UIWebView/WKWebView or SFSafariViewController ` 控制項為字串。


**觸發的回呼：** `setAuthenticationStatus:errorCode, sendTrackingData:forEventType:`

[返回頁首……](#apis)

</br>

#### getAuthenticationToken - [已棄用] {#getAuthNToken}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 從後端伺服器要求驗證Token，以完成驗證流程。 只有當WebView控制項裝載MVPD登入頁面時，將重新導向至自訂URL時，您的應用程式才會呼叫此方法。 `ADOBEPASS_REDIRECT_URL` 常數。\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：擷取驗證Token</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthenticationToken; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+ **直到：** v3.0

**引數：** 無

**觸發的回呼：** `setAuthenticationStatus:errorCode,sendTrackingData:forEventType:`

[返回頁首……](#apis)

&lt;/br

#### setAuthenticationStatus:errorCode: {#setAuthNStatus}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回呼，通知應用程式驗證流程的狀態。 在許多地方，此流程可能會因為使用者的互動或其他未預見的情況（例如網路連線問題等）而失敗。 此回呼會通知應用程式驗證流程的成功/失敗狀態，同時在需要時提供有關失敗原因的其他資訊。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回呼：報告驗證流程的狀態</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setAuthenticationStatus:(int)status 
                       errorCode:(NSString *)code; </code></pre></td>
</tr>
</tbody>
</table>


**可用性：** v1.0+

**引數**：

* *狀態*：可以取下列其中一個值：
   * `ACCESS_ENABLER_STATUS_SUCCESS`  — 驗證流程已成功完成
   * `ACCESS_ENABLER_STATUS_ERROR`  — 驗證流程失敗
* *程式碼*：失敗原因。 若 *狀態* 是 `ACCESS_ENABLER_STATUS_SUCCESS`，則 *程式碼* 為空字串(即由 `USER_AUTHENTICATED` 常數)。 如果失敗，此引數可採用下列其中一個值：
   * `USER_NOT_AUTHENTICATED_ERROR`  — 未驗證使用者。 回應 [checkAuthentication：](#checkAuthN) 當本機權杖快取中沒有有效的驗證權杖時，方法呼叫。
   * `PROVIDER_NOT_SELECTED_ERROR` - AccessEnabler在上層應用程式通過後，已重設驗證狀態機器 *null* 至 [`setSelectedProvider:`](#setSelProv) 以中止驗證流程。  使用者可能已取消驗證流程（即按下「上一步」按鈕）。
   * `GENERIC_AUTHENTICATION_ERROR`  — 驗證流程因網路無法使用或使用者明確取消驗證流程等原因而失敗。

**觸發者：** ` checkAuthentication, getAuthentication, `[getAuthentication:withData:](#getAuthN)，` checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ)

[返回頁首……](#apis)

</br>

### checkPreauthorizedResources： {#checkPreauth}


**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 應用程式會使用此方法來判斷使用者是否已獲授權檢視特定的受保護資源。 此方法的主要用途是擷取用於裝飾UI的資訊 **（例如，使用鎖定和解鎖圖示來指示存取狀態）。**

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：設定目前選取的提供者</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.3+

**引數：**

* *資源：* 應檢查其授權的資源陣列。 清單中的每個元素都應是代表資源ID的字串。 資源ID的限制與呼叫中的資源ID相同，也就是說，它應該是程式設計師與MVPD或媒體RSS片段之間建立的議定值。

**已觸發回呼：** [`preauthorizedResources:`](#preauthResources)

[返回頁首……](#apis)

</br>

### checkPreauthorizedResources:cache: {#checkPreauthCache}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 應用程式會使用此方法來判斷使用者是否已獲授權檢視特定的受保護資源。 此方法的主要用途是擷取資訊以用於裝飾UI （例如，使用鎖定和解鎖圖示來指示存取狀態）。 此 **快取** 引數控制內部快取是否用於解析資源。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：設定目前選取的提供者</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources cache:(BOOL)cache; </code></pre></td>
</tr>
</tbody>
</table>

 

**可用性：** v3.1+

 

**引數：**

* *資源：* 應檢查其授權的資源陣列。 清單中的每個元素都應是代表資源ID的字串。 資源ID的限制與 `getAuthorization:` 呼叫，也就是說，它應該是程式設計師和MVPD或媒體RSS片段之間建立的議定值。
* *快取：* 指定是否使用內部快取來解析資源的布林值。 如果為false，則會略過快取，導致每次呼叫此API時都進行伺服器呼叫。

**已觸發回呼：** [`preauthorizedResources:`](#preauthResources)

[返回頁首……](#apis)

</br>

### preauthorizedResources： {#preauthResources}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明：** 回呼觸發者： `checkPreauthorizedResources:`. 提供使用者已獲授權檢視的資源清單。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：設定目前選取的提供者</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.3+

**引數：**

* `resources`：使用者已獲授權可檢視的資源陣列。

**觸發者：** [`checkPreauthorizedResources:`](#checkPreauth)

 

[返回頁首……](#apis)

</br>

### checkAuthorization：， checkAuthorization:withData: {#checkAuthZ}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 應用程式使用此方法來檢查授權狀態。 首先檢查驗證狀態。 如果未驗證， [tokenRequestFailed:errorCode:errorDescription：](#tokenReqFailed) 會觸發callback，而方法會結束。 如果使用者已通過驗證，它也會觸發授權流程。 欲知詳情，請參閱 [`getAuthorization:`](#getAuthZ) 方法。


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：檢查授權狀態</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthorization:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：檢查授權狀態</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthorization:(NSString *)resource:
                   withData:(NSDictionary *)data; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.9+

**引數：**

* *資源*：使用者要求授權的資源ID。
* *資料*：由要傳送至Pay-TV Pass服務的索引鍵值配對組成的字典。 Adobe可使用此資料來啟用未來的功能，而不需變更SDK。 

**觸發的回呼：**
[tokenRequestFailed:errorCode:errorDescription：](#tokenReqFailed)`,setToken:forResource:, sendTrackingData:forEventType:, setAuthenticationStatus:errorCode:`

[返回頁首……](#apis)

</br>

### getAuthorization：， getAuthorization:withData: {#getAuthZ}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 應用程式會使用此方法來起始授權流程。 如果使用者尚未驗證，它也會啟動驗證流程。 如果使用者通過驗證，AccessEnabler會繼續發出授權權杖（如果本機權杖快取中不存在有效的授權權杖）和短期媒體權杖的請求。 取得短媒體權杖後，授權流程即視為完成。 此 [setToken:forResource:](#setToken) 系統會觸發callback，並將簡短媒體權杖作為引數傳送至應用程式。 如果由於任何原因，授權失敗， [tokenRequestFailed:forEventType:](#tokenReqFailed) 會觸發回呼，並提供錯誤代碼/詳細資訊。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：起始授權流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthorization:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：起始授權流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthorization:(NSString *)resource:
                 withData:(NSDictionary *)data; </code></pre></td>
</tr>
</tbody>
</table>

 

**可用性：** v1.9+

**引數：**

* *資源*：使用者要求授權的資源ID。
* *資料*：由要傳送至Pay-TV Pass服務的索引鍵值配對組成的字典。 Adobe可使用此資料來啟用未來的功能，而不需變更SDK。 

**觸發的回呼：** `tokenRequestFailed:errorCode:errorDescription:, setToken:forResource:,sendTrackingData:forEventType:`

**觸發的其他回呼：**\
此方法也可以觸發下列回呼（如果同時啟動驗證流程）： `setAuthenticationStatus:errorCode:`， `displayProviderDialog:`\
 
**注意：請使用checkAuthorization： / checkAuthorization:withData: 而不是getAuthorization： / getAuthorization:withData: 儘可能使用。 getAuthorization： / getAuthorization:withData: 方法將啟動完整的驗證流程（如果使用者未驗證），這可能會導致程式設計人員方面的複雜實施。**

[返回頁首……](#apis)

</br>

### setToken:forResource: {#setToken}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回呼，通知您的應用程式授權流程已成功完成。 短期媒體代號也會作為引數傳遞。\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回呼：授權流程已成功完成</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setToken:(NSString *)token 
      forResource:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**引數**：

* *token*：短期媒體權杖
* *資源*：取得授權的資源

**觸發者：** [checkAuthorization：](#checkAuthZ)` , `[checkAuthorization:withData:](#checkAuthZ)，` `[getAuthorization：](#getAuthZ)， [getAuthorization:withData:](#getAuthZ)

[返回頁首……](#apis)

</br>

### tokenRequestFailed:errorCode:errorDescription： {#tokenReqFailed}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回呼，通知上層應用程式授權流程失敗。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回呼：授權流程失敗</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) tokenRequestFailed:(NSString *)resource 
                  errorCode:(NSString *)code 
           errorDescription:(NSString *)description; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**引數**：

* *資源*：取得授權的資源。
* *程式碼*：與失敗案例相關聯的錯誤代碼。 可能的值：
   * `USER_NOT_AUTHORIZED_ERROR`  — 使用者無法授權指定的資源
* *說明*：有關失敗情況的其他詳細資訊。 如果此描述性字串因任何原因無法使用，Primetime驗證會傳送空字串 **(「」)**. \
   MVPD可使用此字串來傳遞自訂錯誤訊息或銷售相關訊息。 例如，如果拒絕訂閱者對資源的授權，MVPD會傳送訊息，例如：「您目前無法在封裝中存取此通道。 若要升級您的套件，請按一下 **此處**.」 Primetime驗證會透過此回呼將訊息傳遞給程式設計師，程式設計師可以選擇顯示或忽略訊息。 Primetime驗證也可以使用此引數來提供可能導致錯誤的狀況通知。 例如，「與提供者的授權服務通訊時發生網路錯誤」。

**觸發者：** ` checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ)， `getAuthorization:, `[getAuthorization:withData:](#getAuthZ)

[返回頁首……](#apis)

</br>

### 登出 {#logout}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 您的應用程式會呼叫此方法以起始登出流程。 登出是一系列HTTP重新導向作業的結果，因為使用者需要同時從Primetime驗證伺服器和MVPD伺服器登出。 由於此流程無法使用AccessEnabler程式庫發出的簡單HTTP要求完成， `UIWebView/WKWebView or SFSafariViewController` 控制器必須具現化，才能遵循HTTP重新導向操作。

登出流程與驗證流程的不同之處在於，使用者不需要與 `UIWebView/WKWebView or SFSafariViewController`  控制器。 因此，Adobe建議您在登出過程中隱藏控制項。

採用類似於驗證流程的模式。 iOS AccessEnabler會觸發 `navigateToUrl:` 回呼或 `navigateToUrl:useSVC:` 建立 `UIWebView/WKWebView or SFSafariViewController` 和來載入回呼中提供的URL `url` 引數。 這是後端伺服器上登出端點的URL。 對於tvOS AccessEnabler，兩者皆非 `navigateToUrl:` 回呼或 `navigateToUrl:useSVC:` 已呼叫callback。

在執行數個重新導向作業時，您的應用程式必須監控 `UIWebView/WKWebView or SFSafariViewController `並偵測載入特定自訂URL的時間。 請注意，這個特定自訂URL實際上無效，控制器並非打算實際載入此URL。 應用程式必須將其解譯為登出流程已完成，且關閉控制器是安全的訊號。 當控制器載入這個特定的自訂URL時，您的應用程式必須關閉控制器並呼叫AccessEnabler的 `handleExternalURL:url `api方法。 如果您的應用程式需要使用 `SFSafariViewController `控制器特定的自訂URL由您設定的 `application's custom scheme` (例如：`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否則此特定自訂URL會由 `ADOBEPASS_REDIRECT_URL `常數(即 `adobepass://ios.app`)。

最後，AccessEnabler會呼叫 [`setAuthenticationStatus()`](#setAuthNStatus) 狀態碼為0的回呼，表示登出流程成功。

**注意：** 如果使用者使用Apple SSO登入，則會觸發VSA203狀態。 如果是這種情況，應指示使用者也從系統設定登出。 若未這麼做，應用程式重新啟動時，將導致重新驗證。


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：起始登出流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) logout; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**引數：** 無

**觸發的回呼：** `navigateToUrl:, `[`setAuthenticationStatus:errorCode:`](#setAuthNStatus)

 

[返回頁首……](#apis)

</br>

### getselectedprovider {#getSelProv}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 使用此方法可判斷目前選取的提供者。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：判斷目前選取的MVPD</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getSelectedProvider; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**引數：** 無

**觸發的回呼：** [`selectedProvider:`](#selProv)

[返回頁首……](#apis)

</br>

### selectedprovider {#selProv}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回呼，將目前所選MVPD的相關資訊傳送給應用程式。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回呼：目前所選MVPD的相關資訊</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) selectedProvider:(MVPD *)mvpd;</code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**引數**：

* *mvpd*：包含目前所選MVPD相關資訊的物件

**觸發者：** [`getSelectedProvider`](#getSelProv)

[返回頁首……](#apis)

</br>

### getMetadata： {#getMeta}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 使用此方法可擷取AccessEnabler程式庫公開為中繼資料的資訊。 應用程式可透過提供字典來存取此資料 *金鑰* 輸入引數。

程式設計師可以使用兩種中繼資料型別：

* 靜態中繼資料（驗證權杖TTL、授權權杖TTL和裝置ID） 
* 使用者中繼資料（使用者特定資訊，例如使用者ID、郵遞區號；可以在驗證和授權流程期間，從MVPD傳遞至使用者的裝置）

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：查詢AccessEnabler以取得中繼資料</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getMetadata:(NSDictionary *)keyDictionary; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**引數：**

* *索引鍵字典*：字典資料結構，格式如下：
   * 如果索引鍵為 `METADATA_OPCODE_KEY` 而值是 `METADATA_AUTHENTICATION`，則會進行查詢以取得驗證權杖到期時間。
   * 如果索引鍵為 `METADATA_OPCODE_KEY` 而值是 `METADATA_AUTHORIZATION` **和**\
      索引鍵是 `METADATA_RESOURCE_ID_KEY` 且值為特定資源ID，則會進行查詢以獲取與指定資源關聯的授權權杖的到期時間。
   * 如果索引鍵為 `METADATA_OPCODE_KEY` 而值是 `METADATA_DEVICE_ID`，則會執行查詢以獲取目前的裝置id。 請注意，此功能預設為停用，程式設計師應聯絡Adobe以取得有關啟用和費用的資訊。
   * 如果索引鍵為 `METADATA_OPCODE_KEY` 而值是 `METADATA_USER_META` **和** 索引鍵是 `METADATA_USER_META_KEY` 而value是中繼資料的名稱，則會針對使用者中繼資料進行查詢。 可用的使用者中繼資料型別清單：
      * `zip`  — 郵遞區號清單
      * `householdID`  — 家庭識別碼。 在MVPD不支援附屬帳戶的情況下，這將會與 `userID`.
      * `maxRating`  — 使用者的最大家長分級的集合
      * `userID`  — 使用者識別碼。 如果MVPD支援附屬帳戶，且使用者不是主要帳戶， `userID` 將不同於 `householdID.`
      * `channelID`  — 使用者有權檢視的管道清單。
   >[!NOTE]
   >
   >程式設計師可用的實際使用者中繼資料取決於MVPD提供的內容。 此清單將隨著新的中繼資料可用並新增到Primetime驗證系統中而擴展。

**觸發的回呼：** [`setMetadataStatus:encrypted:forKey:andArguments:`](#setMetaStatus)

**更多資訊：** [使用者中繼資料](/help/authentication/user-metadata.md)

[返回頁首……](#apis)

</br>

### presentTVProviderDialog {#presentTvDialog}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 呼叫後由AccessEnabler觸發的回呼[getAuthentication()](#getAuthN) 如果目前的要求者支援至少一個支援SSO的MVPD。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回呼：SSO流程的結果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) presentTvProviderDialog: (UIViewController *) viewController; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v2.0+

**引數**：

* viewController：代表Apple SSO對話方塊。 此viewController需要顯示在畫面上。

**觸發者：** [`getAuthentication`](#getAuthN)

**更多資訊：** [iOS/tvOS單一登入](#presentTvDialog)

[返回頁首……](#apis)

</br>

### dissisTVProviderDialog {#dismissTvDialog}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 使用者關閉Apple SSO對話方塊後，AccessEnabler所觸發的回呼。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回呼：SSO流程的結果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) dismissTvProviderDialog: (UIViewController *) viewController; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v2.0+

**引數**：

* viewController：代表Apple SSO對話方塊。 此viewController需要從畫面中移除。

**觸發者：** 使用者動作

**更多資訊：** [iOS/tvOS單一登入](#presentTvDialog)

[返回頁首……](#apis)

</br>

### setmetadataStatus:encrypted:forKey:andArguments: {#setMetaStatus}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回呼，透過傳遞請求的中繼資料 [`getMetadata:`](#getMeta) 呼叫。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回撥：中繼資料擷取請求的結果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setMetadataStatus:(id)metadata
                 encrypted:(bool)encrypted 
                    forKey:(int)key 
              andArguments:(NSDictionary *)arguments; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**引數**：

* *中繼資料*：要求的中繼資料。 此值是一個 `NSString` 若是靜態中繼資料（驗證TTL、授權TTL、裝置ID）。  請求使用者專屬的中繼資料時，這是一個複雜的物件。 此複雜物件通常是JSON裝載的Objective-C表示法(例如&#39;{&quot;street&quot;： &quot;Main Avenue&quot;， &quot;buildings&quot;： [「150」、「320」]}&#39;在Objective-C中翻譯為NSDictionary(&quot;street&quot; -> &quot;Main Avenue&quot;， &quot;buildings&quot; -> NSArray(&quot;150&quot;， &quot;320&quot;))。   中繼資料JSON物件範例：

```JSON
        {
            updated: 1334243471,
            encrypted: ["encryptedProp"],
            data: {
                zip: ["12345", "34567"],
                maxRating: { 
                    "MPAA": "PG-13",
                    "VCHIP": "TV-Y", 
                    "URL": "http://exam.pl/e/manage/ratings"
                },
                householdID: "3456",
                userID: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
                channelID: ["channel-1", "channel-2"]
            }
```

* *已加密*：指定是否加密擷取的中繼資料的布林值。 此引數僅對使用者中繼資料請求有意義，對始終未加密接收的靜態中繼資料（例如驗證TTL）沒有意義。 如果此引數設為true，則由程式設計師決定是否使用白名單私密金鑰（在中用於簽署請求者ID的相同私密金鑰）執行RSA解密，以取得未加密的使用者中繼資料值。 [`setRequestor:setSignedRequestorId:`](#setReq) 和 `setRequestor:setSignedRequestorId:serviceProviders: `呼叫次數)。

* *金鑰*：用於制定中繼資料擷取要求的索引鍵。

* *引數*：傳遞至的相同字典 [`getMetadata:`](#getMeta) 呼叫。 提供此屬性，是為了讓應用程式可比對要求與回應。

**觸發者：** [`getMetadata:`](#getMeta)

**更多資訊：** [使用者中繼資料](/help/authentication/user-metadata.md)


[返回頁首……](#apis)

</br>

### MVPD {#mvpd}

**檔案：** AccessEnabler/headers/model/MVPD.h

**說明** 說明MVPD物件。 可用於取得MVPD屬性的相關資訊。

**可用性：** v1.0+ [boardingStatus屬性可在v2.2中使用] 

**屬性**：

* (NSString) ID - MVPD ID。
* (NSString) displayName - MVPD名稱。 [這應該用於顯示在選擇器中]
* (NSString) logoURL - MVPD標誌位址。
* (BOOL) enablePlatformServices — 如果為true，則MVPD支援SSO服務，例如 [APPLE SSO](#presentTvDialog).
* (NSString) boardingStatus — 可以有3個值：
   * 無 — MVPD不支援Apple SSO。
   * 選取器 — MVPD可出現在Apple選取器中，但驗證流程會由Adobe完成。
   * 支援 — Apple完全支援MVPD，且將使用Apple的SSO權杖。

[返回頁首……](#apis)

</br>

## 追蹤事件 {#tracking}

AccessEnabler會觸發其他回呼，而此回呼不一定與權益流程相關。 實作 [`sendTrackingData()`](#sendTracking) 回呼函式為選用，但可讓應用程式追蹤特定事件並編譯統計資料，例如成功/失敗的驗證/授權嘗試次數。 

### sendTrackingData:forEventType: {#sendTracking}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler向應用程式發出各種事件（例如驗證/授權流程完成/失敗）的訊號所觸發的回呼。 使用Primetime驗證1.6時，裝置型別、AccessEnabler使用者端型別和作業系統會由報告 [`sendTrackingData()`](#sendTracking). 此 [`sendTrackingData()`](#sendTracking) 回呼會保持回溯相容性。

**回撥：追蹤事件**

```
(void) sendTrackingData:(NSArray *)data 
             forEventType:(int)event;
```

**可用性：** v1.0+

**注意：** 裝置型別和作業系統衍生自使用公用Java程式庫(<http://java.net/projects/user-agent-utils>)和使用者代理字串。 請注意，此資訊僅以粗略的方式提供，以將運作量度劃分為裝置類別，但該Adobe對錯誤結果概不負責。 請據以使用新功能。

* 裝置型別的可能值：
   * `computer`
   * `tablet`
   * `mobile`
   * `gameconsole`
   * `unknown`

* AccessEnabler使用者端型別的可能值：
   * `flash`
   * `html5`
   * `ios`
   * `android`


**引數**：

* *事件*：正在追蹤之事件的程式碼。 追蹤事件型別共有三種：
   * **authorizationDetection：** 每當授權權杖請求傳回時(事件為 `TRACKING_AUTHORIZATION`)
   * **authenticationdetection：** 每當驗證檢查發生時(事件為 `TRACKING_AUTHENTICATION`)
   * **mvpdSelection：** 當使用者在MVPD選擇表單中選取MVPD時(事件為 `TRACKING_GET_SELECTED_PROVIDER`)
* *資料*：與已報告事件相關聯的其他資料。 此資料會以值清單的形式呈現。

**觸發者：** `checkAuthentication, getAuthentication, `[getAuthentication:withData:](#getAuthN)， `checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ)， `getAuthorization:, `[getAuthorization:withData:](#getAuthZ)， `setSelectedProvider:`

解譯「 」中值的指示 *資料* 陣列：

* 適用於trackingEventType `TRACKING_AUTHENTICATION:`
   * **0**  — 權杖要求是否成功(true/false)，如果成功：
   * **1** - MVPD ID字串
   * **2** - GUID （md5雜湊）
   * **3**  — 權杖已存在於快取中(true/false)
   * **4**  — 裝置型別
   * **5** - AccessEnabler使用者端型別
   * **6**  — 作業系統型別

* 適用於trackingEventType `TRACKING_AUTHORIZATION:`
   * **0**  — 權杖要求是否成功(true/false)，如果成功：
   * **1** - MVPD ID
   * **2** - GUID （md5雜湊）
   * **3**  — 權杖已存在於快取中(true/false)
   * **4**  — 錯誤
   * **5**  — 詳細資料
   * **6**  — 裝置型別
   * **7** - AccessEnabler使用者端型別
   * **8**  — 作業系統型別
* 適用於trackingEventType `TRACKING_GET_SELECTED_PROVIDER:`
   * **0**  — 目前所選MVPD的ID
   * **1**  — 裝置型別
   * **2** - AccessEnabler使用者端型別
   * **3**  — 作業系統型別

</br>

## 相關資訊 {#related}

* [iOS整合逐步指南](/help/authentication/iostvos-sdk-cookbook.md)
* [iOS技術概覽](/help/authentication/iostvos-sdk-overview.md)
* [權益流程](/help/authentication/entitlement-flow.md)
   <!--* [Tracking Data in Primetime authentication](https://tve.helpdocsonline.com/tracking-data-in-adobe-pass)-->
