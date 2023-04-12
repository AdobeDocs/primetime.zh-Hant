---
title: iOS/tvOS API參考
description: iOS/tvOS API參考
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '7000'
ht-degree: 0%

---


# iOS/tvOS SDK API參考 {#iostvos-sdk-api-reference}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 簡介 {#intro}

本頁說明iOS/tvOS原生用戶端針對Adobe Primetime驗證公開的方法和回呼函式。 此處所述的方法和回呼函式定義於 `AccessEnabler.h` 和 `EntitlementDelegate.h` 標題檔案；您可以在iOS AccessEnabler SDK中找到它們： `[SDK directory]/AccessEnabler/headers/api/`


相關檔案：

* 如需基本Primetime驗證權限流程的說明，請參閱 [權利流程](/help/authentication/entitlement-flow.md).
* 如需如何使用此API實作Primetime驗證權限流程的逐步說明，請參閱 [iOS整合逐步指南](/help/authentication/iostvos-sdk-cookbook.md).
* 有關最新的iOS AccessEnabler SDK，請參見 [iOS Native Access Enabler Library](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library).

>[!NOTE]
>
>Adobe建議您只使用Primetime驗證 *公共* API:
>
>* 公用API可供使用，並在所有支援的用戶端類型上全面測試。 對於任何公用功能，我們會確定每個用戶端類型都具有相關聯方法的對應版本。
>* 公用API必須盡可能穩定，以支援回溯相容性，並確保合作夥伴整合不會中斷。 不過，對於非公開API，我們保留日後隨時變更其簽名的權利。 如果您遇到無法透過目前公用Primetime驗證API呼叫組合支援的特定流程，最佳方法就是通知我們。 根據您的需求，我們可以修改公用API，並提供穩定的解決方案，以推動未來的發展。


</br>

## API參考 {#apis}

