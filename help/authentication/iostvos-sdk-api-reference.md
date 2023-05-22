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
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 導言 {#intro}

本頁介紹iOS/tvOS本機客戶端為Adobe Primetime身份驗證而公開的方法和回調函式。 此處介紹的方法和回調函式在 `AccessEnabler.h` 和 `EntitlementDelegate.h` 標頭檔；您可以在iOSAccessEnabler SDK中找到它們： `[SDK directory]/AccessEnabler/headers/api/`


相關文檔：

* 有關基本的黃金時段身份驗證權利流程的說明，請參閱 [權利流](/help/authentication/entitlement-flow.md)。
* 有關如何使用此API實現黃金時段身份驗證權利流的逐步介紹，請參見 [iOS整合烹飪書](/help/authentication/iostvos-sdk-cookbook.md)。
* 有關最新的iOSAccessEnabler SDK，請參見 [iOS本機Access啟用程式庫](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library)。

>[!NOTE]
>
>Adobe鼓勵您僅使用黃金時段身份驗證 *公共* API:
>
>* 公共API可用，並在所有受支援的客戶端類型上進行了充分測試。 對於任何公共功能，我們確保每個客戶端類型都具有相關方法的相應版本。
>* 公共API必須盡可能穩定，以支援向後相容性，並確保合作夥伴整合不會中斷。 但是，對於非公有API，我們保留在將來任何時刻更改其簽名的權利。 如果您遇到當前公共黃金時段身份驗證API調用的組合所無法支援的特定流，最好的方法是讓我們知道。 考慮到您的需要，我們可以修改公共API並提供一個穩定的解決方案。


</br>

## API參考 {#apis}

* [初始化](#initWithSoftwareStatement):softwareStatement — 實例化AccessEnabler對象。

* **[已棄用]** [初始化](#init)  — 實例化AccessEnabler對象。

* [setOptions:options:](#setOptions)  — 配置全局SDK選項，如配置檔案或visitorID。

* [setRequestor:](#setReqV3)[請求者ID](#setReqV3)。[setRequestor:requestorID:服務提供商：](#setReqV3)  — 確定程式設計師的身份。

* **[已棄用]** [setRequestor:signedRequestorId:](#setReq)。[setRequestor:signedRequestorId:服務提供商：](#setReq)  — 確定程式設計師的身份。

* **[已棄用]** [setRequestor:signedRequestorId:密鑰：公鑰](#setReq_tvos)。 [setRequestor:signedRequestorId:服務提供程式:secret:公鑰](#setReq_tvos) — 確定程式設計師的身份。

* [setRequestorComplete:](#setReqComplete)  — 通知您的應用程式配置階段已完成。

* [checkAuthentication（檢查驗證）](#checkAuthN)  — 檢查當前用戶的身份驗證狀態。

* [getAuthentication（獲取身份驗證）](#getAuthN)。 [getAuthentication（獲取身份驗證）:withData:](#getAuthN)  — 啟動完整身份驗證工作流。

* [getAuthentication：篩選器](#getAuthN_filter)。[getAuthentication（獲取身份驗證）:withData:](#getAuthN)[和篩選器](#getAuthN_filter)  — 啟動完整身份驗證工作流。

* [displayProviderDialog:](#dispProvDialog)  — 通知應用程式實例化用戶選擇MVPD的適當UI元素。

* [setSelectedProvider:](#setSelProv)  — 通知AccessEnabler用戶的MVPD選擇。

* [導航至URL:](#nav2url)  — 通知您的應用程式需要向用戶顯示MVPD登錄頁。

* [導航至URL:useSVC:](#nav2urlSVC)  — 通知您的應用程式，需要使用SFSafariViewController向用戶顯示MVPD登錄頁

* [handleExternalURL:url](#handleExternalURL)  — 完成驗證/註銷流。

* **[已棄用]** [getAuthenticationToken](#getAuthNToken)  — 從後端伺服器請求身份驗證令牌。

* [setAuthenticationStatus:errorCode:](#setAuthNStatus)  — 通知您的應用程式驗證流的狀態。

* [checkPreauthorizedResources:](#checkPreauth)  — 確定是否已授權用戶查看特定受保護的資源。

* [checkPreauthorizedResources:cache:](#checkPreauthCache)  — 確定是否已授權用戶查看特定受保護的資源。

* [預授權資源：](#preauthResources)  — 提供已授權用戶查看的資源清單。

* [checkAuthorization:](#checkAuthZ)。 [checkAuthorization（檢查授權）:withData:](#checkAuthZ)  — 檢查當前用戶的授權狀態。

* [getAuthorization:](#getAuthZ)。 [getAuthorization:withData:](#getAuthZ)  — 啟動授權流。

* [setToken:forResource:](#setToken)  — 通知您的應用程式授權流已成功完成。

* [tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed)  — 通知您的應用程式授權流失敗。

* [註銷](#logout)  — 啟動註銷流。

* [getSelectedProvider](#getSelProv)  — 確定當前選定的提供程式。

* [selectedProvider:](#selProv)  — 將有關當前選定MVPD的資訊提供給您的應用程式。

* [getMetadata:](#getMeta)  — 檢索AccessEnabler庫以元資料形式公開的資訊。

* [presentTvProviderDialog:](#presentTvDialog)  — 通知您的應用程式顯示「AppleSSO」對話框。

* [取消TvProviderDialog:](#dismissTvDialog)  — 通知您的應用程式隱藏「AppleSSO」對話框。

* [setMetadataStatus:encrypted:對鍵:andArguments:](#setMetaStatus)  — 提供由 [getMetadata:](#getMeta) 呼叫。

* [sendTrackingData:forEventType:](#sendTracking)  — 提供跟蹤資料資訊。

* [MVPD](#mvpd) - MVPD類。 [包含有關MVPD的資訊]

### init:software語句 {#initWithSoftwareStatement}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**描述：** 實例化AccessEnabler對象。 每個應用程式實例應有一個AccessEnabler實例。

| **API調用：iOSAccessEnabler建構子** |
| --- |
| `- (id) init:` <br> |
| `(NSString *)softwareStatement;` |


**可用性：** v3.0+

**參數：**

* **softwareStatement（軟體語句）:** 標識Adobe系統中應用程式的字串。 檢查如何獲取軟體語句。

[回到最上面……](#apis)



### 初始化 —  [已棄用]{#init}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**描述：** 實例化AccessEnabler對象。 每個應用程式實例應有一個AccessEnabler實例。

| API調用：iOSAccessEnabler建構子 |
| --- |
| ```- (id) init;``` |

**可用性：** v1.0+ **直到：** v3.0

**參數：** 無

[回到最上面……](#apis)

</br>

### setOptions：選項 {#setOptions}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**描述：** 配置全局SDK選項。 它接受NSDictionary作為論據。 字典中的值將隨SDK進行的每次網路調用一起傳遞到伺服器。

**注：** 這些值將獨立於當前流（驗證/授權）傳遞給伺服器。 如果要更改值，可以在任何時間點調用此方法。

| API調用：setOptions |
| --- |
| ```- (void) setOptions:(NSDictionary *)options;``` |

**可用性：** v2.3.0+

**參數：**

* *選項*:包含全局SDK選項的NSDictionary。 目前，以下選項可用：
   * **應用程式配置檔案**  — 它可用於根據此值進行伺服器配置。
   * **訪問者ID** -Marketing Cloud訪客ID。 此值稍後可用於高級分析報告。
   * **句柄SVC**  — 指示程式設計師是否將處理SFSafariViewControllers的布爾值。 請參閱 [iOSSDK 3.2+上的SFSafariViewController支援](/help/authentication/sfsafariviewcontroller-support-on-ios-sdk-32.md) 的子菜單。
      * 如果設定為 **假的，** SDK將自動向最終用戶提供SFSafariViewController。 SDK將進一步導航到MVPD登錄頁URL。
      * 如果設定為 **沒錯，** SDK將 **不** 自動向最終用戶提供SFSafariViewController。 SDK將進一步觸發 **導航(toUrl:{url},useSVC:YES)**。
* **設備\_資訊**  — 客戶端資訊，如所述 [傳遞客戶端資訊](/help/authentication/passing-client-information-device-connection-and-application.md)。

[回到最上面……](#apis)


### setRequestor:requestorID, setRequestor:requestorID:服務提供商： {#setReqV3}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**描述：** 確定程式設計師的身份。 當向黃金時段Adobe系統註冊時，為每個程式設計師分配唯一ID。 在處理SSO和遠程令牌時，當應用程式處於後台時，驗證狀態可以改變，當應用程式進入前台時，可以再次調用setRequestor以與系統狀態同步（如果啟用SSO，則提取遠程令牌；如果同時發生註銷，則刪除本地令牌）。

伺服器響應包含MVPD清單以及附加到程式設計師身份的某些配置資訊。 伺服器響應由AccessEnabler代碼在內部使用。 只有操作的狀態（即SUCCESS/FAIL）通過 `setRequestorComplete:` 回叫。

如果 `urls` 未使用參數，生成的網路呼叫目標為預設服務提供商URL:Adobe版本/生產環境。


如果為 `urls` 參數，生成的網路調用以中提供的所有URL為目標 `urls` 的下界。 所有配置請求都在單獨的線程中同時觸發。 編譯MVPD清單時，第一響應程式優先。 對於清單中的每個MVPD,AccessEnabler會記住關聯服務提供商的URL。 所有後續權利請求都指向在配置階段與目標MVPD配對的與服務提供商關聯的URL。

| API調用：請求者配置 |
| --- |
| ```- (void) setRequestor:(NSString *)requestorID``` |


**可用性：** v3.0+

| API調用：請求者配置 |
| --- |
| `- (void) setRequestor:(NSString *)requestorID serviceProviders:(NSArray *)urls;` |


**可用性：** v3.0+

**參數：**

* *請求者ID*:與程式設計師關聯的唯一ID。 在首次註冊黃金時段Adobe服務時，將通過驗證分配的唯一ID傳遞到您的站點。
* *URL*:可選參數；預設情況下，使用Adobe服務提供程式(http://sp.auth.adobe.com/)。 此陣列允許您為Adobe提供的身份驗證和授權服務指定端點（可能會將不同的實例用於調試目的）。 您可以使用它來指定多個Moginiqe身份驗證服務提供程式實例。 執行此操作時，MVPD清單由來自所有服務提供商的端點組成。 每個MVPD都與最快速的服務提供商相關聯；即，首先響應的提供程式，並且支援該MVPD。

>[!NOTE]
>
>如果調用時沒有 `serviceProviders` 參數，庫將從預設服務提供程式(即 `https://sp.auth.adobe.com` 用於生產配置檔案或 `https://sp.auth-staging.adobe.com` )。 如果 `serviceProviders` 參數，它必須是URL的陣列。從所有指定端點檢索配置資訊並合併。 如果不同的服務提供商響應中存在重複資訊，則衝突將得到解決，有利於最快響應的伺服器（即優先於具有最短響應時間的伺服器）。

**觸發的回調：** [`setRequestorComplete:`](#setReqComplete)

[回到最上面……](#apis)

</br>

### setRequestor:setSignedRequestorId:, setRequestor:setSignedRequestorId:服務提供商： - [已棄用] {#setReq}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**描述：** 確定程式設計師的身份。 當向黃金時段Adobe系統註冊時，為每個程式設計師分配唯一ID。 在處理SSO和遠程令牌時，當應用程式處於後台時，驗證狀態可能會更改，當應用程式進入前台時，可以再次調用setRequestor以與系統狀態同步（如果啟用了SSO，則提取遠程令牌；如果同時發生註銷，則刪除本地令牌）。

伺服器響應包含MVPD清單以及附加到程式設計師身份的某些配置資訊。 伺服器響應由AccessEnabler代碼在內部使用。 只有操作的狀態（即SUCCESS/FAIL）通過 `setRequestorComplete:` 回叫。

如果 `urls` 未使用參數，生成的網路呼叫目標為預設服務提供商URL:Adobe版本/生產環境。

如果為 `urls` 參數，生成的網路調用以中提供的所有URL為目標 `urls` 的下界。 所有配置請求都在單獨的線程中同時觸發。 編譯MVPD清單時，第一響應程式優先。 對於清單中的每個MVPD,AccessEnabler會記住關聯服務提供商的URL。 所有後續權利請求都指向在配置階段與目標MVPD配對的與服務提供商關聯的URL。

| API調用：請求者配置 |
| --- |
| </br>`- (void) setRequestor:(NSString *)requestorID`</br>`signedRequestorID:(NSString *)signedRequestorID;` </br></br> |

**可用性：** v1.0+ **直到：** v3.0

| API調用：請求者配置 |
| --- |
| `- (void) setRequestor:(NSString *)requestorID ` <br> `       signedRequestorID:(NSString *)signedRequestorID` <br> `         serviceProviders:(NSArray *)urls;` |

**可用性：** v1.0+ **直到：** v3.0

**參數：**

* *請求者ID*:與程式設計師關聯的唯一ID。 在您首次註冊黃金時段Adobe服務時，將通過驗證分配的唯一ID傳遞到您的站點。
* *簽名請求者ID*: **此參數在iOSAccessEnabler 1.2及更高版本中存在。** 用您的私鑰進行數字簽名的請求者ID的副本。 <!--For more details, see [Registering Native Clients](https://tve.helpdocsonline.com/registering-native-clients)-->。
* *URL*:可選參數；預設情況下，使用Adobe服務提供程式(http://sp.auth.adobe.com/)。 此陣列允許您為Adobe提供的身份驗證和授權服務指定端點（可能會將不同的實例用於調試目的）。 您可以使用它來指定多個Moginiqe身份驗證服務提供程式實例。 執行此操作時，MVPD清單由來自所有服務提供商的端點組成。 每個MVPD都與最快速的服務提供商相關聯；即，首先響應的提供程式，並且支援該MVPD。

**附註：** 如果調用時沒有 `serviceProviders` 參數，庫將從預設服務提供程式(即`https://sp.auth.adobe.com` 用於生產配置檔案或 `https://sp.auth-staging.adobe.com` )。 如果 `serviceProviders` 參數，它必須是URL的陣列。從所有指定端點檢索配置資訊並合併。 如果不同的服務提供商響應中存在重複資訊，則衝突被解決，有利於最快響應的伺服器（即優先於具有最短響應時間的伺服器）。

**觸發的回調：** [`setRequestorComplete:`](#setReqComplete)


[回到最上面……](#apis)

### setRequestor:setSignedRequestorId:secret:publicKey, setRequestor:setSignedRequestorId:服務提供程式:secret:公鑰 —  [已棄用] {#setReq_tvos}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**描述：** 確定程式設計師的身份。 當向黃金時段Adobe系統註冊時，為每個程式設計師分配唯一ID。 此設定應在應用程式的生命週期中僅執行一次。

伺服器響應包含MVPD清單以及附加到程式設計師身份的某些配置資訊。 伺服器響應由AccessEnabler代碼在內部使用。 只有操作的狀態（即SUCCESS/FAIL）通過 `setRequestorComplete:` 回叫。

如果 `urls` 未使用參數，生成的網路呼叫目標為預設服務提供商URL:Adobe版本/生產環境。

如果為 `urls` 參數，生成的網路調用以中提供的所有URL為目標 `urls` 的下界。 所有配置請求都在單獨的線程中同時觸發。 編譯MVPD清單時，第一響應程式優先。 對於清單中的每個MVPD,AccessEnabler會記住關聯服務提供商的URL。 所有後續權利請求都指向在配置階段與目標MVPD配對的與服務提供商關聯的URL。



<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API調用：請求者配置</th>
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
<th>API調用：請求者配置</th>
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

* *請求者ID*:與程式設計師關聯的唯一ID。 在您首次註冊黃金時段Adobe服務時，將通過驗證分配的唯一ID傳遞到您的站點。
* *簽名請求者ID*: **此參數在iOSAccessEnabler 1.2及更高版本中存在。** 用您的私鑰進行數字簽名的請求者ID的副本。 <!--For more details, see [Registering Native Clients](https://tve.helpdocsonline.com/registering-native-clients)-->。
* *URL*:可選參數；預設情況下，使用Adobe服務提供程式(http://sp.auth.adobe.com/)。 此陣列允許您為Adobe提供的身份驗證和授權服務指定端點（可能會將不同的實例用於調試目的）。 您可以使用它來指定多個Moginiqe身份驗證服務提供程式實例。 執行此操作時，MVPD清單由來自所有服務提供商的端點組成。 每個MVPD都與最快速的服務提供商相關聯；即，首先響應的提供程式，並且支援該MVPD。
* secret和publicKey:用於簽署第二個螢幕呼叫的密鑰和公鑰。 有關詳細資訊，請參閱 [無附屬檔案](#create_dev)。

如果調用時沒有 `serviceProviders` 參數，庫將從預設服務提供程式(如 `https://sp.auth.adobe.com` 生產配置檔案，或登台配置檔案的https://sp.auth-staging.adobe.com)。 如果 `serviceProviders` 參數，它必須是URL的陣列。從所有指定端點檢索配置資訊並合併。 如果不同的服務提供商響應中存在重複資訊，則衝突被解決，有利於最快響應的伺服器（即優先於具有最短響應時間的伺服器）。

**觸發的回調：** [`setRequestorComplete:`](#setReqComplete)

[回到最上面……](#apis)

</br>

### setRequestorComplete: {#setReqComplete}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回調，該回調通知您的應用程式配置階段已完成。 這是一個信號，表明應用可以開始發出權利請求。 在配置階段完成之前，應用程式不能發出任何權利請求。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回叫：請求者配置完成</th>
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

* *狀態*:可以選取以下值之一：
   * `ACCESS_ENABLER_STATUS_SUCCESS`  — 配置階段已成功完成
   * `ACCESS_ENABLER_STATUS_ERROR`  — 配置階段失敗

**觸發者：**
`setRequestor:setSignedRequestorId:, `[`setRequestor:setSignedRequestorId:serviceProviders:`](#setReq)

[回到最上面……](#apis)

</br>

### checkAuthentication（檢查驗證） {#checkAuthN}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**描述：** 檢查當前用戶的身份驗證狀態。
它通過在本地令牌儲存空間中搜索有效的身份驗證令牌來做到這一點。 調用此方法不執行網路調用。 應用程式使用它來查詢用戶的驗證狀態並相應地更新UI（即更新登錄/註銷UI）。 認證狀態通過 [`setAuthenticationStatus:errorCode:`](#setAuthNStatus) 回叫。\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API調用：檢查驗證狀態</th>
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

**觸發的回調：**
[`setAuthenticationStatus:errorCode:`](#setAuthNStatus)

[回到最上面……](#apis)

</br>

### getAuthentication、getAuthentication:withData: {#getAuthN}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**描述：** 啟動完整身份驗證工作流。 首先檢查身份驗證狀態。 如果尚未進行身份驗證，則啟動身份驗證流狀態機：

* 如果上次身份驗證嘗試成功，則跳過MVPD選擇階段，並 [`navigateToUrl:`](#nav2url) 觸發回調。 應用程式使用此回調實例化向用戶顯示MVPD登錄頁的WebView控制項。 **[注：自Access Enabler 1.5起，由於SDK中的限制，此功能不可用]。**
* 如果上次身份驗證嘗試失敗或用戶明確註銷， [`displayProviderDialog:`](#dispProvDialog) 觸發回調。 您的應用程式使用此回調來顯示MVPD選擇UI。 此外，還需要您的應用通過以下方式將用戶的MVPD選擇通知AccessEnabler庫，以恢復身份驗證流： [`setSelectedProvider:`](#setSelProv) 的雙曲餘切值。

當用戶的憑據在MVPD登錄頁上得到驗證時，您的應用程式需要監視在用戶在MVPD登錄頁上進行身份驗證時發生的多次重定向操作。 輸入正確的憑據後，WebView控制項將重定向到由 `ADOBEPASS_REDIRECT_URL` 常數。 此URL不打算由WebView載入。 應用程式必須截取此URL並將此事件解釋為登錄階段已完成的信號。 然後，它應將控制權移交給AccessEnabler以完成身份驗證流(通過調用 [handleExternalURL](#handleExternalURL) )。

最後，通過該認證狀態將認證狀態傳送到該應用 [setAuthenticationStatus:errorCode:](#setAuthNStatus) 回叫。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API調用：啟動驗證流</th>
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
<th>API調用：啟動驗證流</th>
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

* *福爾森*:一個標誌，它指定是否應啟動驗證流，而不管用戶是否已經過驗證。
* *資料*:由要發送到付費電視通行服務的鍵值對組成的字典。 Adobe可以使用此資料來啟用將來的功能，而無需更改SDK。

**觸發的回調：** ` setAuthenticationStatus:errorCode:, `[`displayProviderDialog:`](#dispProvDialog)`,`` sendTrackingData:forEventType:`


[回到最上面……](#apis)

</br>

### getAuthentication:filter,getAuthentication:withData:和篩選器 {#getAuthN_filter}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**描述：** 啟動完整身份驗證工作流。 首先檢查身份驗證狀態。 如果尚未進行身份驗證，則啟動身份驗證流狀態機：

* [presentTvProviderDialog()](#presentTvDialog) 如果當前請求者至少有一個支援SSO的MVPD，則調用。 如果沒有MVPD支援SSO，則經典身份驗證流將開始，過濾器參數將被忽略。
* 用戶完成AppleSSO流後 [dismisdTvProviderDialog()](#dismissTvDialog) 將被觸發，驗證過程將完成。

最後，通過該認證狀態將認證狀態傳送到該應用 [setAuthenticationStatus:errorCode:](#setAuthNStatus) 回叫。

**可用性：** v2.4+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API調用：啟動驗證流</th>
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
<th>API調用：啟動驗證流</th>
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

* *福爾森*:一個標誌，它指定是否應啟動驗證流，而不管用戶是否已經過驗證。
* *資料*:由要發送到付費電視通行服務的鍵值對組成的字典。 Adobe可以使用此資料來啟用將來的功能，而無需更改SDK。 
* 篩選器：包含兩個MVPD ID清單的字典，應出現在「AppleSSO」對話框中。 任何不支援SSO的MVPD都將被忽略，但將遵守該命令。 字典需要有兩個鍵：
   * TV\_PROVIDERS:包含應出現在選取器中的所有MVPD的清單
   * 特色\_TV\_PROVIDERS:一個清單，其中應標籤為選取器中特徵的所有MVPD。 此清單中的MVPD還必須在TV\_PROVIDERS清單中指定。

**可用性：** v2.0 - v2.3.1


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API調用：啟動驗證流</th>
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
<th>API調用：啟動驗證流</th>
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

* *福爾森*:一個標誌，它指定是否應啟動驗證流，而不管用戶是否已經過驗證。
* *資料*:由要發送到付費電視通行服務的鍵值對組成的字典。 Adobe可以使用此資料來啟用將來的功能，而無需更改SDK。 
* 篩選器：應出現在「AppleSSO」對話框中的MVPD ID清單。 任何不支援SSO的MVPD都將被忽略，但將遵守該命令。

**觸發的回調：** `setAuthenticationStatus:errorCode:, presentTvProviderDialog, dismissTvProviderDialog`


[回到最上面……](#apis)

</br>

#### displayProviderDialog: {#dispProvDialog}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回調，用於通知應用程式需要實例化相應的UI元素，以允許用戶選擇所需的MVPD。 回調提供MVPD對象清單，其中包含有助於正確構建選擇UI面板的附加資訊（如指向MVPD徽標的URL、友好顯示名稱等）

一旦用戶選擇了所需的MVPD，則需要上層應用程式通過調用來恢複驗證流 `setSelectedProvider:` 並傳遞與用戶選擇對應的MVPD ID。

**中止驗證流**  — 此時用戶能夠按「後退」按鈕，這相當於中止驗證流。 在該情形中，您的應用程式需要調用 [setSelectedProvider:](#setSelProv) 方法，將null作為參數傳遞，使AccessEnabler有機會重置其驗證狀態機。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回叫：顯示MVPD選擇UI</th>
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

* *mvpd*:包含與MVPD相關資訊的MVPD對象清單，應用程式可以使用這些資訊構建MVPD選擇UI元素。

**觸發者：** ` getAuthentication, `[getAuthentication（獲取身份驗證）:withData:](#getAuthN)。` getAuthorization:, `[getAuthorization:withData:](#getAuthZ)


[回到最上面……](#apis)

</br>

#### setSelectedProvider: {#setSelProv}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**描述：** 應用程式調用此方法以通知Access Enabler用戶的MVPD選擇。 應用程式可以使用此方法選擇或更改用於驗證的服務提供商。

如果所選的MVPD是TempPass MVPD，則它將自動向該MVPD進行身份驗證，而無需隨後調用getAuthentication()。

請注意，對於在getAuthentication()方法上提供額外參數的促銷臨時傳遞，這是不可能的。

過路時 *空* 作為參數，Access Enabler假定用戶已取消驗證流（即按「後退」按鈕），並通過重置驗證狀態機和調用驗證流 [setAuthenticationStatus:errorCode:](#setAuthNStatus) 回調 `AccessEnabler.PROVIDER_NOT_SELECTED_ERROR` 錯誤代碼。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API調用：設定當前選定的提供程式</th>
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

**觸發的回調：** ` setAuthenticationStatus:errorCode:,sendTrackingData:forEventType:,  `[`navigateToUrl:`](#nav2url)

[回到最上面……](#apis)

</br>

#### 導航至URL: {#nav2url}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**描述：** 由AccessEnabler觸發的回調，用於請求應用程式實例化UIWebView/WKWebView控制器並載入回調中提供的URL **`url`** 的下界。 回調通過 **`url`** 參數，它表示驗證終結點的URL或註銷終結點的URL。

作為UIWebView/WKWebView` `控制器經歷多次重定向，您的應用程式必須監視控制器的活動並檢測載入由定義的特定自定義URL的時間 `ADOBEPASS_REDIRECT_URL `常數(即 `adobepass://ios.app`)。 請注意，此特定自定義URL實際上無效，並且不是供控制器實際載入的。 您的應用程式只能將其解釋為驗證或註銷流程已完成並且關閉控制器是安全的信號。 當控制器載入此特定自定義URL時，您的應用程式必須關閉UIWebView/WKWebView並調用AccessEnabler `handleExternalURL:url `API方法。

**注：** 請注意，在驗證流中，用戶可以按「後退」按鈕，這相當於中止驗證流。 在這種情況下，您的應用程式需要調用 [setSelectedProvider:](#setSelProv) 傳遞 **`nil`** 作為參數，並使AccessEnabler有機會重置其驗證狀態機。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回叫：顯示MVPD登錄頁</th>
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

* *url*:指向MVPD登錄頁的URL

**觸發者：** [setSelectedProvider:](#setSelProv)

 

[回到最上面……](#apis)

</br>

#### 導航至URL:useSVC: {#nav2urlSVC}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**描述：** 由AccessEnabler觸發的回調，而不是 `navigateToUrl:` 回調，以防應用程式以前通過以下方式啟用手動Safari View Controller(SVC)處理 [setOptions(\[&quot;handleSVC&quot;:true&quot;\])](#setOptions) 調用，並且僅在MVPD需要Safari View Controller(SVC)時。 對於所有其它MVPD `navigateToUrl:` 將調用回調。 請參閱[iOSSDK 3.2+上的SFSafariViewController支援](/help/authentication/sfsafariviewcontroller-support-on-ios-sdk-32.md) 有關如何管理Safari View Controller(SVC)的詳細資訊。

與 `navigateToUrl:` 回調 `navigateToUrl:useSVC:` 由AccessEnabler觸發，請求應用程式實例化 `SFSafariViewController` 控制器和載入回調中提供的URL **`url`** 的下界。 回調通過 **`url`** 參數，它表示驗證終結點的URL或註銷終結點的URL，以及 **`useSVC`** 參數，該參數指定應用程式必須使用 `SFSafariViewController`。

作為 `SFSafariViewController` 控制器經歷多次重定向，您的應用程式必須監視控制器的活動並檢測載入由您定義的特定自定義URL的時間 `application's custom scheme` (例如** **`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)。 請注意，此特定自定義URL實際上無效，並且不是供控制器實際載入的。 您的應用程式只能將其解釋為驗證或註銷流程已完成並且關閉控制器是安全的信號。 當控制器載入此特定自定義URL時，您的應用程式必須關閉 `SFSafariViewController` 並調用AccessEnabler `handleExternalURL:url `API方法。

**注：** 請注意，在驗證流中，用戶可以按「後退」按鈕，這相當於中止驗證流。 在這種情況下，您的應用程式需要調用 [setSelectedProvider:](#setSelProv) 傳遞 **`nil`** 作為參數，並使AccessEnabler有機會重置其驗證狀態機。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回叫：在SFSafariViewController中顯示MVPD登錄頁</th>
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

* *url:* 指向MVPD登錄頁的URL
* *useSVC:* 是否應將url載入到SFSafariViewController中。

**觸發者：**[ setOptions:](#setOptions) 先 [setSelectedProvider:](#setSelProv) 

[回到最上面……](#apis)

</br>

#### handleExternalURL:url {#handleExternalURL}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**描述：** 應用程式將調用此方法以完成驗證或註銷流程。 應在應用程式檢測到 `UIWebView/WKWebView or SFSafariViewController` 控制器被重定向到特定自定義URL。 如果您的應用程式需要使用 `SFSafariViewController `控制器指定的自定義URL由 `application's custom scheme` (例如`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否則此特定自定義URL由 `ADOBEPASS_REDIRECT_URL `常數(即 `adobepass://ios.app`)。

在驗證流的情況下，AccessEnabler通過從後端伺服器檢索驗證令牌並將其本地儲存在令牌儲存中來完成該流。 AccessEnabler將通過調用 `setAuthenticationStatus()`<!--(http://tve.helpdocsonline.com/ios-technical-overview#setAuthNStatus)--> 狀態代碼為1的回調，表示成功。 如果執行這些步驟時出錯， `setAuthenticationStatus()`<!--(http://tve.helpdocsonline.com/ios-technical-overview#setAuthNStatus)--> 回調被觸發，狀態代碼為0，表示身份驗證失敗，並且有相應的錯誤代碼。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API調用：完成驗證或註銷流</th>
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

* *url*:截獲的URL ` UIWebView/WKWebView or SFSafariViewController ` 控制項作為字串。


**觸發的回調：** `setAuthenticationStatus:errorCode, sendTrackingData:forEventType:`

[回到最上面……](#apis)

</br>

#### getAuthenticationToken - [已棄用] {#getAuthNToken}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**描述：** 通過從後端伺服器請求驗證令牌來完成驗證流。 只有當承載MVPD登錄頁的WebView控制項重定向到由 `ADOBEPASS_REDIRECT_URL` 常數。\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API調用：檢索身份驗證令牌</th>
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

**觸發的回調：** `setAuthenticationStatus:errorCode,sendTrackingData:forEventType:`

[回到最上面……](#apis)

&lt;/br

#### setAuthenticationStatus:errorCode: {#setAuthNStatus}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回調，它通知應用程式驗證流的狀態。 有許多地方，此流可能會因用戶交互或其他不可預見的情形（如網路連接問題等）而失敗。 此回調通知應用程式驗證流的成功/失敗狀態，同時在需要時還提供有關失敗原因的附加資訊。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回叫：報告驗證流的狀態</th>
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

* *狀態*:可以選取以下值之一：
   * `ACCESS_ENABLER_STATUS_SUCCESS`  — 身份驗證流已成功完成
   * `ACCESS_ENABLER_STATUS_ERROR`  — 驗證流失敗
* *代碼*:失敗原因。 如果 *狀態* 是 `ACCESS_ENABLER_STATUS_SUCCESS`，則 *代碼* 是空字串(即由 `USER_AUTHENTICATED` 常數)。 在失敗時，此參數可以採用以下值之一：
   * `USER_NOT_AUTHENTICATED_ERROR`  — 用戶未經過身份驗證。 響應 [checkAuthentication:](#checkAuthN) 當本地令牌快取中沒有有效的驗證令牌時調用方法。
   * `PROVIDER_NOT_SELECTED_ERROR`  — 在上層應用程式通過後， AccessEnabler已重置身份驗證狀態機 *空* 至 [`setSelectedProvider:`](#setSelProv) 中止驗證流。  用戶可能已取消驗證流（即按「後退」按鈕）。
   * `GENERIC_AUTHENTICATION_ERROR`  — 由於網路不可用或用戶明確取消了驗證流等原因，驗證流失敗。

**觸發者：** ` checkAuthentication, getAuthentication, `[getAuthentication（獲取身份驗證）:withData:](#getAuthN)。` checkAuthorization:, `[checkAuthorization（檢查授權）:withData:](#checkAuthZ)

[回到最上面……](#apis)

</br>

### checkPreauthorizedResources: {#checkPreauth}


**檔案：** AccessEnabler/headers/AccessEnabler.h

**描述：** 應用程式使用此方法來確定用戶是否已獲得查看特定受保護資源的授權。 此方法的主要目的是檢索用於裝飾UI的資訊 **（例如，用鎖定和解鎖表徵圖指示訪問狀態）。**

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API調用：設定當前選定的提供程式</th>
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

* *資源：* 應檢查其授權的資源陣列。 清單中的每個元素都應是表示資源ID的字串。 資源ID受與呼叫中資源ID相同的限制，即，它應是程式設計師與MVPD或媒體RSS片段之間建立的商定值。

**觸發的回調：** [`preauthorizedResources:`](#preauthResources)

[回到最上面……](#apis)

</br>

### checkPreauthorizedResources:cache: {#checkPreauthCache}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**描述：** 應用程式使用此方法來確定用戶是否已獲得查看特定受保護資源的授權。 此方法的主要目的是檢索用於裝飾UI的資訊（例如，用鎖定和解鎖表徵圖指示訪問狀態）。 的 **快取** 參數控制是否使用內部快取來解析資源。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API調用：設定當前選定的提供程式</th>
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

* *資源：* 應檢查其授權的資源陣列。 清單中的每個元素都應是表示資源ID的字串。 資源ID受與 `getAuthorization:` 呼叫，即，它應是程式設計師與MVPD或媒體RSS片段之間所確定的商定值。
* *快取：* 布爾值，指定是否使用內部快取解析資源。 如果為false，將跳過快取，導致每次調用此API時都會調用伺服器。

**觸發的回調：** [`preauthorizedResources:`](#preauthResources)

[回到最上面……](#apis)

</br>

### 預授權資源： {#preauthResources}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**描述：** 觸發的回調 `checkPreauthorizedResources:`。 提供已授權用戶查看的資源清單。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API調用：設定當前選定的提供程式</th>
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

* `resources`:已授權用戶查看的資源陣列。

**觸發者：** [`checkPreauthorizedResources:`](#checkPreauth)

 

[回到最上面……](#apis)

</br>

### checkAuthorization:,checkAuthorization:withData: {#checkAuthZ}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**描述：** 此方法由應用程式用於檢查授權狀態。 首先檢查身份驗證狀態。 如果未通過身份驗證， [tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed) 回調被觸發，該方法退出。 如果用戶被認證，則它還觸發授權流。 請參閱 [`getAuthorization:`](#getAuthZ) 的雙曲餘切值。


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API調用：檢查授權狀態</th>
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
<th>API調用：檢查授權狀態</th>
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

* *資源*:用戶請求授權的資源的ID。
* *資料*:由要發送到付費電視通行服務的鍵值對組成的字典。 Adobe可以使用此資料來啟用將來的功能，而無需更改SDK。 

**觸發的回調：**
[tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed)`,setToken:forResource:, sendTrackingData:forEventType:, setAuthenticationStatus:errorCode:`

[回到最上面……](#apis)

</br>

### getAuthorization:,getAuthorization:withData: {#getAuthZ}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**描述：** 應用程式使用此方法啟動授權流。 如果用戶尚未經過身份驗證，它還會啟動身份驗證流。 如果用戶獲得身份驗證，AccessEnabler將繼續發出授權令牌的請求（如果本地令牌快取中沒有有效的授權令牌）和短時間媒體令牌的請求。 一旦獲得了短媒體令牌，則認為授權流完成。 的 [setToken:forResource:](#setToken) 觸發回調，並將短媒體令牌作為參數傳遞給應用程式。 如因任何原因授權失敗， [tokenRequestFailed:forEventType:](#tokenReqFailed) 觸發回調，並提供錯誤代碼/詳細資訊。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API調用：啟動授權流</th>
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
<th>API調用：啟動授權流</th>
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

* *資源*:用戶請求授權的資源的ID。
* *資料*:由要發送到付費電視通行服務的鍵值對組成的字典。 Adobe可以使用此資料來啟用將來的功能，而無需更改SDK。 

**觸發的回調：** `tokenRequestFailed:errorCode:errorDescription:, setToken:forResource:,sendTrackingData:forEventType:`

**觸發的其他回調：**\
此方法還可以觸發以下回調（如果還啟動了驗證流）: `setAuthenticationStatus:errorCode:`。 `displayProviderDialog:`\
 
**注：請使用checkAuthorization:/ check授權:withData: 而不是getAuthorization: / getAuthorization:withData: 盡可能。 getAuthorization: / getAuthorization:withData: 方法將啟動一個完全驗證流（如果用戶未經驗證），這可能導致程式設計師方面的複雜實現。**

[回到最上面……](#apis)

</br>

### setToken:forResource: {#setToken}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回調，該回調通知您的應用程式授權流已成功完成。 短壽命媒體令牌也作為參數傳遞。\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回叫：授權流已成功完成</th>
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

* *標籤*:短命的媒體標誌
* *資源*:獲得授權的資源

**觸發者：** [checkAuthorization:](#checkAuthZ)` , `[checkAuthorization（檢查授權）:withData:](#checkAuthZ)。` `[getAuthorization:](#getAuthZ)。 [getAuthorization:withData:](#getAuthZ)

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
<th>回叫：授權流失敗</th>
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
* *代碼*:與故障方案關聯的錯誤代碼。 可能的值：
   * `USER_NOT_AUTHORIZED_ERROR`  — 用戶無法授權給定資源
* *描述*:有關失敗方案的其他詳細資訊。 如果此描述性字串因任何原因不可用，Oracle Mighine驗證將發送一個空字串 **(&quot;&quot;)**。 \
   MVPD可以使用此字串傳遞自定義錯誤消息或與銷售相關的消息。 例如，如果拒絕訂閱者對資源的授權，則MVPD可以發送消息，如：「您目前在軟體包中沒有訪問此渠道的權限。 如果要升級包，請按一下 **這裡**&quot; 通過此回調，該消息通過黃金時段身份驗證傳遞給程式設計師，程式設計師可以選擇顯示或忽略它。 黃金時段身份驗證還可以使用此參數來提供可能導致錯誤的條件通知。 例如，「與提供商的授權服務通信時發生網路錯誤」。

**觸發者：** ` checkAuthorization:, `[checkAuthorization（檢查授權）:withData:](#checkAuthZ)。 `getAuthorization:, `[getAuthorization:withData:](#getAuthZ)

[回到最上面……](#apis)

</br>

### 註銷 {#logout}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**描述：** 應用程式調用此方法以啟動註銷流。 註銷是一系列HTTP重定向操作的結果，因為用戶需要從Mogine Authentication伺服器和MVPD伺服器註銷。 由於AccessEnabler庫發出的簡單HTTP請求無法完成此流，因此 `UIWebView/WKWebView or SFSafariViewController` 需要實例化控制器，以便能夠執行HTTP重定向操作。

註銷流與驗證流不同，因為用戶不需要與 `UIWebView/WKWebView or SFSafariViewController`  控制器。 因此，Adobe建議您使控制項不可見(即 隱藏)。

採用與認證流相似的模式。 iOSAccessEnabler觸發 `navigateToUrl:` 回調或 `navigateToUrl:useSVC:` 建立 `UIWebView/WKWebView or SFSafariViewController` 控制器和載入回調中提供的URL `url` 的下界。 這是後端伺服器上註銷終結點的URL。 對於tvOS AccessEnabler, `navigateToUrl:` 回調或 `navigateToUrl:useSVC:` 調用回調。

在多次重定向時，您的應用程式必須監視 `UIWebView/WKWebView or SFSafariViewController `控制器並檢測載入特定自定義URL的時間。 請注意，此特定自定義URL實際上無效，並且不是供控制器實際載入的。 您的應用程式只能將其解釋為註銷流程已完成並且關閉控制器是安全的信號。 當控制器載入此特定自定義URL時，您的應用程式必須關閉控制器並調用AccessEnabler `handleExternalURL:url `API方法。 如果您的應用程式需要使用 `SFSafariViewController `控制器指定的自定義URL由 `application's custom scheme` (例如`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否則此特定自定義URL由 `ADOBEPASS_REDIRECT_URL `常數(即 `adobepass://ios.app`)。

最後， AccessEnabler將調用 [`setAuthenticationStatus()`](#setAuthNStatus) 回調，狀態代碼為0，表示註銷流成功。

**注：** 如果用戶使用AppleSSO登錄，則將觸發VSA203狀態。 如果出現這種情況，應指示用戶也從系統設定註銷。 如果不執行此操作，將在應用程式重新啟動時導致重新驗證。


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API調用：啟動註銷流</th>
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

**觸發的回調：** `navigateToUrl:, `[`setAuthenticationStatus:errorCode:`](#setAuthNStatus)

 

[回到最上面……](#apis)

</br>

### getSelectedProvider {#getSelProv}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**描述：** 使用此方法可確定當前選定的提供程式。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API調用：確定當前選定的MVPD</th>
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

**觸發的回調：** [`selectedProvider:`](#selProv)

[回到最上面……](#apis)

</br>

### 選定提供程式 {#selProv}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回調，該啟用程式將有關當前選定MVPD的資訊傳送到應用程式。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回叫：有關當前選定MVPD的資訊</th>
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

* *mvpd*:包含有關當前選定MVPD的資訊的對象

**觸發者：** [`getSelectedProvider`](#getSelProv)

[回到最上面……](#apis)

</br>

### getMetadata: {#getMeta}

**檔案：** AccessEnabler/headers/AccessEnabler.h

**描述：** 使用此方法可檢索AccessEnabler庫作為元資料公開的資訊。 該應用程式可以通過提供基於字典的資料來訪問該資料 *鍵* 輸入參數。

程式設計師可使用兩種類型的元資料：

* 靜態元資料（驗證令牌TTL、授權令牌TTL和設備ID） 
* 用戶元資料(用戶特定資訊，如用戶ID、郵遞區號；可以在驗證和授權流程期間從MVPD傳遞到用戶設備)

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API調用：查詢AccessEnabler以獲取元資料</th>
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

* *鍵字典*:字典資料結構，格式如下：
   * 如果鍵為 `METADATA_OPCODE_KEY` 值 `METADATA_AUTHENTICATION`，然後進行查詢以獲得認證令牌的過期時間。
   * 如果鍵為 `METADATA_OPCODE_KEY` 值 `METADATA_AUTHORIZATION` **和**\
      鍵 `METADATA_RESOURCE_ID_KEY` 並且值是特定資源ID，然後進行查詢以獲得與指定資源相關聯的授權令牌的到期時間。
   * 如果鍵為 `METADATA_OPCODE_KEY` 值 `METADATA_DEVICE_ID`，然後進行查詢以獲取當前設備id。 請注意，此功能預設為禁用，程式設計師應與Adobe聯繫，以獲取有關啟用和費用的資訊。
   * 如果鍵為 `METADATA_OPCODE_KEY` 值 `METADATA_USER_META` **和** 鍵 `METADATA_USER_META_KEY` 值是元資料的名稱，然後對用戶元資料進行查詢。 可用用戶元資料類型清單：
      * `zip`  — 郵遞區號清單
      * `householdID`  — 家庭標識。 如果MVPD不支援子帳戶，則這與 `userID`。
      * `maxRating`  — 用戶的最高家長評分集
      * `userID`  — 用戶標識符。 如果MVPD支援子帳戶，並且用戶不是主帳戶， `userID` 將不同於 `householdID.`
      * `channelID`  — 用戶有權查看的頻道清單。
   >[!NOTE]
   >
   >程式設計師可用的實際用戶元資料取決於MVPD提供的內容。 此清單將隨著新的元資料被提供並添加到黃金時段身份驗證系統中而擴展。

**觸發的回調：** [`setMetadataStatus:encrypted:forKey:andArguments:`](#setMetaStatus)

**更多資訊：** [用戶元資料](/help/authentication/user-metadata.md)

[回到最上面……](#apis)

</br>

### presentTVProvider對話框 {#presentTvDialog}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 調用後由AccessEnabler觸發的回調[getAuthentication()](#getAuthN) 如果當前請求者支援至少一個MVPD並支援SSO。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回叫：SSO流的結果</th>
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

* viewController:代表AppleSSO對話。 此viewController需要顯示在螢幕上。

**觸發者：** [`getAuthentication`](#getAuthN)

**更多資訊：** [iOS/電視OS單一登錄](#presentTvDialog)

[回到最上面……](#apis)

</br>

### 消除TVProviderDialog {#dismissTvDialog}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 用戶關閉「AppleSSO」對話框後由AccessEnabler觸發的回調。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回叫：SSO流的結果</th>
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

* viewController:代表AppleSSO對話。 需要從螢幕中刪除此viewController。

**觸發者：** 用戶操作

**更多資訊：** [iOS/電視OS單一登錄](#presentTvDialog)

[回到最上面……](#apis)

</br>

### setMetadataStatus:encrypted:對鍵:andArguments: {#setMetaStatus}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler觸發的回調，該啟用程式通過 [`getMetadata:`](#getMeta) 呼叫。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回叫：元資料檢索請求結果</th>
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

* *元資料*:請求的元資料。 此值是 `NSString` 靜態元資料（驗證TTL、授權TTL、設備ID）。  在請求用戶特定元資料時，它是一個複雜的對象。 此複雜對象通常是JSON負載的Objective-C表示(例如，「{」街道：「主大道」、「建築」： [&quot;150&quot;、&quot;320&quot;]}&#39;在Objective-C中被翻譯為NSDictionary(&quot;street&quot; -> &quot;Main Avenue&quot;, &quot;boulds&quot; -> NSArray(&quot;150&quot;, &quot;320&quot;))。   元資料JSON對象示例：

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

* *加密*：指定是否加密檢索到的元資料的布爾值。 此參數僅對用戶元資料請求有重要意義，對始終未加密接收的靜態元資料（如驗證TTL）沒有意義。 如果此參數設定為true，則程式設計師需要使用白名單私鑰（與在中籤名請求者ID時使用的相同私鑰）執行RSA解密來獲取未加密的用戶元資料值 [`setRequestor:setSignedRequestorId:`](#setReq) 和 `setRequestor:setSignedRequestorId:serviceProviders: `呼叫)。

* *鍵*:用於構建元資料檢索請求的鍵。

* *參數*:同一本字典 [`getMetadata:`](#getMeta) 呼叫。 這允許應用程式將請求與響應匹配。

**觸發者：** [`getMetadata:`](#getMeta)

**更多資訊：** [用戶元資料](/help/authentication/user-metadata.md)


[回到最上面……](#apis)

</br>

### MVPD {#mvpd}

**檔案：** AccessEnabler/headers/model/MVPD.h

**說明** 描述MVPD對象。 可用於獲取有關MVPD屬性的資訊。

**可用性：** v1.0+ [boardingStatus屬性可從v2.2獲得] 

**屬性**:

* (NSString)ID - MVPD ID。
* (NSString)displayName - MVPD名稱。 [此選項應用於在機械臂中顯示]
* (NSString)logoURL - MVPD徽標地址。
* (BOOL)enablePlatformServices — 如果為true，則MVPD支援SSO服務，如 [Apple](#presentTvDialog)。
* (NSString)boardingStatus — 可以有3個值：
   * nil - MVPD不支援AppleSSO。
   * PICKER - MVPD可以顯示在Apple選取器中，但驗證流由Adobe完成。
   * 支援 — Apple完全支援MVPD，並將使用Apple的SSO令牌。

[回到最上面……](#apis)

</br>

## 跟蹤事件 {#tracking}

AccessEnabler會觸發與權利流不一定相關的附加回調。 執行 [`sendTrackingData()`](#sendTracking) 回調函式是可選的，但它使應用程式能夠跟蹤特定事件並編譯統計資訊，如成功/失敗的身份驗證/授權嘗試次數。 

### sendTrackingData:forEventType: {#sendTracking}

**檔案：** AccessEnabler/headers/EntitlementDelegate.h

**說明** 由AccessEnabler向應用程式發出的回調信號觸發了各種事件的發生，如驗證/授權流的完成/失敗。 使用Mighide身份驗證1.6 ，將報告設備類型、AccessEnabler客戶端類型和作業系統 [`sendTrackingData()`](#sendTracking)。 的 [`sendTrackingData()`](#sendTracking) 回調仍然向後相容。

**回叫：跟蹤事件**

```
(void) sendTrackingData:(NSArray *)data 
             forEventType:(int)event;
```

**可用性：** v1.0+

**注：** 設備類型和作業系統是通過使用公共Java庫(<http://java.net/projects/user-agent-utils>)和用戶代理字串。 請注意，提供此資訊只是一種將操作度量細分為設備類別的粗略方法，但Adobe不能對不正確的結果負責。 請相應地使用新功能。

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

* *事件*:正在跟蹤的事件的代碼。 有三種可能的跟蹤事件類型：
   * **授權檢測：** 授權令牌請求返回(事件為 `TRACKING_AUTHORIZATION`)
   * **驗證檢測：** 驗證檢查時(事件為 `TRACKING_AUTHENTICATION`)
   * **mvpdSelection:** 當用戶在MVPD選擇表單中選擇MVPD時(事件為 `TRACKING_GET_SELECTED_PROVIDER`)
* *資料*:與報告的事件關聯的其他資料。 此資料以值清單的形式顯示。

**觸發者：** `checkAuthentication, getAuthentication, `[getAuthentication（獲取身份驗證）:withData:](#getAuthN)。 `checkAuthorization:, `[checkAuthorization（檢查授權）:withData:](#checkAuthZ)。 `getAuthorization:, `[getAuthorization:withData:](#getAuthZ)。 `setSelectedProvider:`

解釋中的值的說明 *資料* 陣列：

* 用於trackingEventType `TRACKING_AUTHENTICATION:`
   * **0**  — 令牌請求是否成功(true/false)，如果成功：
   * **1** - MVPD ID字串
   * **2** - GUID（md5散列）
   * **3**  — 快取中已有的標籤(true/false)
   * **4**  — 設備類型
   * **5** - AccessEnabler客戶端類型
   * **6**  — 作業系統類型

* 用於trackingEventType `TRACKING_AUTHORIZATION:`
   * **0**  — 令牌請求是否成功(true/false)，如果成功：
   * **1** - MVPD ID
   * **2** - GUID（md5散列）
   * **3**  — 快取中已有的標籤(true/false)
   * **4**  — 錯誤
   * **5**  — 詳細資訊
   * **6**  — 設備類型
   * **7** - AccessEnabler客戶端類型
   * **8**  — 作業系統類型
* 用於trackingEventType `TRACKING_GET_SELECTED_PROVIDER:`
   * **0**  — 當前選定MVPD的ID
   * **1**  — 設備類型
   * **2** - AccessEnabler客戶端類型
   * **3**  — 作業系統類型

</br>

## 相關資訊 {#related}

* [iOS整合烹飪書](/help/authentication/iostvos-sdk-cookbook.md)
* [iOS技術概述](/help/authentication/iostvos-sdk-overview.md)
* [權利流](/help/authentication/entitlement-flow.md)
   <!--* [Tracking Data in Primetime authentication](https://tve.helpdocsonline.com/tracking-data-in-adobe-pass)-->
