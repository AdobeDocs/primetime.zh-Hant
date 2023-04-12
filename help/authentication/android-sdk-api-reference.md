---
title: Android SDK API參考
description: Android SDK API參考
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '4517'
ht-degree: 0%

---



# Android SDK API參考 {#android-sdk-api-reference}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 簡介 {#intro}

本檔案詳細說明Android SDK公開的Adobe Primetime驗證方法和回呼，Adobe Primetime驗證1.7版及更新版本支援此方法和回呼。 此處描述的方法和回調函式在AccessEnabler.h和EntitlementDelegate.h標頭檔案中定義。

請參閱 [https://tve.zendesk.com/hc/en-us/articles/204963219-Android-Native-AccessEnabler-Library](https://tve.zendesk.com/hc/en-us/articles/204963219-Android-Native-AccessEnabler-Library) 最新Android AccessEnabler SDK的資訊。 


**注意：** Adobe Primetime驗證團隊鼓勵您只使用Adobe Primetime驗證 *公共* API:

- 公用API可供使用 *經過充分測試* 所有支援的用戶端類型。 對於任何公用功能，我們會確定每個用戶端類型都具有相關聯方法的對應版本。</span>
- 公用API必須盡可能穩定，以支援回溯相容性，並確保合作夥伴整合不會中斷。 不過， *non* — 公用API，我們保留在未來任何時間點更改其簽名的權利。 如果您遇到無法透過目前公用Adobe Primetime驗證API呼叫組合來支援的特定流程，最佳方法就是告訴我們。 根據您的需求，我們可以修改公用API，並提供穩定的解決方案，以推動未來的發展。

## Android API {#api}

- [getInstance](#getInstance)
- [setOptions](#setOptions)
- [setRequestor](#setRequestor)
- [setRequestorComplete](#setRequestorComplete)
- [checkAuthentication](#checkAuthN)
- [getAuthentication](#getAuthN)
- [displayProviderDialog](#displayProviderDialog)
- [setSelectedProvider](#setSelectedProvider)
- [navigateToUrl](#navigagteToUrl)
- [getAuthenticationToken](#getAuthNToken)
- [setAuthenticationStatus](#setAuthNStatus)
- 預先授權
- [checkAuthorization](#checkAuthZ)
- [getAuthorization](#getAuthZ)
- [setToken](#setToken)
- [tokenRequestFailed](#tokenRequestFailed)
- [註銷](#logout)
- [getSelectedProvider](#getSelectedProvider)
- [selectedProvider](#selectedProvider)
- [getMetadata](#getMetadata)
- [setMetadataStatus](#setMetadaStatus)
- [getVersion](#getVersion)

### Factory.getInstance {#getInstance}

**說明：** 實例化Access Enabler對象。 每個應用程式實例應有一個Access Enabler實例。

| API呼叫：建構函式 |
| --- |
| **公用靜態** AccessEnabler **getInstance**(Context appContext, String softwareStatement, String redirectUrl)<br>        **stres** AccessEnablerException <br><br>**公用靜態** AccessEnabler getInstance（ContextAppContext，字串env_url，字串softwareStatement，字串redirectUrl）<br>**stres** AccessEnablerException |

**可用性：** v3.1.2+

**參數：**

- *appContext*:Android應用程式內容。
- env\_url:若要使用Adobe中繼環境進行測試，可將env\_url設為「sp.auth-staging.adobe.com」

**已棄用：**

```
    public static AccessEnabler getInstance(Context appContext)
        throws AccessEnablerException
```



### setRequestor {#setRequestor}

**說明：** 建立程式設計師的身份。 在向Adobe Primetime驗證系統的Adobe註冊時，每個程式設計師被分配一個唯一ID。 處理SSO和遠端代號時，當應用程式在背景時，驗證狀態可能會改變，當應用程式進入前景時，可再次呼叫setRequestor以與系統狀態同步（如果啟用SSO，則擷取遠端代號，若同時發生登出，則刪除本機代號）。

伺服器響應包含MVPD的清單以及附加到程式設計師標識的一些配置資訊。 伺服器響應由Access Enabler代碼在內部使用。 只會透過setRequestorComplete()回呼向您的應用程式顯示操作狀態（即SUCCESS/FAIL）。

若 *url* 參數，則產生的網路呼叫會鎖定預設服務提供者URL:Adobe發行/生產環境。

如果為 *url* 參數，產生的網路呼叫會鎖定 *url* 參數。 所有配置請求都在單獨的線程中同時觸發。 編譯MVPD清單時，第一回應者優先。 對於清單中的每個MVPD,Access Enabler會記住相關服務提供商的URL。 所有後續的權限請求都會導向至在設定階段與目標MVPD成對之服務提供者相關聯的URL。

| API呼叫：請求者設定 |
| --- |
| ```public void setRequestor(String requestorId)``` |

**可用性：** v3.0+

| API呼叫：請求者設定 |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |
**可用性：** v3.0+


**參數：**

- *requestorID*:與程式設計師關聯的唯一ID。 在您首次向Adobe Primetime驗證服務註冊時，將Adobe指派的唯一ID傳遞至您的網站。

- *signedRequestorID*:以您的私密金鑰進行數位簽署的要求者ID副本。 <!--For more details. see [Registering Native Clients](http://tve.helpdocsonline.com/registering-native-clients)-->.

- *url*:選用參數；依預設，會使用Adobe服務提供者(http://sp.auth.adobe.com/)。 此陣列可讓您為Adobe提供的驗證和授權服務指定端點（可能會使用不同的執行個體進行除錯）。 您可以使用此ID來指定多個Adobe Primetime驗證服務提供者例項。 執行此操作時，MVPD清單由來自所有服務提供者的端點組成。 每個MVPD都與最快的服務提供商相關聯；即第一個回應且支援該MVPD的提供者。

**已觸發回呼：** `setRequestorComplete()`

已棄用：

    public void setRequestor(String requestorId, String signedRequestorId)
    
    public void setRequestor(String requestorId, String signedRequestorId, ArrayList&lt;string> url)

[返回Android API...](#api)

### setRequestorComplete {#setRequestorComplete}

**說明：** 由Access Enabler觸發的回調，該回調通知您的應用程式配置階段已完成。 這是一個訊號，表示應用程式可以開始發出權限請求。 在配置階段完成之前，應用程式不能發出任何權限請求。

| 回撥：請求者配置完成 |
| --- |
| java public void setRequestorComplete(int status) |

**可用性：** v1.0+

**參數：**

- *狀態*:可採用下列其中一個值：
   - SDK \>= 3.4.0
      - `AccessEnablerConstants.ACCESS_ENABLER_STATUS_SUCCESS`  — 已成功完成配置階段
      - `AccessEnablerConstants.ACCESS_ENABLER_STATUS_ERROR`  — 配置階段失敗
   - SDK \&lt; 3.4
      - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS`  — 已成功完成配置階段
      - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR`  — 配置階段失敗

**觸發者：** `setRequestor()`

[返回Android API...](#api)

### setOptions {#setOptions}

**說明：** 設定全域SDK選項。 接受 **地圖\&lt;string string=&quot;&quot;>** 作為引數。 地圖中的值會連同SDK進行的每個網路呼叫一併傳遞至伺服器。

這些值將獨立於當前流（驗證/授權）傳遞到伺服器。 如果您想要變更值，可以隨時呼叫此方法。

| API呼叫：setOptions |
| --- |
| public void setOptions(HashMap&lt;string string=&quot;&quot;> 選項) |

**可用性：** v1.9.2+

**參數：**

- *選項*:地圖&lt;string string=&quot;&quot;> 包含全域SDK選項。 目前可使用下列選項：
   - **applicationProfile**  — 可根據此值進行伺服器配置。
   - **ap_vi** -Marketing CloudvisitorID。 此值稍後可用於進階分析報表。
   - **ap_ai**  — 廣告ID
   - **device_info**  — 客戶端資訊，如下所述： [傳遞客戶資訊設備連接和應用](/help/authentication/passing-client-information-device-connection-and-application.md).

[回到最上面……](#apis)


### checkAuthentication {#checkAuthN}

**說明：** 檢查驗證狀態。 它會透過搜尋本機Token儲存空間中的有效驗證Token來執行此作業。 呼叫此方法不會執行網路呼叫。 應用程式使用它來查詢使用者的驗證狀態並據以更新UI（即更新登入/登出UI）。 驗證狀態通過 [*setAuthenticationStatus()*](#setAuthNStatus) 回呼。

如果MVPD支援「每個要求者進行驗證」功能，則可在裝置上儲存多個驗證Token。  如需此功能的詳細資訊，請參閱 [快取准則](#$caching) 一節中。

| API呼叫：檢查驗證狀態 |
| --- |
| public void checkAuthentication() |

**可用性：** v1.0+

**參數：** 無

**已觸發回呼：** `setAuthenticationStatus()`

[返回Android API...](#api)


### getAuthentication {#getAuthN}

**說明：** 啟動完整驗證工作流程。 首先檢查驗證狀態。 如果尚未驗證，則啟動驗證流狀態機：

- 如果上次驗證嘗試成功，則會略過MVPD選取階段，而 [*navigateToUrl()*](#navigagteToUrl) 已觸發回呼。 應用程式會使用此回呼來實例化向使用者顯示MVPD登入頁面的WebView控制項。
- 如果上次驗證嘗試失敗或用戶明確登出，則 [*displayProviderDialog()*](#displayProviderDialog) 已觸發回呼。 您的應用程式會使用此回呼來顯示MVPD選取UI。 此外，您的應用程式必須透過 [setSelectedProvider()](#setSelectedProvider) 方法。

當使用者的認證在MVPD登入頁面上驗證時，您的應用程式必須監控當使用者在MVPD的登入頁面驗證時發生的多個重新導向操作。 輸入正確的憑證時，WebView控制項會重新導向至 *AccessEnabler.ADOBEPASS\_REDIRECT\_URL* 常數。 此URL不打算由WebView載入。 應用程式必須截取此URL，並將此事件解譯為登入階段完成的訊號。 然後，它應將控制權移交給Access Enabler以完成驗證流程(通過調用 *getAuthenticationToken()* 方法)。

如果MVPD支援「每個請求者的驗證」功能，則可在一個裝置上儲存多個驗證Token（每個程式設計師一個）。  如需此功能的詳細資訊，請參閱 [快取准則](#$caching) 一節中。

最後，驗證狀態通過 *setAuthenticationStatus()* 回呼。



| API呼叫：啟動驗證流程 |
| --- |
| public void getAuthentication() |

**可用性：** v1.0+

| API呼叫：啟動驗證流程 |
| --- |
| public void getAuthentication(boolean forceAuthN, Map&lt;string object=&quot;&quot;> genericData) |

**可用性：** v1.8+

**參數：**

- *forceAuthn*:此標幟指定是否應啟動驗證流程，而不論使用者是否已通過驗證。
- *資料*:由要傳送至付費電視傳遞服務的鍵值值組所組成的地圖。 Adobe可以使用此資料來啟用未來功能，而不需變更SDK。

**已觸發回呼：** `setAuthenticationStatus(), displayProviderDialog(), navigateToUrl(), sendTrackingData()`


[返回Android API...](#api)

### displayProviderDialog {#displayProviderDialog}

**說明** 由Access Enabler觸發的回呼，通知應用程式需要具現化適當的UI元素，以允許使用者選取所需的MVPD。 回呼會提供MVPD物件清單，其中包含可協助正確建立選取UI面板的其他資訊（例如指向MVPD標誌的URL、好記的顯示名稱等）

一旦使用者選取了所需的MVPD，上層應用程式就需要透過呼叫來繼續驗證流程 *setSelectedProvider()* 並傳遞與使用者選取相對應之MVPD的ID。\
 
>[!NOTE]
>
> 中止驗證流程
> </br></br>
> 請注意，這是使用者能夠按下「返回」按鈕的點，這等同於中止驗證流程。 在這種情況下，您的應用程式必須呼叫 `setSelectedProvider()` 方法，傳遞 *null* 作為參數，使Access Enabler有機會重置其身份驗證狀態機。

| 回撥：顯示MVPD選擇UI |
| --- |
| `public void displayProviderDialog(ArrayList<Mvpd> mvpds)` |

**可用性：** v1.0+

**參數**:

- *mvpds*:MVPD物件清單，其中包含應用程式可用於建立MVPD選取UI元素的MVPD相關資訊。

**觸發者：** `getAuthentication(), getAuthorization()`

[返回Android API...](#api)


### setSelectedProvider {#setSelectedProvider}

**說明：** 應用程式會呼叫此方法，以通知Access Enabler使用者的MVPD選擇。 應用程式可以使用此方法來選擇或更改用於身份驗證的服務提供商。

如果所選MVPD是TempPass MVPD，則它將自動使用該MVPD進行驗證，而無需在之後調用getAuthentication()。

請注意，在getAuthentication()方法上提供額外參數的促銷臨時通行證則無法這麼做。

傳遞時 *null* 作為參數，Access Enabler假定用戶已取消身份驗證流（即按下「返回」按鈕），並通過重置身份驗證狀態機和調用 *setAuthenticationStatus()* 以回呼 `AccessEnablerConstants.PROVIDER_NOT_SELECTED_ERROR` 錯誤代碼。

| API呼叫：設定當前選擇的提供程式 |
| --- |
| public void setSelectedProvider(String mvpdId) |

**可用性：** v1.0+

**參數：** 無

**已觸發回呼：** `setAuthenticationStatus(), sendTrackingData(), navigateToUrl()`

[返回Android API...](#api)


### navigateToUrl {#navigagteToUrl}

**已棄用：** 從Android SDK 3.0開始，只有在裝置上不存在Chrome自訂分頁時，才會使用navigateToUrl

**說明：** 由Access Enabler觸發的回呼，該回呼通知應用程式需要向用戶顯示MVPD登錄頁以輸入其憑據。 Access Enabler作為參數傳遞MVPD登錄頁的URL。 您的應用程式必須具現化WebView控制項，並將其導向至此URL。 此外，應用程式需要監視由WebView控制項載入的URL，並截取針對由 `AccessEnabler.ADOBEPASS_REDIRECT_URL (deprecated)` 常數。 在此事件上，應用程式需要關閉或隱藏WebView控制項，並通過調用 *getAuthenticationToken()* 方法。 Access Enabler通過從後端伺服器中檢索身份驗證令牌並將其本地儲存到令牌儲存器來完成身份驗證流程。  

>[!WARNING]
>
> **中止驗證流程**  <br>請注意，這是使用者能夠按下「返回」按鈕的點，這等同於中止驗證流程。 在這種情況下，您的應用程式必須呼叫 _setSelectedProvider()_ 傳遞 _null_ 作為參數，並讓Access Enabler有機會重置其身份驗證狀態機。

| 回撥：顯示MVPD登入頁面 |
| --- |
| 公用void navigateToUrl（字串URL） |

**可用性：** v1.0+

**參數：**

- *url*:指向MVPD登入頁面的URL

**觸發者：** `getAuthentication(), setSelectedProvider()`

[返回Android API...](#api)


### getAuthenticationToken {#getAuthNToken}

**已棄用：** 從Android SDK 3.0開始，由於Chrome自訂分頁用於驗證，因此應用程式不再使用此方法。

**說明：** 從後端伺服器要求驗證Token以完成驗證流程。 您的應用程式只應在回應MVPD登入頁面所在的WebView控制項，重新導向至由 `AccessEnabler.ADOBEPASS_REDIRECT_URL` 常數。

| API呼叫：擷取驗證Token |
| --- |
| public void getAuthenticationToken() |

**可用性：** v1.0+

**參數：**

- *cookie*:目標網域上設定的Cookie（如需參考實作，請參閱SDK中的示範應用程式）。

**已觸發回呼：** `setAuthenticationStatus()`, `sendTrackingData()`

[返回Android API...](#api)


### setAuthenticationStatus {#setAuthNStatus}

**說明：** 由Access Enabler觸發的回調，它通知應用程式驗證流的狀態。 有許多地方可能會因為用戶交互或其他意外情況（如網路連接問題等）而導致此流失敗。 此回呼會通知應用程式驗證流程的成功/失敗狀態，並視需要提供關於失敗原因的其他資訊。

| 回撥：報告驗證流程的狀態 |
| --- |
| public void setAuthenticationStatus(int status, String errorCode) |

**可用性：** v1.0+

**參數：**

- *狀態*:可採用下列其中一個值：
   - `AccessEnablerConstants.ACCESS_ENABLER_STATUS_SUCCESS`  — 驗證流程已成功完成
   - `AccessEnablerConstants.ACCESS_ENABLER_STATUS_ERROR`  — 驗證流失敗
- *代碼*:失敗原因。 若 *狀態* is `AccessEnablerConstants.ACCESS_ENABLER_STATUS_SUCCESS`，然後 *代碼* 是空字串(亦即，由 `AccessEnablerConstants.USER_AUTHENTICATED` 常數)。 如果失敗，此參數可取用下列其中一個值：
   - `AccessEnablerConstants.USER_NOT_AUTHENTICATED_ERROR`  — 未驗證用戶。 回應 *checkAuthentication()* 當本機權杖快取中沒有有效的驗證權杖時，方法會呼叫。
   - `AccessEnablerConstants.PROVIDER_NOT_SELECTED_ERROR`  — 在上層應用程式通過後， AccessEnabler已重置身份驗證狀態機 *null* to `setSelectedProvider()` 中止驗證流程。  用戶可能已取消身份驗證流（即按「返回」按鈕）。
   - `AccessEnablerConstants.GENERIC_AUTHENTICATION_ERROR`  — 由於網路不可用或用戶明確取消身份驗證流等原因，身份驗證流失敗。

**觸發者：** `checkAuthentication(), getAuthentication(), checkAuthorization()`

[返回Android API...](#api)


### checkPreauthorizedResources {#checkPreauth}

>**已棄用：** 從Android SDK 3.6開始，預先授權API將取代checkPreauthorizedResources，提供延伸的錯誤碼。 

**說明：** 此方法由應用程式用於確定用戶是否已獲得查看特定受保護資源的授權。 此方法的主要用途是擷取用於裝飾UI的資訊（例如，使用鎖定和解鎖圖示指示存取狀態）。

| API呼叫：設定當前選擇的提供程式 |
| --- |
| `public void checkPreauthorizedResources(ArrayList<String> resources)` |

**可用性：** v1.3+

**參數：** 此 `resources` 參數是應檢查授權的資源陣列。 清單中的每個元素都應是代表資源ID的字串。 資源ID受與 `getAuthorization()` 呼叫，即，它應是程式設計師和MVPD或媒體RSS片段之間建立的商定值。

**已觸發回呼：** `preauthorizedResources()`

[返回Android API...](#api)


### checkPreauthorizedResources {#checkPreauth2}

**已棄用：** 從Android SDK 3.6開始，預先授權API將取代checkPreauthorizedResources，提供延伸的錯誤碼。 

**說明：** 此方法由應用程式用於確定用戶是否已獲得查看特定受保護資源的授權。 此方法的主要用途是擷取用於裝飾UI的資訊（例如，使用鎖定和解鎖圖示指示存取狀態）。

| API呼叫：設定當前選擇的提供程式 |
| --- |
| `public void checkPreauthorizedResources(ArrayList<String> resources, boolean cache)` |

**可用性：** v3.1+

**參數：** 此 `resources` 參數是應檢查授權的資源陣列。 清單中的每個元素都應是代表資源ID的字串。 資源ID受與 `getAuthorization()` 呼叫，即，它應是程式設計師和MVPD或媒體RSS片段之間建立的商定值。

此 `cache` 參數指定是否可以使用快取預授權響應。 根據預設，快取為true,SDK會傳回先前快取的回應（若有）。

**已觸發回呼：** `preauthorizedResources()`

[返回Android API...](#api)

### preauthorizedResources {#preauthResources}

**已棄用：** 從Android SDK 3.6開始，預先授權API將取代checkPreauthorizedResources，提供延伸的錯誤碼。 不會在新API上呼叫preauthorizedResources回呼。


**說明：** 由checkPreauthorizedResources()觸發的回呼。 提供已授權用戶查看的資源清單。

| API呼叫：設定當前選擇的提供程式 |
| --- |
| `public void checkPreauthorizedResources(ArrayList<String> resources)` |

**可用性：** v1.3+

**參數：** 此 `resources` 參數是一組資源，使用者已獲授權可檢視。

**觸發者：** `checkPreauthorizedResources()`

[返回Android API...](#api)

### <span id="checkAuthZ"></span>checkAuthorization

**說明：** 此方法由應用程式用來檢查授權狀態。 首先檢查驗證狀態。 若未驗證，則 *setTokenRequestFailed()* 回呼會觸發，方法會退出。 如果使用者已驗證，也會觸發授權流程。 請參閱 *getAuthorization()* 方法。

| API呼叫：檢查授權狀態 |
| --- |
| public void checkAuthorization(String resourceId) |

**可用性：** v1.0+

| API呼叫：檢查授權狀態 |
| --- |
| public void checkAuthorization(String resourceId, Map&lt;string object=&quot;&quot;> genericData) |

**可用性：** v1.8+

**參數：**

- *resourceId*:用戶向其請求授權的資源ID。
- *資料*:由要傳送至付費電視傳遞服務的鍵值值組所組成的地圖。 Adobe可以使用此資料來啟用未來功能，而不需變更SDK。

**已觸發回呼：** `tokenRequestFailed(), setToken(),sendTrackingData(), setAuthenticationStatus()`

[返回Android API...](#api)


### <span id="getAuthZ"></span>getAuthorization

**說明：** 此方法由應用程式用來啟動授權流程。 如果用戶尚未驗證，則還會啟動驗證流。 如果用戶通過驗證，Access Enabler將繼續發出授權令牌（如果本地令牌快取中沒有有效的授權令牌）和短期媒體令牌的請求。 一旦獲得短媒體令牌，則認為授權流程已完成。 此 *setToken()* 會觸發回呼，並將短媒體代號以參數的形式傳送至應用程式。 若因任何原因，授權會失敗， *tokenRequestFailed()* 會觸發回呼，並提供錯誤碼和詳細資料。

| API呼叫：啟動授權流程 |
| --- |
| public void getAuthorization(String resourceId) |

**可用性：** v1.0+

| API呼叫：啟動授權流程 |
| --- |
| public void getAuthorization(String resourceId, Map&lt;string object=&quot;&quot;> genericData) |

**可用性：** v1.8+

**參數：**

- *resourceId*:用戶向其請求授權的資源ID。
- *資料*:由要傳送至付費電視傳遞服務的鍵值值組所組成的地圖。 Adobe可以使用此資料來啟用未來功能，而不需變更SDK。 

**已觸發回呼：** `tokenRequestFailed(), setToken(), sendTrackingData()`

>[!WARNING]
>
> **已觸發其他回呼**  <br> 此方法也可以觸發下列回呼（如果也啟動驗證流程）: *setAuthenticationStatus()*, *displayProviderDialog()*, *navigateToUrl()*

**注意：請盡可能使用checkAuthorization()，而不是getAuthorization()。 getAuthorization()方法將啟動完整身份驗證流（如果用戶未通過身份驗證），這可能導致程式設計師端的複雜實現。**

[返回Android API...](#api)


### setToken {#setToken}

**說明：** 由Access Enabler觸發的回調，該回調通知您的應用程式授權流程已成功完成。 短期媒體代號也會以參數的形式傳送。

| 回撥：已成功完成授權流程 |
| --- |
| public void setToken(String token, String resourceId) |

**可用性：** v1.0+

**參數：**

- *token*:短暫的媒體代號
- *resourceId*:獲得授權的資源

**觸發者：** `checkAuthorization()`, `getAuthorization()`


[返回Android API...](#api)

### tokenRequestFailed {#tokenRequestFailed}

**說明：** 由Access Enabler觸發的回調，該回調通知上層應用程式授權流失敗。

| 回撥：授權流失敗 |
| --- |
| public void tokenRequestFailed(String resourceId, <br>        字串errorCode，字串errorDescription) |

**可用性：** v1.0+

**參數：**

- *resourceId*:獲得授權的資源
- *errorCode*:與失敗情境相關聯的錯誤代碼。 可能的值：
   - `AccessEnablerConstants.USER_NOT_AUTHORIZED_ERROR`  — 用戶無法為給定資源授權
- *errorDescription*:有關失敗情況的其他詳細資訊。 如果此描述性字串因任何原因無法使用，Adobe Primetime驗證會傳送空字串 **(&quot;&quot;)**.

   MVPD可使用此字串來傳遞自訂錯誤訊息或銷售相關訊息。 例如，如果訂閱者被拒絕對資源進行授權，MVPD可能會傳送如下訊息：「您目前無法在套件中存取此管道。 如果您想要升級您的套件，請按一下這裡。」 該消息由Adobe Primetime身份驗證通過此回調傳遞給程式設計師，他們可以選擇顯示或忽略它。 Adobe Primetime驗證也可使用此參數來提供可能導致錯誤的條件通知。 例如，「與提供者的授權服務通訊時發生網路錯誤。」

**觸發者：** `checkAuthorization(), getAuthorization()`

[返回Android API...](#api)

### 註銷 {#logout}

**說明：** 使用此方法來啟動註銷流程。 登出是一系列HTTP重新導向操作的結果，因為使用者需要從Adobe Primetime驗證伺服器以及MVPD的伺服器登出。 因此，此流無法通過Access Enabler庫發出的簡單HTTP請求完成。 SDK會使用Chrome自訂分頁來執行HTTP重新導向操作。 此流程將對使用者可見，並在完成時關閉

| API呼叫：啟動註銷流程 |
| --- |
| 公共撤消註銷() |

**可用性：** v1.0+

**參數：** 無

**已觸發回呼：**

- `navigateToUrl()` （適用於3.0之前的SDK版本）
- `setAuthenticationStatus()` 適用於SDK 3.0版以上


[返回Android API...](#api)


### getSelectedProvider {#getSelectedProvider}

**說明：** 使用此方法來確定當前選擇的提供程式。

| API呼叫：決定目前選取的MVPD |
| --- |
| public void getSelectedProvider() |

**可用性：** v1.0+

**參數：** 無

**已觸發回呼：** `selectedProvider()`

[返回Android API...](#api)


### <span id="selectedProvider"></span>selectedProvider

**說明：** 由Access Enabler觸發的回調，該啟用程式將有關當前所選MVPD的資訊提供給應用程式。

| 回撥：目前選取之MVPD的相關資訊 |
| --- |
| public void selectedProvider(Mvpd mvpd) |


**可用性：** v1.0+

**參數：**

- *mvpd*:包含當前所選MVPD資訊的對象

**觸發者：** `getSelectedProvider()`

[返回Android API...](#api)


### getMetadata {#getMetadata}

**說明：** 使用此方法可檢索Access Enabler庫作為元資料公開的資訊。 應用程式可通過提供複合MetadataKey對象來訪問此資訊。

| API呼叫：查詢AccessEnabler中的元資料 |
| --- |
| `public void getMetadata(MetadataKey metadataKey)` |

**可用性：** v1.0+

程式設計師有兩種可用的元資料：

- 靜態中繼資料（驗證Token TTL、授權Token TTL和裝置ID） 
- 使用者中繼資料（使用者專屬資訊，例如使用者ID和郵遞區號；在驗證和/或授權流程期間從MVPD傳遞至使用者裝置）

**參數：**

- *metadataKey*:封裝索引鍵和args變數的資料結構，其含義如下：
   - 如果鍵為 `METADATA_KEY_USER_META` 和args包含名稱為=的SerializableNameValuePair對象 `METADATA_ARG_USER_META` 和值= `[metadata_name]`，則會為使用者中繼資料建立查詢。 可用用戶元資料類型的當前清單：
      - `zip`  — 郵遞區號

      - `householdID`  — 家庭標識符。 如果MVPD不支援子帳戶，則會與 `userID`.

      - `maxRating`  — 用戶的最高父母分級

      - `userID`  — 使用者識別碼。 如果MVPD支援子帳戶，且使用者不是主帳戶， `userID` 將不同於 `householdID`.

      - `channelID`  — 使用者有權檢視的管道清單
   - 如果鍵為 `METADATA_KEY_DEVICE_ID` 然後進行查詢以取得目前的裝置id。 請注意，此功能預設為停用，程式設計人員應聯絡Adobe，以取得啟用和費用的相關資訊。
   - 如果鍵為 `METADATA_KEY_TTL_AUTHZ` 和args包含名稱為=的SerializableNameValuePair對象 `METADATA_ARG_RESOURCE_ID` 和值= `[resource_id]`，然後進行查詢以取得與指定資源相關聯的授權權杖的到期時間。
   - 如果鍵為 `METADATA_KEY_TTL_AUTHN` 然後進行查詢以取得驗證Token過期時間。 

 

>[!NOTE]
>
>SDK 3.4.0的常數： `METADATA_KEY_USER_META, METADATA_KEY_DEVICE_ID, METADATA_KEY_TTL_AUTHZ, METADATA_KEY_TTL_AUTHN` 可從com.adobe.adobepass.accessenabler.api.profile.UserProfileService取得。



>[!NOTE]
>
>程式設計師可用的實際用戶元資料取決於MVPD提供的內容。  當新中繼資料可供使用並新增至Adobe Primetime驗證系統時，此清單將會進一步擴充。

**已觸發回呼：** [`setMetadataStatus()`](#setMetadaStatus)

**更多資訊：** [使用者中繼資料](/help/authentication/user-metadata-feature.md)

[返回Android API...](#api)

### setMetadataStatus {#setMetadaStatus}

**說明：** 由Access Enabler觸發的回調，該啟用程式通過 *getMetadata()* 呼叫。

| 回撥：元資料檢索請求的結果 |
| --- |
| ```public void setMetadataStatus(MetadataKey key, MetadataStatus result)``` |

**可用性：** v1.0+

**參數：**

- *key*:MetadataKey物件，包含要求中繼資料值的索引鍵和相關參數（如需參考實作，請參閱示範應用程式）。
- *結果*:包含所請求元資料的複合對象。 物件有下列欄位：
   - *simpleResult*:代表提出驗證TTL、授權TTL或裝置ID要求時中繼資料值的字串。 如果對用戶元資料提出請求，則此值為null。

   - *userMetadataResult*:包含JSON使用者中繼資料裝載的Java表示的物件。\
      例如：

```json
          '{
          "street": "Main Avenue",
          "buildings": ["150", "320"]
          }'
```

會轉換為Java，如下所示： 

```java
          Map("street" -> "Main Avenue", "buildings" -> List("150", "320")))
```

**用戶元資料對象的實際結構類似於以下內容：**

```json
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
          }
```

對簡單中繼資料（驗證TTL、授權TTL或裝置ID）提出要求時，此值為null。

- *加密*:指定是否加密檢索的元資料的布爾值。 此參數只對使用者中繼資料請求有顯著意義，對靜態中繼資料沒有意義(例如：驗證TTL)，一律未加密接收。 如果此參數設定為True，則由程式設計師通過使用白名單私鑰執行RSA解密來獲取未加密的用戶元資料值(用於在 [`setRequestor`](#setRequestor) 呼叫)。

**觸發者：** [`getMetadata()`](#getMetadata)

**更多資訊：** [使用者中繼資料](/help/authentication/user-metadata-feature.md)


[返回Android API...](#api)


### getVersion {#getVersion}

**說明：** 此方法可用於檢索AccessEnabler庫的版本。

| API呼叫：獲取AccessEnabler版本 |
| --- |
| ```public static String getVersion()``` |


[返回Android API...](#api)

</br>

## 追蹤事件 {#tracking}

Access Enabler會觸發與權限流程不一定相關的附加回調。 實作事件追蹤回呼函式，命名為 *sendTrackingData()* 是可選的，但它使應用程式能夠跟蹤特定事件並編譯統計資訊，如成功/失敗的身份驗證/授權嘗試次數。 以下是 *sendTrackingData()* 回呼：\
 

### sendTrackingData {#sendTrackingData}

**說明：** 由Access Enabler向應用程式發出信號時觸發的回調，該信號會發生各種事件，如驗證/授權流的完成/失敗。 sendTrackingData()還報告了設備類型、Access Enabler客戶端類型和作業系統。

>[!WARNING]
>
> 裝置類型和作業系統是透過使用公用Java程式庫([http://java.net/projects/user-agent-utils](http://java.net/projects/user-agent-utils))和使用者代理字串。 請注意，此資訊僅作為將操作量度劃分為裝置類別的粗略方式提供，但該Adobe對錯誤的結果不負責。 請據此使用新功能。


- 設備類型的可能值：
   - `computer`
   - `tablet`
   - `mobile`
   - `gameconsole`
   - `unknown`


- Access Enabler客戶端類型的可能值：
   - `flash`
   - `html5`
   - `ios`
   - `android`

</br>

| 回撥：追蹤事件 |
| --- |
| ```public void sendTrackingData(Event event, ArrayList<String> data)``` |

**可用性：** v1.0+

**參數：**

- *事件*:正在追蹤的事件。 有三種可能的追蹤事件類型：
   - **authorizationDetection:** 任何時候授權Token請求傳回(事件類型為 `EVENT_AUTHZ_DETECTION`)
   - **authenticationDetection:** 任何時候進行驗證檢查(事件類型為 `EVENT_AUTHN_DETECTION`)
   - **mvpdSelection:** 當使用者在MVPD選取表單中選取MVPD時(事件類型為 `EVENT_MVPD_SELECTION`)
- *資料*:與報告事件相關聯的其他資料。 此資料會以值清單的形式呈現。

以下是解譯 *資料*
陣列：

- 針對事件類型 *`EVENT_AUTHN_DETECTION`:*
   - **0**  — 代號要求是否成功(true/false)，如果上述是true:
   - **1** - MVPD ID字串
   - **2** - GUID（md5雜湊）
   - **3**  — 已在快取中的Token(true/false)
   - **4**  — 設備類型
   - **5**  — 訪問啟用碼客戶端類型
   - **6**  — 作業系統類型

- 針對事件類型 `EVENT_AUTHZ_DETECTION`
   - **0**  — 代號要求是否成功(true/false)，如果成功：
   - **1** - MVPD ID
   - **2** - GUID（md5雜湊）
   - **3**  — 已在快取中的Token(true/false)
   - **4**  — 錯誤
   - **5**  — 詳細資訊
   - **6**  — 設備類型
   - **7**  — 訪問啟用碼客戶端類型
   - **8**  — 作業系統類型

- 針對事件類型 `EVENT_MVPD_SELECTION`
   - **0**  — 目前選取的MVPD ID
   - **1**  — 設備類型
   - **2**  — 訪問啟用碼客戶端類型
   - **3**  — 作業系統類型

**觸發者：** `checkAuthentication()`, `getAuthentication()`, `checkAuthorization()`, `getAuthorization()`, `setSelectedProvider()`

[返回Android API...](#api)


<!--
## Related Information {#related}

- [Android Integration Cookbook](/help/authentication/android-sdk-cookbook.md)
- [Android Technical Overview](/help/authentication/android-sdk-overview.md)

-->