* [init](#initWithSoftwareStatement):softwareStatement — 實例化AccessEnabler物件。

* **[已棄用]** [init](#init)  — 實例化AccessEnabler對象。

* [setOptions:options:](#setOptions)  — 設定全域SDK選項，例如profile或visitorID。

* [setRequestor:](#setReqV3)[requestorID](#setReqV3),[setRequestor:requestorID:serviceProviders:](#setReqV3)  — 建立程式設計師的身份。

* **[已棄用]** [setRequestor:signedRequestorId:](#setReq),[setRequestor:signedRequestorId:serviceProviders:](#setReq)  — 建立程式設計師的身份。

* **[已棄用]** [setRequestor:signedRequestorId:secret:publicKey](#setReq_tvos), [setRequestor:signedRequestorId:serviceProviders:secret:publicKey](#setReq_tvos) — 建立程式設計師的身份。

* [setRequestorComplete:](#setReqComplete)  — 通知您的應用程式配置階段已完成。

* [checkAuthentication](#checkAuthN)  — 檢查當前用戶的驗證狀態。

* [getAuthentication](#getAuthN), [getAuthentication:withData:](#getAuthN)  — 啟動完整驗證工作流。

* [getAuthentication:filter](#getAuthN_filter),[getAuthentication:withData:](#getAuthN)[和篩選](#getAuthN_filter)  — 啟動完整驗證工作流。

* [displayProviderDialog:](#dispProvDialog)  — 通知您的應用程式將適當的UI元素實例化，讓使用者選取MVPD。

* [setSelectedProvider:](#setSelProv)  — 通知AccessEnabler用戶的MVPD選擇。

* [navigateToUrl:](#nav2url)  — 通知您的應用程式，使用者需要顯示MVPD登入頁面。

* [navigateToUrl:useSVC:](#nav2urlSVC)  — 使用SFSafariViewController通知您的應用程式，需要向用戶顯示MVPD登錄頁

* [handleExternalURL:url](#handleExternalURL)  — 完成驗證/註銷流程。

* **[已棄用]** [getAuthenticationToken](#getAuthNToken)  — 從後端伺服器要求驗證Token。

* [setAuthenticationStatus:errorCode:](#setAuthNStatus)  — 通知您的應用程式驗證流程的狀態。

* [checkPreauthorizedResources:](#checkPreauth)  — 確定用戶是否已獲得查看特定受保護資源的授權。

* [checkPreauthorizedResources:cache:](#checkPreauthCache)  — 確定用戶是否已獲得查看特定受保護資源的授權。

* [preauthorizedResources:](#preauthResources)  — 提供已授權用戶查看的資源清單。

* [checkAuthorization:](#checkAuthZ), [checkAuthorization:withData:](#checkAuthZ)  — 檢查當前用戶的授權狀態。

* [getAuthorization:](#getAuthZ), [getAuthorization:withData:](#getAuthZ)  — 啟動授權流程。

* [setToken:forResource:](#setToken)  — 通知您的應用程式授權流程已成功完成。

* [tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed)  — 通知您的應用程式授權流程失敗。

* [註銷](#logout)  — 啟動註銷流程。

* [getSelectedProvider](#getSelProv)  — 確定當前選擇的提供程式。

* [selectedProvider:](#selProv)  — 將目前選取之MVPD的相關資訊傳送至您的應用程式。

* [getMetadata:](#getMeta)  — 檢索AccessEnabler庫作為元資料公開的資訊。

* [presentTvProviderDialog:](#presentTvDialog)  — 通知您的應用程式以顯示Apple SSO對話方塊。

* [disclessTvProviderDialog:](#dismissTvDialog)  — 通知您的應用程式以隱藏Apple SSO對話方塊。

* [setMetadataStatus:encrypted:forKey:andArguments:](#setMetaStatus)  — 傳送 [getMetadata:](#getMeta) 呼叫。

* [sendTrackingData:forEventType:](#sendTracking)  — 提供追蹤資料資訊。

* [MVPD](#mvpd) - MVPD類。 [包含MVPD的相關資訊]

### init:softwareStatement {#initWithSoftwareStatement}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 實例化AccessEnabler對象。 每個應用程式實例應有一個AccessEnabler實例。

| **API呼叫：iOS AccessEnabler建構子** |
| --- |
| `- (id) init:` <br> |
| `(NSString *)softwareStatement;` |


**可用性：** v3.0+

**參數：**

* **softwareStatement:** 用於標識Adobe系統中應用程式的字串。 查看如何獲取軟體陳述式。

[回到最上面……](#apis)



### init - [已棄用]{#init}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 實例化AccessEnabler對象。 每個應用程式實例應有一個AccessEnabler實例。

| API呼叫：iOS AccessEnabler建構子 |
| --- |
| ```- (id) init;``` |

**可用性：** v1.0+ **直到：** v3.0

**參數：** 無

[回到最上面……](#apis)

</br>

### setOptions:options {#setOptions}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 設定全域SDK選項。 它接受NSDictionary作為引數。 字典中的值會連同SDK進行的每個網路呼叫一併傳遞至伺服器。

**注意：** 這些值將獨立於當前流（驗證/授權）傳遞到伺服器。 如果您想要變更值，可以隨時呼叫此方法。

| API呼叫：setOptions |
| --- |
| ```- (void) setOptions:(NSDictionary *)options;``` |

**可用性：** v2.3.0+

**參數：**

* *選項*:包含全域SDK選項的NSDictionary。 目前可使用下列選項：
   * **applicationProfile**  — 可根據此值進行伺服器配置。
   * **visitorID** -Marketing CloudvisitorID。 此值稍後可用於進階分析報表。
   * **handleSVC**  — 指示程式設計師是否將處理SFSafariViewControllers的布爾值。 請參閱 [iOS SDK 3.2+上的SFSafariViewController支援](/help/authentication/sfsafariviewcontroller-support-on-ios-sdk-32.md) 以取得更多詳細資訊。
      * 若設為 **false,** sdk會自動向使用者呈現SFSafariViewController。 SDK將進一步導覽至MVPD登入頁面URL。
      * 若設為 **true,** sdk將 **NOT** 自動向最終用戶提供SFSafariViewController。 SDK將進一步觸發 **navigate(toUrl:{url}, useSVC:YES)**.
* **device\_info**  — 客戶端資訊，如 [傳遞用戶端資訊](/help/authentication/passing-client-information-device-connection-and-application.md).

[回到最上面……](#apis)


### setRequestor:requestorID, setRequestor:requestorID:serviceProviders: {#setReqV3}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 建立程式設計師的身份。 在向Primetime驗證系統的Adobe註冊時，每個程式設計師被分配一個唯一ID。 在處理SSO和遠程令牌時，當應用程式處於後台時，驗證狀態可以改變，當應用程式進入前台時，可以再次調用setRequestor以與系統狀態同步（如果啟用了SSO，則獲取遠程令牌，如果同時發生註銷，則刪除本地令牌）。

伺服器響應包含MVPD的清單以及附加到程式設計師標識的一些配置資訊。 伺服器響應由AccessEnabler代碼在內部使用。 只有操作的狀態（即SUCCESS/FAIL）會透過 `setRequestorComplete:` 回呼。

若 `urls` 參數，則產生的網路呼叫會鎖定預設服務提供者URL:Adobe發行/生產環境。


如果為 `urls` 參數，則產生的網路呼叫會鎖定中提供的所有URL `urls` 參數。 所有配置請求都在單獨的線程中同時觸發。 編譯MVPD清單時，第一回應者優先。 對於清單中的每個MVPD,AccessEnabler會記住關聯服務提供程式的URL。 所有後續的權限請求都會導向至在設定階段與目標MVPD成對之服務提供者相關聯的URL。

| API呼叫：請求者設定 |
| --- |
| ```- (void) setRequestor:(NSString *)requestorID``` |


**可用性：** v3.0+

| API呼叫：請求者設定 |
| --- |
| `- (void) setRequestor:(NSString *)requestorID serviceProviders:(NSArray *)urls;` |


**可用性：** v3.0+

**參數：**

* *requestorID*:與程式設計師關聯的唯一ID。 當您首次註冊Primetime驗證服務時，將由Adobe指派的唯一ID傳遞至您的網站。
* *url*:選用參數；依預設，會使用Adobe服務提供者(http://sp.auth.adobe.com/)。 此陣列可讓您為Adobe提供的驗證和授權服務指定端點（可能會使用不同的執行個體進行除錯）。 您可以使用它來指定多個Primetime驗證服務提供者例項。 執行此操作時，MVPD清單由來自所有服務提供者的端點組成。 每個MVPD都與最快的服務提供商相關聯；即第一個回應且支援該MVPD的提供者。

>[!NOTE]
>
>如果呼叫時沒有 `serviceProviders` 參數，程式庫將從預設服務提供者(即 `https://sp.auth.adobe.com` 針對生產設定檔或 `https://sp.auth-staging.adobe.com` （適用於測試設定檔）。 若 `serviceProviders` 參數，則必須是URL的陣列。從所有指定的端點檢索配置資訊並合併。 如果在不同的服務提供商響應中存在重複資訊，則會解決衝突，以支援響應速度最快的伺服器（即響應時間最短的伺服器優先）。

**已觸發回呼：** [`setRequestorComplete:`](#setReqComplete)

[回到最上面……](#apis)

</br>

### setRequestor:setSignedRequestorId:, setRequestor:setSignedRequestorId:serviceProviders: - [已棄用] {#setReq}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 建立程式設計師的身份。 在向Primetime驗證系統的Adobe註冊時，每個程式設計師被分配一個唯一ID。 處理SSO和遠端代號時，當應用程式在背景時，驗證狀態可能會改變，當應用程式進入前景時，可再次呼叫setRequestor以與系統狀態同步（如果啟用SSO，則擷取遠端代號，若同時發生登出，則刪除本機代號）。

伺服器響應包含MVPD的清單以及附加到程式設計師標識的一些配置資訊。 伺服器響應由AccessEnabler代碼在內部使用。 只有操作的狀態（即SUCCESS/FAIL）會透過 `setRequestorComplete:` 回呼。

若 `urls` 參數，則產生的網路呼叫會鎖定預設服務提供者URL:Adobe發行/生產環境。

如果為 `urls` 參數，則產生的網路呼叫會鎖定中提供的所有URL `urls` 參數。 所有配置請求都在單獨的線程中同時觸發。 編譯MVPD清單時，第一回應者優先。 對於清單中的每個MVPD,AccessEnabler會記住關聯服務提供程式的URL。 所有後續的權限請求都會導向至在設定階段與目標MVPD成對之服務提供者相關聯的URL。

| API呼叫：請求者設定 |
| --- |
| </br>`- (void) setRequestor:(NSString *)requestorID`</br>`signedRequestorID:(NSString *)signedRequestorID;` </br></br> |

**可用性：** v1.0+ **直到：** v3.0

| API呼叫：請求者設定 |
| --- |
| `- (void) setRequestor:(NSString *)requestorID ` <br> `       signedRequestorID:(NSString *)signedRequestorID` <br> `         serviceProviders:(NSArray *)urls;` |

**可用性：** v1.0+ **直到：** v3.0

**參數：**

* *requestorID*:與程式設計師關聯的唯一ID。 在您首次向Primetime驗證服務註冊時，將由Adobe指派的唯一ID傳遞至您的網站。
* *signedRequestorID*: **此參數存在於iOS AccessEnabler 1.2版和更新版本中。** 以您的私密金鑰進行數位簽署的要求者ID副本。 <!--For more details, see [Registering Native Clients](https://tve.helpdocsonline.com/registering-native-clients)-->.
* *url*:選用參數；依預設，會使用Adobe服務提供者(http://sp.auth.adobe.com/)。 此陣列可讓您為Adobe提供的驗證和授權服務指定端點（可能會使用不同的執行個體進行除錯）。 您可以使用它來指定多個Primetime驗證服務提供者例項。 執行此操作時，MVPD清單由來自所有服務提供者的端點組成。 每個MVPD都與最快的服務提供商相關聯；即第一個回應且支援該MVPD的提供者。

**附註：** 如果呼叫時沒有 `serviceProviders` 參數，程式庫將從預設服務提供者(即`https://sp.auth.adobe.com` 針對生產設定檔或 `https://sp.auth-staging.adobe.com` （適用於測試設定檔）。 若 `serviceProviders` 參數，則必須是URL的陣列。從所有指定的端點檢索配置資訊並合併。 如果在不同的服務提供商響應中存在重複資訊，則衝突將被解決，以支援最快響應的伺服器（即，響應時間最短的伺服器優先）。

**已觸發回呼：** [`setRequestorComplete:`](#setReqComplete)


[回到最上面……](#apis)

### setRequestor:setSignedRequestorId:secret:publicKey, setRequestor:setSignedRequestorId:serviceProviders:secret:publicKey - [已棄用] {#setReq_tvos}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 建立程式設計師的身份。 在向Primetime驗證系統的Adobe註冊時，每個程式設計師被分配一個唯一ID。 此設定在應用程式的生命週期中只應執行一次。

伺服器響應包含MVPD的清單以及附加到程式設計師標識的一些配置資訊。 伺服器響應由AccessEnabler代碼在內部使用。 只有操作的狀態（即SUCCESS/FAIL）會透過 `setRequestorComplete:` 回呼。

若 `urls` 參數，則產生的網路呼叫會鎖定預設服務提供者URL:Adobe發行/生產環境。

如果為 `urls` 參數，則產生的網路呼叫會鎖定中提供的所有URL `urls` 參數。 所有配置請求都在單獨的線程中同時觸發。 編譯MVPD清單時，第一回應者優先。 對於清單中的每個MVPD,AccessEnabler會記住關聯服務提供程式的URL。 所有後續的權限請求都會導向至在設定階段與目標MVPD成對之服務提供者相關聯的URL。



<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：請求者設定</th>
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
<th>API呼叫：請求者設定</th>
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

**參數：**

* *requestorID*:與程式設計師關聯的唯一ID。 在您首次向Primetime驗證服務註冊時，將由Adobe指派的唯一ID傳遞至您的網站。
* *signedRequestorID*: **此參數存在於iOS AccessEnabler 1.2版和更新版本中。** 以您的私密金鑰進行數位簽署的要求者ID副本。 <!--For more details, see [Registering Native Clients](https://tve.helpdocsonline.com/registering-native-clients)-->.
* *url*:選用參數；依預設，會使用Adobe服務提供者(http://sp.auth.adobe.com/)。 此陣列可讓您為Adobe提供的驗證和授權服務指定端點（可能會使用不同的執行個體進行除錯）。 您可以使用它來指定多個Primetime驗證服務提供者例項。 執行此操作時，MVPD清單由來自所有服務提供者的端點組成。 每個MVPD都與最快的服務提供商相關聯；即第一個回應且支援該MVPD的提供者。
* secret與publicKey:用來簽署第二個螢幕呼叫的機密和公開金鑰。 如需詳細資訊，請參閱 [無庇護檔案](#create_dev).

如果呼叫時沒有 `serviceProviders` 參數，則程式庫會從預設服務提供者(即 `https://sp.auth.adobe.com` 用於生產設定檔，或是用於測試設定檔的https://sp.auth-staging.adobe.com)。 若 `serviceProviders` 參數，則必須是URL的陣列。從所有指定的端點檢索配置資訊並合併。 如果在不同的服務提供商響應中存在重複資訊，則衝突將被解決，以支援最快響應的伺服器（即，響應時間最短的伺服器優先）。

**已觸發回呼：** [`setRequestorComplete:`](#setReqComplete)

[回到最上面……](#apis)

</br>

### setRequestorComplete: {#setReqComplete}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回調，該回調通知您的應用程式配置階段已完成。 這是一個訊號，表示應用程式可以開始發出權限請求。 在配置階段完成之前，應用程式不能發出任何權限請求。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回撥：請求者配置完成</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestorComplete:(int)status;</code></pre></td>
</tr>
</tbody>
</table>


**可用性：** v1.0+

**參數**:

* *狀態*:可採用下列其中一個值：
   * `ACCESS_ENABLER_STATUS_SUCCESS`  — 已成功完成配置階段
   * `ACCESS_ENABLER_STATUS_ERROR`  — 配置階段失敗

**觸發者：**
`setRequestor:setSignedRequestorId:, `[`setRequestor:setSignedRequestorId:serviceProviders:`](#setReq)

[回到最上面……](#apis)

</br>

### checkAuthentication {#checkAuthN}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 檢查當前用戶的驗證狀態。
它會透過搜尋本機Token儲存空間中的有效驗證Token來執行此作業。 呼叫此方法不會執行網路呼叫。 應用程式使用它來查詢用戶的驗證狀態並相應地更新UI（即更新登錄/註銷UI）。 驗證狀態通過 [`setAuthenticationStatus:errorCode:`](#setAuthNStatus) 回呼。\
 

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

**參數：** 無

**已觸發回呼：**
[`setAuthenticationStatus:errorCode:`](#setAuthNStatus)

[回到最上面……](#apis)

</br>

### getAuthentication, getAuthentication:withData: {#getAuthN}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 啟動完整驗證工作流程。 首先檢查驗證狀態。 如果尚未驗證，則啟動驗證流狀態機：

* 如果上次驗證嘗試成功，則會略過MVPD選取階段，而 [`navigateToUrl:`](#nav2url) 已觸發回呼。 應用程式會使用此回呼來實例化向使用者顯示MVPD登入頁面的WebView控制項。 **[注意：自Access Enabler 1.5起，由於SDK中的限制，此功能不可用].**
* 如果上次驗證嘗試失敗，或使用者明確登出，則 [`displayProviderDialog:`](#dispProvDialog) 已觸發回呼。 您的應用程式會使用此回呼來顯示MVPD選取UI。 此外，您的應用程式需要透過 [`setSelectedProvider:`](#setSelProv) 方法。

當使用者的認證在MVPD登入頁面上驗證時，您的應用程式必須監控當使用者在MVPD的登入頁面驗證時發生的多個重新導向操作。 輸入正確的憑證時，WebView控制項會重新導向至 `ADOBEPASS_REDIRECT_URL` 常數。 此URL不打算由WebView載入。 應用程式必須截取此URL，並將此事件解譯為登入階段完成的訊號。 然後，它應將控制權交給AccessEnabler以完成驗證流程(通過調用 [handleExternalURL](#handleExternalURL) 方法)。

最後，驗證狀態通過 [setAuthenticationStatus:errorCode:](#setAuthNStatus) 回呼。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：啟動驗證流程</th>
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
<th>API呼叫：啟動驗證流程</th>
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

**參數：**

* *forceAuthn*:此標幟指定是否應啟動驗證流程，而不論使用者是否已通過驗證。
* *資料*:包含要傳送至付費電視通行證服務之鍵值值組的字典。 Adobe可以使用此資料來啟用未來功能，而不需變更SDK。

**已觸發回呼：** ` setAuthenticationStatus:errorCode:, `[`displayProviderDialog:`](#dispProvDialog)`,`` sendTrackingData:forEventType:`


[回到最上面……](#apis)

</br>

### getAuthentication:filter, getAuthentication:withData:和篩選 {#getAuthN_filter}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 啟動完整驗證工作流程。 首先檢查驗證狀態。 如果尚未驗證，則啟動驗證流狀態機：

* [presentTvProviderDialog()](#presentTvDialog) 如果目前要求者至少有一個支援SSO的MVPD，則會呼叫。 如果沒有MVPD支援SSO，則傳統驗證流程將開始，且會忽略篩選參數。
* 使用者完成Apple SSO流程後 [disclessTvProviderDialog()](#dismissTvDialog) 將會觸發，驗證程式將會完成。

最後，驗證狀態通過 [setAuthenticationStatus:errorCode:](#setAuthNStatus) 回呼。

**可用性：** v2.4+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：啟動驗證流程</th>
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
<th>API呼叫：啟動驗證流程</th>
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

 

**參數：**

* *forceAuthn*:此標幟指定是否應啟動驗證流程，而不論使用者是否已通過驗證。
* *資料*:包含要傳送至付費電視通行證服務之鍵值值組的字典。 Adobe可以使用此資料來啟用未來功能，而不需變更SDK。 
* 篩選：包含兩個MVPD ID清單的字典，應會出現在Apple SSO對話方塊中。 任何不支援SSO的MVPD都會被忽略，但會遵守順序。 字典需要兩個鍵：
   * TV\_PROVIDERS:選擇器中應出現的清單，其中包含所有MVPD
   * 精選\_TV\_PROVIDERS:清單中應標示為「精選」中精選的所有MVPD。 TV\_PROVIDERS清單中也必須指定此清單中的MVPD。

**可用性：** v2.0 - v2.3.1


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：啟動驗證流程</th>
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
<th>API呼叫：啟動驗證流程</th>
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

 

**參數：**

* *forceAuthn*:此標幟指定是否應啟動驗證流程，而不論使用者是否已通過驗證。
* *資料*:包含要傳送至付費電視通行證服務之鍵值值組的字典。 Adobe可以使用此資料來啟用未來功能，而不需變更SDK。 
* 篩選：應出現在Apple SSO對話方塊中的MVPD ID清單。 任何不支援SSO的MVPD都會被忽略，但會遵守順序。

**已觸發回呼：** `setAuthenticationStatus:errorCode:, presentTvProviderDialog, dismissTvProviderDialog`


[回到最上面……](#apis)

</br>

#### displayProviderDialog: {#dispProvDialog}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回呼，通知應用程式需要具現化適當的UI元素，以允許使用者選取所需的MVPD。 回呼會提供MVPD物件清單，其中包含可協助正確建立選取UI面板的其他資訊（例如指向MVPD標誌的URL、好記的顯示名稱等）

一旦使用者選取了所需的MVPD，上層應用程式就需要透過呼叫來繼續驗證流程 `setSelectedProvider:` 並傳遞與使用者選取相對應之MVPD的ID。

**中止驗證流程**  — 此時，使用者能夠按下「返回」按鈕，這等同於中止驗證流程。 在該案例中，您的應用程式必須呼叫 [setSelectedProvider:](#setSelProv) 方法，將null作為參數傳遞，使AccessEnabler有機會重置其身份驗證狀態機。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回撥：顯示MVPD選擇UI</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) displayProviderDialog:(NSArray *)mvpds;</code></pre></td>
</tr>
</tbody>
</table>


**可用性：** v1.0+

**參數**:

* *mvpds*:MVPD物件清單，其中包含應用程式可用於建立MVPD選取UI元素的MVPD相關資訊。

**觸發者：** ` getAuthentication, `[getAuthentication:withData:](#getAuthN),` getAuthorization:, `[getAuthorization:withData:](#getAuthZ)


[回到最上面……](#apis)

</br>

#### setSelectedProvider: {#setSelProv}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 應用程式會呼叫此方法，以通知Access Enabler使用者的MVPD選擇。 應用程式可以使用此方法來選擇或更改用於身份驗證的服務提供商。

如果所選MVPD是TempPass MVPD，則它將自動使用該MVPD進行驗證，而無需在之後調用getAuthentication()。

請注意，在getAuthentication()方法上提供額外參數的促銷臨時通行證則無法這麼做。

傳遞時 *null* 作為參數，Access Enabler假定用戶已取消身份驗證流（即按下「返回」按鈕），並通過重置身份驗證狀態機和調用 [setAuthenticationStatus:errorCode:](#setAuthNStatus) 以回呼 `AccessEnabler.PROVIDER_NOT_SELECTED_ERROR` 錯誤代碼。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：設定當前選擇的提供程式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setSelectedProvider:(NSString *)mvpdId;</code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**參數：** 無

**已觸發回呼：** ` setAuthenticationStatus:errorCode:,sendTrackingData:forEventType:,  `[`navigateToUrl:`](#nav2url)

[回到最上面……](#apis)

</br>

#### navigateToUrl: {#nav2url}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明：** 由AccessEnabler觸發的回呼，請求您的應用程式實例化UIWebView/WKWebView控制器並載入回呼中提供的URL **`url`** 參數。 回呼會傳遞 **`url`** 參數，表示驗證端點的URL或登出端點的URL。

作為UIWebView/WKWebView` `controller執行數個重新導向，您的應用程式必須監控控制器的活動，並偵測其載入由 `ADOBEPASS_REDIRECT_URL `常數(即 `adobepass://ios.app`)。 請注意，此特定自訂URL實際上無效，且並非供控制器實際載入。 您的應用程式只能將它解釋為驗證或註銷流程已完成且關閉控制器是安全的信號。 當控制器載入此特定自定義URL時，您的應用程式必須關閉UIWebView/WKWebView並調用AccessEnabler的 `handleExternalURL:url `API方法。

**注意：** 請注意，若是驗證流程，則表示使用者有能力按下「上一步」按鈕，這等同於驗證流程中止。 在這種情況下，您的應用程式必須呼叫 [setSelectedProvider:](#setSelProv) 傳遞 **`nil`** 作為參數，並讓AccessEnabler有機會重置其身份驗證狀態機。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回撥：顯示MVPD登入頁面</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) navigateToUrl:(NSString *)url; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**參數**:

* *url*:指向MVPD登入頁面的URL

**觸發者：** [setSelectedProvider:](#setSelProv)

 

[回到最上面……](#apis)

</br>

#### navigateToUrl:useSVC: {#nav2urlSVC}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明：** 由AccessEnabler觸發的回調，而非 `navigateToUrl:` 回撥，以備應用程式先前透過手動Safari檢視控制器(SVC)處理 [setOptions(\[&quot;handleSVC&quot;:true&quot;\])](#setOptions) 呼叫，且僅限於需要Safari檢視控制器(SVC)的MVPD時。 對於所有其他MVPD, `navigateToUrl:` 將呼叫callback。 請參閱[iOS SDK 3.2+上的SFSafariViewController支援](/help/authentication/sfsafariviewcontroller-support-on-ios-sdk-32.md) 有關如何管理Safari視圖控制器(SVC)的詳細資訊。

類似於 `navigateToUrl:` 回撥 `navigateToUrl:useSVC:` 由AccessEnabler觸發，請求應用程式實例化 `SFSafariViewController` 控制器和，以載入回呼中提供的URL **`url`** 參數。 回呼會傳遞 **`url`** 參數，表示驗證端點的URL或註銷端點的URL，以及 **`useSVC`** 參數，指定應用程式必須使用 `SFSafariViewController`.

作為 `SFSafariViewController` 控制器會執行數個重新導向，您的應用程式必須監控控制器的活動，並偵測其載入您所定義之特定自訂URL的時刻 `application's custom scheme` (例如** **`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)。 請注意，此特定自訂URL實際上無效，且並非供控制器實際載入。 您的應用程式只能將它解釋為驗證或註銷流程已完成且關閉控制器是安全的信號。 當控制器載入此特定自訂URL時，您的應用程式必須關閉 `SFSafariViewController` 並調用AccessEnabler的 `handleExternalURL:url `API方法。

**注意：** 請注意，若是驗證流程，則表示使用者有能力按下「上一步」按鈕，這等同於驗證流程中止。 在這種情況下，您的應用程式必須呼叫 [setSelectedProvider:](#setSelProv) 傳遞 **`nil`** 作為參數，並讓AccessEnabler有機會重置其身份驗證狀態機。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回撥：在SFSafariViewController中顯示MVPD登錄頁</th>
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

**參數**:

* *url:* 指向MVPD登入頁面的URL
* *useSVC:* 是否應在SFSafariViewController中載入url。

**觸發者：**[ setOptions:](#setOptions) befor [setSelectedProvider:](#setSelProv) 

[回到最上面……](#apis)

</br>

#### handleExternalURL:url {#handleExternalURL}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 應用程式會呼叫此方法以完成驗證或登出流程。 您的應用程式偵測到 `UIWebView/WKWebView or SFSafariViewController` 控制器會重新導向至特定自訂URL。 若您的應用程式需要使用 `SFSafariViewController `控制器由 `application's custom scheme` (例如`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否則此特定自訂URL會由 `ADOBEPASS_REDIRECT_URL `常數(即 `adobepass://ios.app`)。

如果驗證流，AccessEnabler將通過從後端伺服器中檢索驗證令牌並將其本地儲存到令牌儲存器來完成該流。 AccessEnabler將通過調用 `setAuthenticationStatus()`<!--(http://tve.helpdocsonline.com/ios-technical-overview#setAuthNStatus)--> 狀態代碼為1的回呼表示成功。 如果執行這些步驟期間發生錯誤，則 `setAuthenticationStatus()`<!--(http://tve.helpdocsonline.com/ios-technical-overview#setAuthNStatus)--> 狀態碼為0時觸發回呼，表示驗證失敗，以及相應的錯誤碼。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：完成驗證或註銷流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code> (void) handleExternalURL:(NSString *)url; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v3.0+

**參數：** 

* *url*:從 ` UIWebView/WKWebView or SFSafariViewController ` 控制為字串。


**已觸發回呼：** `setAuthenticationStatus:errorCode, sendTrackingData:forEventType:`

[回到最上面……](#apis)

</br>

#### getAuthenticationToken - [已棄用] {#getAuthNToken}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 從後端伺服器要求驗證Token以完成驗證流程。 您的應用程式只應在回應MVPD登入頁面所在的WebView控制項，重新導向至由 `ADOBEPASS_REDIRECT_URL` 常數。\
 

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

**參數：** 無

**已觸發回呼：** `setAuthenticationStatus:errorCode,sendTrackingData:forEventType:`

[回到最上面……](#apis)

&lt;/br

#### setAuthenticationStatus:errorCode: {#setAuthNStatus}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回調，該回調通知應用程式身份驗證流的狀態。 有許多地方可能會因為用戶交互或其他意外情況（如網路連接問題等）而導致此流失敗。 此回呼會通知應用程式驗證流程的成功/失敗狀態，並視需要提供關於失敗原因的其他資訊。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回撥：報告驗證流程的狀態</th>
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

**參數**:

* *狀態*:可採用下列其中一個值：
   * `ACCESS_ENABLER_STATUS_SUCCESS`  — 驗證流程已成功完成
   * `ACCESS_ENABLER_STATUS_ERROR`  — 驗證流失敗
* *代碼*:失敗原因。 若 *狀態* is `ACCESS_ENABLER_STATUS_SUCCESS`，然後 *代碼* 是空字串(亦即，由 `USER_AUTHENTICATED` 常數)。 如果失敗，此參數可取用下列其中一個值：
   * `USER_NOT_AUTHENTICATED_ERROR`  — 未驗證用戶。 回應 [checkAuthentication:](#checkAuthN) 當本機權杖快取中沒有有效的驗證權杖時，方法會呼叫。
   * `PROVIDER_NOT_SELECTED_ERROR`  — 在上層應用程式通過後， AccessEnabler已重置身份驗證狀態機 *null* to [`setSelectedProvider:`](#setSelProv) 中止驗證流程。  用戶可能已取消身份驗證流（即按「返回」按鈕）。
   * `GENERIC_AUTHENTICATION_ERROR`  — 由於網路不可用或用戶明確取消身份驗證流等原因，身份驗證流失敗。

**觸發者：** ` checkAuthentication, getAuthentication, `[getAuthentication:withData:](#getAuthN),` checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ)

[回到最上面……](#apis)

</br>

### checkPreauthorizedResources: {#checkPreauth}


**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 此方法由應用程式用於確定用戶是否已獲得查看特定受保護資源的授權。 此方法的主要用途是擷取用於裝飾UI的資訊 **（例如，使用鎖定和解鎖表徵圖指示訪問狀態）。**

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：設定當前選擇的提供程式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.3+

**參數：**

* *資源：* 應檢查授權的資源陣列。 清單中的每個元素都應是代表資源ID的字串。 資源ID受與呼叫中的資源ID相同的限制，即，它應是程式設計師和MVPD或媒體RSS片段之間建立的商定值。

**已觸發回呼：** [`preauthorizedResources:`](#preauthResources)

[回到最上面……](#apis)

</br>

### checkPreauthorizedResources:cache: {#checkPreauthCache}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 此方法由應用程式用於確定用戶是否已獲得查看特定受保護資源的授權。 此方法的主要用途是擷取用於裝飾UI的資訊（例如，使用鎖定和解鎖圖示指示存取狀態）。 此 **快取** 參數控制是否使用內部快取來解析資源。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：設定當前選擇的提供程式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources cache:(BOOL)cache; </code></pre></td>
</tr>
</tbody>
</table>

 

**可用性：** v3.1+

 

**參數：**

* *資源：* 應檢查授權的資源陣列。 清單中的每個元素都應是代表資源ID的字串。 資源ID受與 `getAuthorization:` 呼叫，即，它應是程式設計師和MVPD或媒體RSS片段之間建立的商定值。
* *快取：* 指定是否使用內部快取來解析資源的布林值。 如果為false，系統會略過快取，導致每次呼叫此API時都會進行伺服器呼叫。

**已觸發回呼：** [`preauthorizedResources:`](#preauthResources)

[回到最上面……](#apis)

</br>

### preauthorizedResources: {#preauthResources}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明：** 由觸發的回呼 `checkPreauthorizedResources:`. 提供已授權用戶查看的資源清單。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：設定當前選擇的提供程式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.3+

**參數：**

* `resources`:已授權使用者檢視的資源陣列。

**觸發者：** [`checkPreauthorizedResources:`](#checkPreauth)

 

[回到最上面……](#apis)

</br>

### checkAuthorization:, checkAuthorization:withData: {#checkAuthZ}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 此方法由應用程式用來檢查授權狀態。 首先檢查驗證狀態。 若未驗證，則 [tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed) 回呼會觸發，方法會退出。 如果使用者已驗證，也會觸發授權流程。 請參閱 [`getAuthorization:`](#getAuthZ) 方法。


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

**參數：**

* *資源*:用戶向其請求授權的資源ID。
* *資料*:包含要傳送至付費電視通行證服務之鍵值值組的字典。 Adobe可以使用此資料來啟用未來功能，而不需變更SDK。 

**已觸發回呼：**
[tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed)`,setToken:forResource:, sendTrackingData:forEventType:, setAuthenticationStatus:errorCode:`

[回到最上面……](#apis)

</br>

### getAuthorization:, getAuthorization:withData: {#getAuthZ}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 此方法由應用程式用來啟動授權流程。 如果用戶尚未驗證，則還會啟動驗證流。 如果用戶通過驗證，AccessEnabler將繼續發出授權令牌（如果本地令牌快取中沒有有效的授權令牌）和短期媒體令牌的請求。 一旦獲得短媒體令牌，則認為授權流程已完成。 此 [setToken:forResource:](#setToken) 會觸發回呼，並將短媒體代號以參數的形式傳送至應用程式。 若因任何原因，授權會失敗， [tokenRequestFailed:forEventType:](#tokenReqFailed) 會觸發回呼，並提供錯誤碼/詳細資料。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：啟動授權流程</th>
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
<th>API呼叫：啟動授權流程</th>
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

**參數：**

* *資源*:用戶向其請求授權的資源ID。
* *資料*:包含要傳送至付費電視通行證服務之鍵值值組的字典。 Adobe可以使用此資料來啟用未來功能，而不需變更SDK。 

**已觸發回呼：** `tokenRequestFailed:errorCode:errorDescription:, setToken:forResource:,sendTrackingData:forEventType:`

**已觸發其他回呼：**\
此方法也可以觸發下列回呼（如果也啟動驗證流程）: `setAuthenticationStatus:errorCode:`, `displayProviderDialog:`\
 
**注意：請使用checkAuthorization:/ checkAuthorization:withData: 而不是getAuthorization: / getAuthorization:withData: 盡可能。 getAuthorization: / getAuthorization:withData: 方法將啟動完整驗證流程（如果用戶未通過驗證），這可能導致程式設計師端的複雜實現。**

[回到最上面……](#apis)

</br>

### setToken:forResource: {#setToken}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回調，該回調通知您的應用程式授權流程已成功完成。 短期媒體代號也會以參數的形式傳送。\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回撥：已成功完成授權流程</th>
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

**參數**:

* *token*:短暫的媒體代號
* *資源*:獲得授權的資源

**觸發者：** [checkAuthorization:](#checkAuthZ)` , `[checkAuthorization:withData:](#checkAuthZ),` `[getAuthorization:](#getAuthZ), [getAuthorization:withData:](#getAuthZ)

[回到最上面……](#apis)

</br>

### tokenRequestFailed:errorCode:errorDescription: {#tokenReqFailed}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回調，該回調通知上層應用程式授權流失敗。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回撥：授權流失敗</th>
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

**參數**:

* *資源*:獲得授權的資源。
* *代碼*:與失敗情境相關聯的錯誤代碼。 可能的值：
   * `USER_NOT_AUTHORIZED_ERROR`  — 用戶無法為給定資源授權
* *說明*:有關失敗情況的其他詳細資訊。 如果此描述性字串因任何原因不可用，Primetime驗證會傳送空字串 **(&quot;&quot;)**. \
   MVPD可使用此字串來傳遞自訂錯誤訊息或銷售相關訊息。 例如，如果訂閱者被拒絕對資源進行授權，MVPD可能會傳送如下訊息：「您目前無法在套件中存取此管道。 如果要升級包，請按一下 **此處**.&quot; 該消息由Primetime身份驗證通過此回調傳遞給程式設計師，他們可以選擇顯示或忽略它。 Primetime驗證也可使用此參數來提供可能導致錯誤的條件通知。 例如，「與提供者的授權服務通信時發生網路錯誤」。

**觸發者：** ` checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ), `getAuthorization:, `[getAuthorization:withData:](#getAuthZ)

[回到最上面……](#apis)

</br>

### 註銷 {#logout}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 應用程式會呼叫此方法以起始登出流程。 登出是一系列HTTP重新導向操作的結果，因為使用者需要從Primetime驗證伺服器以及MVPD的伺服器登出。 因為此流無法通過AccessEnabler庫發出的簡單HTTP請求完成， `UIWebView/WKWebView or SFSafariViewController` 控制器需要具現化，才能遵循HTTP重新導向操作。

註銷流與驗證流不同，因為用戶不需要與 `UIWebView/WKWebView or SFSafariViewController`  控制者。 因此，Adobe建議您在註銷過程中隱藏控制項（即隱藏）。

採用與驗證流類似的模式。 iOS AccessEnabler觸發 `navigateToUrl:` callback或 `navigateToUrl:useSVC:` 建立 `UIWebView/WKWebView or SFSafariViewController` 控制器和，以載入回呼中提供的URL `url` 參數。 這是後端伺服器上登出端點的URL。 對於tvOS AccessEnabler , `navigateToUrl:` callback或 `navigateToUrl:useSVC:` 呼叫回呼。

當它經過數個重新導向時，您的應用程式必須監控 `UIWebView/WKWebView or SFSafariViewController `controller和偵測載入特定自訂URL的時機。 請注意，此特定自訂URL實際上無效，且並非供控制器實際載入。 您的應用程式只能將它解釋為註銷流程已完成且關閉控制器是安全的信號。 當控制器載入此特定自定義URL時，您的應用程式必須關閉控制器並調用AccessEnabler的 `handleExternalURL:url `API方法。 若您的應用程式需要使用 `SFSafariViewController `控制器由 `application's custom scheme` (例如`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否則此特定自訂URL會由 `ADOBEPASS_REDIRECT_URL `常數(即 `adobepass://ios.app`)。

最後，AccessEnabler將調用 [`setAuthenticationStatus()`](#setAuthNStatus) 狀態代碼為0的回呼，表示登出流程成功。

**注意：** 如果使用Apple SSO登入，則會觸發VSA203狀態。 如果是這種情況，應指示用戶也從系統設定註銷。 若無法這麼做，應用程式重新啟動時，將會重新驗證。


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：啟動註銷流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) logout; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**參數：** 無

**已觸發回呼：** `navigateToUrl:, `[`setAuthenticationStatus:errorCode:`](#setAuthNStatus)

 

[回到最上面……](#apis)

</br>

### getSelectedProvider {#getSelProv}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 使用此方法來確定當前選擇的提供程式。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：決定目前選取的MVPD</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getSelectedProvider; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**參數：** 無

**已觸發回呼：** [`selectedProvider:`](#selProv)

[回到最上面……](#apis)

</br>

### selectedProvider {#selProv}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回調，該回調將有關當前所選MVPD的資訊提供給應用程式。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回撥：目前選取之MVPD的相關資訊</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) selectedProvider:(MVPD *)mvpd;</code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**參數**:

* *mvpd*:包含當前所選MVPD資訊的對象

**觸發者：** [`getSelectedProvider`](#getSelProv)

[回到最上面……](#apis)

</br>

### getMetadata: {#getMeta}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**說明：** 使用此方法可檢索AccessEnabler庫作為元資料公開的資訊。 應用程式可提供以字典為基礎的存取資料 *key* 輸入參數。

程式設計師有兩種可用的元資料：

* 靜態中繼資料（驗證Token TTL、授權Token TTL和裝置ID） 
* 使用者中繼資料(使用者專屬資訊，例如使用者ID、郵遞區號；可在驗證和授權流程期間，從MVPD傳遞至使用者裝置)

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API呼叫：查詢AccessEnabler中的元資料</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getMetadata:(NSDictionary *)keyDictionary; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**參數：**

* *keyDictionary*:字典資料結構，格式如下：
   * 如果鍵為 `METADATA_OPCODE_KEY` 和值 `METADATA_AUTHENTICATION`，則會進行查詢以取得驗證Token過期時間。
   * 如果鍵為 `METADATA_OPCODE_KEY` 和值 `METADATA_AUTHORIZATION` **和**\
      key `METADATA_RESOURCE_ID_KEY` 並且值是特定資源ID，然後進行查詢以獲得與指定資源相關聯的授權令牌的到期時間。
   * 如果鍵為 `METADATA_OPCODE_KEY` 和值 `METADATA_DEVICE_ID`，然後進行查詢以取得目前的裝置id。 請注意，此功能預設為停用，程式設計人員應聯絡Adobe，以取得啟用和費用的相關資訊。
   * 如果鍵為 `METADATA_OPCODE_KEY` 和值 `METADATA_USER_META` **和** key `METADATA_USER_META_KEY` 而值是中繼資料的名稱，則會為使用者中繼資料建立查詢。 可用的用戶元資料類型清單：
      * `zip`  — 郵遞區號清單
      * `householdID`  — 家庭標識符。 如果MVPD不支援子帳戶，則會等同於 `userID`.
      * `maxRating`  — 用戶最高父母評級的集合
      * `userID`  — 使用者識別碼。 如果MVPD支援子帳戶，且使用者不是主帳戶， `userID` 將不同於 `householdID.`
      * `channelID`  — 使用者有權檢視的管道清單。
   >[!NOTE]
   >
   >程式設計師可用的實際用戶元資料取決於MVPD提供的內容。 當新中繼資料可供使用並新增至Primetime驗證系統時，此清單會擴充。

**已觸發回呼：** [`setMetadataStatus:encrypted:forKey:andArguments:`](#setMetaStatus)

**更多資訊：** [使用者中繼資料](/help/authentication/user-metadata.md)

[回到最上面……](#apis)

</br>

### presentTVProviderDialog {#presentTvDialog}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 在調用後由AccessEnabler觸發的回調[getAuthentication()](#getAuthN) 如果目前請求者支援至少一個具有SSO支援的MVPD。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回撥：SSO流的結果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) presentTvProviderDialog: (UIViewController *) viewController; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v2.0+

**參數**:

* viewController:代表Apple SSO對話方塊。 此viewController必須顯示在螢幕上。

**觸發者：** [`getAuthentication`](#getAuthN)

**更多資訊：** [iOS/tvOS單一登入](#presentTvDialog)

[回到最上面……](#apis)

</br>

### discupsTVProviderDialog {#dismissTvDialog}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 用戶關閉Apple SSO對話框後，AccessEnabler觸發的回調。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回撥：SSO流的結果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) dismissTvProviderDialog: (UIViewController *) viewController; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v2.0+

**參數**:

* viewController:代表Apple SSO對話方塊。 需要從螢幕中刪除此viewController。

**觸發者：** 使用者動作

**更多資訊：** [iOS/tvOS單一登入](#presentTvDialog)

[回到最上面……](#apis)

</br>

### setMetadataStatus:encrypted:forKey:andArguments: {#setMetaStatus}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回調，該AccessEnabler通過 [`getMetadata:`](#getMeta) 呼叫。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回撥：元資料檢索請求的結果</th>
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

**參數**:

* *中繼資料*:請求的元資料。 此值是 `NSString` 若是靜態中繼資料（驗證TTL、授權TTL、裝置ID）。  請求使用者特定中繼資料時，這是複雜的物件。 此複雜物件通常是JSON裝載的Objective-C表示(例如&#39;{&quot;street&quot;:「主大道」、「建築」： [「150」、「320」]}&#39;在Objective-C中翻譯為NSDictionary(&quot;street&quot; -> &quot;Main Avenue&quot;, &quot;boulds&quot; -> NSArray(&quot;150&quot;, &quot;320&quot;))。   範例中繼資料JSON物件：

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

* *加密*：指定擷取的中繼資料是否加密的布林值。 此參數只對使用者中繼資料請求有顯著意義，對於一律未加密接收的靜態中繼資料（例如驗證TTL）則沒有意義。 如果此參數設定為true，則由程式設計師通過使用白名單私鑰執行RSA解密來獲取未加密的用戶元資料值（該私鑰與在中用於簽名請求者ID的私鑰相同） [`setRequestor:setSignedRequestorId:`](#setReq) 和 `setRequestor:setSignedRequestorId:serviceProviders: `呼叫)。

* *key*:用於制定元資料檢索請求的鍵。

* *引數*:那本字典是 [`getMetadata:`](#getMeta) 呼叫。 這可讓應用程式將要求與回應相符。

**觸發者：** [`getMetadata:`](#getMeta)

**更多資訊：** [使用者中繼資料](/help/authentication/user-metadata.md)


[回到最上面……](#apis)

</br>

### MVPD {#mvpd}

**檔案：** AccessEnabler/headers/model/MVPD.h

**說明** 說明MVPD物件。 可用來取得MVPD屬性的相關資訊。

**可用性：** v1.0+ [v2.2提供boardingStatus屬性] 

**屬性**:

* (NSString)ID - MVPD ID。
* (NSString)displayName - MVPD名稱。 [此值應用於顯示在選取器中]
* (NSString)logoURL - MVPD標誌位址。
* (BOOL)enablePlatformServices — 如果為true,MVPD會支援類似 [AppleSSO](#presentTvDialog).
* (NSString)boodingStatus — 可以有3個值：
   * nil - MVPD不支援Apple SSO。
   * 選擇器 — MVPD可顯示在Apple選擇器中，但驗證流程由Adobe完成。
   * 支援 — Apple完全支援MVPD，且將使用Apple的SSO代號。

[回到最上面……](#apis)

</br>

## 追蹤事件 {#tracking}

AccessEnabler會觸發與權限流程不一定相關的附加回調。 實作 [`sendTrackingData()`](#sendTracking) callback函式是可選函式，但它使應用程式能夠跟蹤特定事件並編譯統計資訊，如成功/失敗的身份驗證/授權嘗試次數。 

### sendTrackingData:forEventType: {#sendTracking}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler向應用程式發出信號時觸發的回調，該信號會發生各種事件，如驗證/授權流的完成/失敗。 使用Primetime身份驗證1.6時，將報告設備類型、 AccessEnabler客戶端類型和作業系統 [`sendTrackingData()`](#sendTracking). 此 [`sendTrackingData()`](#sendTracking) 回呼仍回溯相容。

**回撥：追蹤事件**

```
(void) sendTrackingData:(NSArray *)data 
             forEventType:(int)event;
```

**可用性：** v1.0+

**注意：** 裝置類型和作業系統是透過使用公用Java程式庫(<http://java.net/projects/user-agent-utils>)和使用者代理字串。 請注意，此資訊僅作為將操作量度劃分為裝置類別的粗略方式提供，但該Adobe對錯誤的結果不負責。 請據此使用新功能。

* 設備類型的可能值：
   * `computer`
   * `tablet`
   * `mobile`
   * `gameconsole`
   * `unknown`

* AccessEnabler客戶端類型的可能值：
   * `flash`
   * `html5`
   * `ios`
   * `android`


**參數**:

* *事件*:正在追蹤之事件的程式碼。 有三種可能的追蹤事件類型：
   * **authorizationDetection:** 授權Token請求傳回時(事件為 `TRACKING_AUTHORIZATION`)
   * **authenticationDetection:** 任何時候進行驗證檢查(事件為 `TRACKING_AUTHENTICATION`)
   * **mvpdSelection:** 當使用者在MVPD選取表單中選取MVPD時(事件為 `TRACKING_GET_SELECTED_PROVIDER`)
* *資料*:與報告事件相關聯的其他資料。 此資料會以值清單的形式呈現。

**觸發者：** `checkAuthentication, getAuthentication, `[getAuthentication:withData:](#getAuthN), `checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ), `getAuthorization:, `[getAuthorization:withData:](#getAuthZ), `setSelectedProvider:`

解譯 *資料* 陣列：

* 針對trackingEventType `TRACKING_AUTHENTICATION:`
   * **0**  — 代號要求是否成功(true/false)，如果成功：
   * **1** - MVPD ID字串
   * **2** - GUID（md5雜湊）
   * **3**  — 已在快取中的Token(true/false)
   * **4**  — 設備類型
   * **5** - AccessEnabler客戶端類型
   * **6**  — 作業系統類型

* 針對trackingEventType `TRACKING_AUTHORIZATION:`
   * **0**  — 代號要求是否成功(true/false)，如果成功：
   * **1** - MVPD ID
   * **2** - GUID（md5雜湊）
   * **3**  — 已在快取中的Token(true/false)
   * **4**  — 錯誤
   * **5**  — 詳細資訊
   * **6**  — 設備類型
   * **7** - AccessEnabler客戶端類型
   * **8**  — 作業系統類型
* 針對trackingEventType `TRACKING_GET_SELECTED_PROVIDER:`
   * **0**  — 目前選取的MVPD ID
   * **1**  — 設備類型
   * **2** - AccessEnabler客戶端類型
   * **3**  — 作業系統類型

</br>

## 相關資訊 {#related}

* [iOS整合逐步指南](/help/authentication/iostvos-sdk-cookbook.md)
* [iOS技術概述](/help/authentication/iostvos-sdk-overview.md)
* [權利流程](/help/authentication/entitlement-flow.md)
   <!--* [Tracking Data in Primetime authentication](https://tve.helpdocsonline.com/tracking-data-in-adobe-pass)-->
