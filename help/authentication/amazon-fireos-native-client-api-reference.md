---
title: Amazon FireOS原生用戶端API參考
description: Amazon FireOS原生用戶端API參考
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '3416'
ht-degree: 0%

---


# Amazon FireOS原生用戶端API參考 {#amazon-fireos-native-client-api-reference}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

</br>

## 簡介 {#intro}

本檔案詳細說明Amazon FireOS SDK公開的Adobe Primetime驗證方法和回呼(支援Adobe Primetime驗證)。</span> 此處描述的方法和回調函式在AccessEnabler.h和EntitlementDelegate.h標頭檔案中定義。

請參閱 <https://tve.zendesk.com/hc/en-us/articles/115005561623-fire-TV-Native-AccessEnabler-Library> 以取得最新的Amazon FireOS AccessEnabler SDK。 

**注意：** Adobe Primetime驗證團隊鼓勵您只使用Adobe Primetime驗證 *公共* API:

- 公用API可供使用 *經過充分測試* 所有支援的用戶端類型。 對於任何公用功能，我們會確定每個用戶端類型都具有相關聯方法的對應版本。
- 公用API必須盡可能穩定，以支援回溯相容性，並確保合作夥伴整合不會中斷。 不過， *non* — 公用API，我們保留在未來任何時間點更改其簽名的權利。 如果您遇到無法透過目前公用Adobe Primetime驗證API呼叫組合來支援的特定流程，最佳方法就是告訴我們。 根據您的需求，我們可以修改公用API，並提供穩定的解決方案，以推動未來的發展。

## Amazon FireOS SDK API {#api}

- [getInstance](#getInstance)
- [setOptions](#fire_setOption)
- [setRequestor](#setRequestor)
- [setRequestorComplete](#setRequestorComplete)
- [checkAuthentication](#checkAuthN)
- [getAuthentication](#getAuthN)
- [displayProviderDialog](#displayProviderDialog)
- [setSelectedProvider](#setSelectedProvider)
- [navigateToUrl](#navigagteToUrl)
- [getAuthenticationToken](#getAuthNToken)
- [setAuthenticationStatus](#setAuthNStatus)
- [checkPreauthorizedResources](#checkPreauth)
- [preauthorizedResources](#preauthResources)
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

</br>

### Factory.getInstance {#getInstance}

**說明：** 實例化Access Enabler對象。 每個應用程式實例應有一個Access Enabler實例。

| API呼叫：建構函式 |
| --- |
| ```public static AccessEnabler getInstance(Context appContext, String softwareStatement, String redirectUrl)<br>        throws AccessEnablerException```<br><br> |
| ```public static AccessEnabler getInstance(Context appContext, String env_url, String softwareStatement, String redirectUrl) throws AccessEnablerException``` |

**可用性：** v3.0+


**參數：**

- *appContext*:Amazon引發OS應用程式內容。
- softwareStatement
- redirectUrl :若是FireOS，則會忽略參數值，並設為預設值：adobepass://android.app
- env_url:若要使用Adobe中繼環境進行測試，可將env\_url設為「sp.auth-staging.adobe.com」

**已棄用：**

```java
    public static AccessEnabler getInstance(Context appContext)
        throws AccessEnablerException
```
 

### setRequestor {#setRequestor}

**說明：** 建立程式設計師的身份。 在向Adobe Primetime驗證系統的Adobe註冊時，每個程式設計師被分配一個唯一ID。 此設定在應用程式的生命週期中只應執行一次。

伺服器響應包含MVPD的清單以及附加到程式設計師標識的一些配置資訊。 伺服器響應由Access Enabler代碼在內部使用。 只會透過setRequestorComplete()回呼向您的應用程式顯示操作狀態（即SUCCESS/FAIL）。

若 *url* 參數，則產生的網路呼叫會鎖定預設服務提供者URL:Adobe發行/生產環境。

如果為 *url* 參數，產生的網路呼叫會鎖定 *url* 參數。 所有配置請求都在單獨的線程中同時觸發。 編譯MVPD清單時，第一回應者優先。 對於清單中的每個MVPD,Access Enabler會記住相關服務提供商的URL。 所有後續的權限請求都會導向至在設定階段與目標MVPD成對之服務提供者相關聯的URL。

| API呼叫：請求者設定 |
| --- |
| ```public void setRequestor(String requestorId)``` |


**可用性：**v 3.0+


| API呼叫：請求者設定 |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**可用性：** v3.0+


**參數：**

- *requestorID*:與程式設計師關聯的唯一ID。 在您首次向Adobe Primetime驗證服務註冊時，將Adobe指派的唯一ID傳遞至您的網站。
- *url*:選用參數；依預設，會使用Adobe服務提供者(http://sp.auth.adobe.com/)。 此陣列可讓您為Adobe提供的驗證和授權服務指定端點（可能會使用不同的執行個體進行除錯）。 您可以使用此ID來指定多個Adobe Primetime驗證服務提供者例項。 執行此操作時，MVPD清單由來自所有服務提供者的端點組成。 每個MVPD都與最快的服務提供商相關聯；即第一個回應且支援該MVPD的提供者。

**已觸發回呼：** `setRequestorComplete()`

 

**已棄用：**

```
    public void setRequestor(String requestorId, String signedRequestorId)

    public void setRequestor(String requestorId, String signedRequestorId, ArrayList<String> urls)
```
 
</br>


### setRequestorComplete {#setRequestorComplete}

**說明：** 由Access Enabler觸發的回調，該回調通知您的應用程式配置階段已完成。 這是一個訊號，表示應用程式可以開始發出權限請求。 在配置階段完成之前，應用程式不能發出任何權限請求。

| 回撥：請求者配置完成 |
| --- |
| ```public void setRequestorComplete(int status)``` |

**可用性：** v1.0+

**參數：**

- *狀態*:可採用下列其中一個值：
   - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS`  — 已成功完成配置階段
   - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR`  — 配置階段失敗

**觸發者：** `setRequestor()`

</br> 


### setOptions {#fire_setOption}

**說明：** 設定全域SDK選項。 接受 **地圖\&lt;string string=&quot;&quot;>** 作為引數。 地圖中的值會連同SDK進行的每個網路呼叫一併傳遞至伺服器。

這些值將獨立於當前流（驗證/授權）傳遞到伺服器。 如果您想要變更值，可以隨時呼叫此方法。

 

| API呼叫：setOptions |
| --- |
| ```public void setOptions(HashMap<String,String> options)``` |

**可用性：** v3.0+

**參數：**

- *選項*:地圖\&lt;string string=&quot;&quot;> 包含全域SDK選項。 目前提供下列選項：
   - **applicationProfile**  — 可根據此值進行伺服器配置。
   - **ap\_vi** -Marketing CloudvisitorID。 此值稍後可用於進階分析報表。
   - **device\_info**  — 設備資訊，如 **傳遞裝置資訊逐步指南**

</br>

### checkAuthentication {#checkAuthN}

**說明：** 檢查驗證狀態。 它會透過搜尋本機Token儲存空間中的有效驗證Token來執行此作業。 呼叫此方法不會執行網路呼叫。 應用程式使用它來查詢使用者的驗證狀態並據以更新UI（即更新登入/登出UI）。 驗證狀態通過 [*setAuthenticationStatus()*](#setAuthNStatus) 回呼。

如果MVPD支援「每個要求者進行驗證」功能，則可在裝置上儲存多個驗證Token。 

| API呼叫：檢查驗證狀態 |
| --- |
| ```public void checkAuthentication()``` |

**可用性：** v1.0+

**參數：** 無

**已觸發回呼：** `setAuthenticationStatus()`

</br>

### getAuthentication {#getAuthN}

**說明：** 啟動完整驗證工作流程。 首先檢查驗證狀態。 如果尚未驗證，則啟動驗證流狀態機：

- 如果上次驗證嘗試成功，則會跳過MVPD選擇階段，WebView控制項將向用戶顯示MVPD的登錄頁。
- 如果上次驗證嘗試失敗或用戶明確登出，則 [*displayProviderDialog()*](#displayProviderDialog) 已觸發回呼。 您的應用程式會使用此回呼來顯示MVPD選取UI。 此外，您的應用程式必須透過 [setSelectedProvider()](#setSelectedProvider) 方法。

如果MVPD支援「每個請求者的驗證」功能，則可在一個裝置上儲存多個驗證Token（每個程式設計師一個）。

最後，驗證狀態通過 *setAuthenticationStatus()* 回呼。

| API呼叫：啟動驗證流程 |
| --- |
| ```public void getAuthentication()``` |

**可用性：** v1.0+

| API呼叫：啟動驗證流程 |
| --- |
| ```public void getAuthentication(boolean forceAuthN, Map<String, Object> genericData)``` |

**可用性：** v1.0+

**參數：**

- *forceAuthn*:此標幟指定是否應啟動驗證流程，而不論使用者是否已通過驗證。
- *資料*:由要傳送至付費電視傳遞服務的鍵值值組所組成的地圖。 Adobe可以使用此資料來啟用未來功能，而不需變更SDK。

**已觸發回呼：** `setAuthenticationStatus(), displayProviderDialog(), sendTrackingData()`

</br>

### displayProviderDialog {#displayProviderDialog}

**說明** 由Access Enabler觸發的回呼，通知應用程式需要具現化適當的UI元素，以允許使用者選取所需的MVPD。 回呼會提供MVPD物件清單，其中包含可協助正確建立選取UI面板的其他資訊（例如指向MVPD標誌的URL、好記的顯示名稱等）

一旦使用者選取了所需的MVPD，上層應用程式就需要透過呼叫來繼續驗證流程 *setSelectedProvider()* 並傳遞與使用者選取相對應之MVPD的ID。\
 

| **回撥：顯示MVPD選擇UI** |
| --- |
| ```public void displayProviderDialog(ArrayList<Mvpd> mvpds)``` |

**可用性：** v1.0+

**參數**:

- *mvpds*:MVPD物件清單，其中包含應用程式可用於建立MVPD選取UI元素的MVPD相關資訊。

**觸發者：** `getAuthentication(), getAuthorization()`

</br>

### setSelectedProvider {#setSelectedProvider}

**說明：** 應用程式會呼叫此方法，以通知Access Enabler使用者的MVPD選擇。 傳遞時 *null* 作為參數，Access Enabler將當前MVPD重置為null值。

| **API呼叫：設定當前選擇的提供程式** |
| --- |
| ```public void setSelectedProvider(String mvpdId)``` |


**可用性：**v 1.0+

**參數：** 無

**已觸發回呼：** `setAuthenticationStatus(), sendTrackingData()`
</br>

### navigateToUrl {#navigagteToUrl}

**說明：** 由Android SDK上的Access Enabler觸發的回呼。 在Amazon FireOS SDK上應忽略它。

| **回撥：顯示MVPD登入頁面** |
| --- |
| ```public void navigateToUrl(String url)``` |

**可用性：** v1.0+

**參數：**

- *url*:指向MVPD登入頁面的URL

**觸發者：** `getAuthentication(), setSelectedProvider()`

</br>

### getAuthenticationToken {#getAuthNToken}

**說明：** 從後端伺服器要求驗證Token以完成驗證流程。 

| **API呼叫：擷取驗證Token** |
| --- |
| ```public void getAuthenticationToken(String cookies)``` |

**可用性：** v1.0+

**參數：**

- *cookie*:目標網域上設定的Cookie（如需參考實作，請參閱SDK中的示範應用程式）。

**已觸發回呼：** `setAuthenticationStatus(), sendTrackingData()`

</br>

### setAuthenticationStatus {#setAuthNStatus}

**說明：** 由Access Enabler觸發的回調，它通知應用程式身份驗證的狀態。 有許多地方的驗證流可能會失敗，原因可能是用戶交互或其他不可預見的情況（如網路連接問題等）。 此回呼會通知應用程式驗證的成功/失敗狀態，並視需要提供關於失敗原因的其他資訊。

註銷流程完成時，此回調也會發出信號。

| **回撥：報告驗證流程的狀態** |
| --- |
| ```public void setAuthenticationStatus(int status, String errorCode)``` |

**可用性：** v1.0+

**參數：**

- *狀態*:可採用下列其中一個值：
   - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS`  — 驗證流程已成功完成
   - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR`  — 驗證流失敗
   - `AccessEnabler.ACCESS_ENABLER_STATUS_LOGOUT`  — 註銷
- *代碼*:呈現狀態的原因。 若 *狀態* is `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS`，然後 *代碼* 是空字串(亦即，由 `AccessEnabler.USER_AUTHENTICATED` 常數)。 如果未驗證，此參數可能會取用下列其中一個值：
   - `AccessEnabler.USER_NOT_AUTHENTICATED_ERROR`  — 未驗證用戶。 回應 *checkAuthentication()* 當本機權杖快取中沒有有效的驗證權杖時，方法會呼叫。
   - `AccessEnabler.PROVIDER_NOT_SELECTED_ERROR`  — 在上層應用程式通過後， AccessEnabler已重置身份驗證狀態機 *null* to `setSelectedProvider()` 中止驗證流程。  用戶可能已取消身份驗證流（即按「返回」按鈕）。
   - `AccessEnabler.GENERIC_AUTHENTICATION_ERROR`  — 由於網路不可用或用戶明確取消身份驗證流等原因，身份驗證流失敗。
   - `AccessEnabler.LOGOUT`  — 由於註銷操作，用戶未被驗證。 

**觸發者：** `checkAuthentication(), getAuthentication(), checkAuthorization()`

</br>

### checkPreauthorizedResources {#checkPreauth}

**說明：** 此方法由應用程式用於確定用戶是否已獲得查看特定受保護資源的授權。 此方法的主要用途是擷取用於裝飾UI的資訊（例如，使用鎖定和解鎖圖示指示存取狀態）。

| **API呼叫：設定當前選擇的提供程式** |
| --- |
| ```public void checkPreauthorizedResources(ArrayList<String> resources)``` |

**可用性：** v1.0+

**&lt;parameters: span=&quot;&quot; id=&quot;1&quot; translate=&quot;no&quot; /> 此 `resources` 參數是應檢查授權的資源陣列。**&#x200B;清單中的每個元素都應是代表資源ID的字串。 資源ID受與 `getAuthorization()` 呼叫，即，它應是程式設計師和MVPD或媒體RSS片段之間建立的商定值。

**已觸發回呼：** `preauthorizedResources()`

</br>

### preauthorizedResources {#preauthResources}

**說明：** 由checkPreauthorizedResources()觸發的回呼。 提供已授權用戶查看的資源清單。

| **API呼叫：設定當前選擇的提供程式** |
| --- |
| ```public void checkPreauthorizedResources(ArrayList<String> resources)``` |

**可用性：**v 1.0+

**參數：** 此 `resources` 參數是一組資源，使用者已獲授權可檢視。

**觸發者：** `checkPreauthorizedResources()`

<br>

### checkAuthorization {#checkAuthZ}

**說明：** 此方法由應用程式用來檢查授權狀態。 首先檢查驗證狀態。 若未驗證，則 *setTokenRequestFailed()* 回呼會觸發，方法會退出。 如果使用者已驗證，也會觸發授權流程。 請參閱 *getAuthorization()* 方法。

| **API呼叫：檢查授權狀態** |
| --- |
| ```public void checkAuthorization(String resourceId)``` |

**可用性：** v1.0+

| **API呼叫：檢查授權狀態** |
| --- |
| ```public void checkAuthorization(String resourceId, Map<String, Object> genericData)``` |

**可用性：** v1.0+

**參數：**

- *resourceId*:用戶向其請求授權的資源ID。
- *資料*:由要傳送至付費電視傳遞服務的鍵值值組所組成的地圖。 Adobe可以使用此資料來啟用未來功能，而不需變更SDK。

**已觸發回呼：** `tokenRequestFailed(), setToken(), sendTrackingData(), setAuthenticationStatus()`

</br>

### getAuthorization {#getAuthZ}

**說明：** 此方法由應用程式用來啟動授權流程。 如果用戶尚未驗證，則還會啟動驗證流。 如果用戶通過驗證，Access Enabler將繼續發出授權令牌（如果本地令牌快取中沒有有效的授權令牌）和短期媒體令牌的請求。 一旦獲得短媒體令牌，則認為授權流程已完成。 此 *setToken()* 會觸發回呼，並將短媒體代號以參數的形式傳送至應用程式。 若因任何原因，授權會失敗， *tokenRequestFailed()* 會觸發回呼，並提供錯誤碼和詳細資料。

| **API呼叫：啟動授權流程** |
| --- |
| ```public void getAuthorization(String resourceId)``` |

**可用性：** v1.0+

| **API呼叫：啟動授權流程** |
| --- |
| ```public void getAuthorization(String resourceId, Map<String, Object> genericData)``` |

**可用性：** v1.0+

**參數：**

- *resourceId*:用戶向其請求授權的資源ID。
- *資料*:由要傳送至付費電視傳遞服務的鍵值值組所組成的地圖。 Adobe可以使用此資料來啟用未來功能，而不需變更SDK。 

**已觸發回呼：** `tokenRequestFailed(), setToken(), sendTrackingData()`

|  |  |
| --- | --- |
| ![](http://learn.adobe.com/wiki/images/icons/emoticons/warning.gif) | **已觸發其他回呼**  <br>此方法也可以觸發下列回呼（如果也啟動驗證流程）: _setAuthenticationStatus()_, _displayProviderDialog()_ |

**注意：請盡可能使用checkAuthorization()，而不是getAuthorization()。 getAuthorization()方法將啟動完整身份驗證流（如果用戶未通過身份驗證），這可能導致程式設計師端的複雜實現。**

</br>

### setToken {#setToken}

**說明：** 由Access Enabler觸發的回調，該回調通知您的應用程式授權流程已成功完成。 短期媒體代號也會以參數的形式傳送。

| **回撥：已成功完成授權流程** |
| --- |
| ```public void setToken(String token, String resourceId)``` |

**可用性：**v 1.0+

**參數：**

- *token*:短暫的媒體代號
- *resourceId*:獲得授權的資源

**觸發者：** `checkAuthorization(), getAuthorization()`

<br>

### tokenRequestFailed {#tokenRequestFailed}

**說明：** 由Access Enabler觸發的回調，該回調通知上層應用程式授權流失敗。

| **回撥：授權流失敗** |
| --- |
| ```public void tokenRequestFailed(String resourceId, <br>        String errorCode, String errorDescription)``` |

**可用性：** v1.0+

**參數：**

- *resourceId*:獲得授權的資源
- *errorCode*:與失敗情境相關聯的錯誤代碼。 可能的值：
   - `AccessEnabler.USER_NOT_AUTHORIZED_ERROR`  — 用戶無法為給定資源授權
- *errorDescription*:有關失敗情況的其他詳細資訊。 如果此描述性字串因任何原因無法使用，Adobe Primetime驗證會傳送空字串>**(&quot;&quot;)**.  MVPD可使用此字串來傳遞自訂錯誤訊息或銷售相關訊息。 例如，如果訂閱者被拒絕對資源進行授權，MVPD可能會傳送如下訊息：「您目前無法在套件中存取此管道。 如果您想要升級您的套件，請按一下這裡。」 該消息由Adobe Primetime身份驗證通過此回調傳遞給程式設計師，他們可以選擇顯示或忽略它。 Adobe Primetime驗證也可使用此參數來提供可能導致錯誤的條件通知。 例如，「與提供者的授權服務通訊時發生網路錯誤。」

**觸發者：** `checkAuthorization(), getAuthorization()`

</br>

### 註銷 {#logout}

**說明：** 使用此方法來啟動註銷流程。 登出是一系列HTTP重新導向操作的結果，因為使用者需要從Adobe Primetime驗證伺服器以及MVPD的伺服器登出。 

| **API呼叫：啟動註銷流程** |
| --- |
| ```public void logout()``` |

**可用性：** v1.0+

**參數：** 無

**已觸發回呼：** 無

</br>

### getSelectedProvider {#getSelectedProvider}

**說明：** 使用此方法來確定當前選擇的提供程式。

| **API呼叫：決定目前選取的MVPD** |
| --- |
| ```public void getSelectedProvider()``` |

**可用性：** v1.0+

**參數：** 無

**已觸發回呼：** `selectedProvider()`

</br>

### selectedProvider {#selectedProvider}

**說明：** 由Access Enabler觸發的回調，該啟用程式將有關當前所選MVPD的資訊提供給應用程式。

| **回撥：目前選取之MVPD的相關資訊** |
| --- |
| ```public void selectedProvider(Mvpd mvpd)``` |

**可用性：** v1.0+

**參數：**

- *mvpd*:包含當前所選MVPD資訊的對象

**觸發者：** `getSelectedProvider()`

</br>

### getMetadata {#getMetadata}

**說明：** 使用此方法可檢索Access Enabler庫作為元資料公開的資訊。 應用程式可通過提供複合MetadataKey對象來訪問此資訊。

| **API呼叫：查詢AccessEnabler中的元資料** |
| --- |
| ```public void getMetadata(MetadataKey metadataKey)``` |

**可用性：** v1.0+

程式設計師有兩種可用的元資料：

- 靜態中繼資料（驗證Token TTL、授權Token TTL和裝置ID） 
- 使用者中繼資料（使用者專屬資訊，例如使用者ID和郵遞區號；在驗證和/或授權流程期間從MVPD傳遞至使用者裝置）

**參數：**

- *metadataKey*:封裝索引鍵和args變數的資料結構，其含義如下：
   - 如果鍵為 `METADATA_KEY_TTL_AUTHN` 然後進行查詢以取得驗證Token過期時間。
   - 如果鍵為 `METADATA_KEY_TTL_AUTHZ` 和args包含名稱為=的SerializableNameValuePair對象 `METADATA_ARG_RESOURCE_ID` 和值= `[resource_id]`，然後進行查詢以取得與指定資源相關聯的授權權杖的到期時間。
   - 如果鍵為 `METADATA_KEY_DEVICE_ID` 然後進行查詢以取得目前的裝置id。 請注意，此功能預設為停用，程式設計人員應聯絡Adobe，以取得啟用和費用的相關資訊。
   - 如果鍵為 `METADATA_KEY_USER_META` 和args包含名稱為=的SerializableNameValuePair對象 `METADATA_KEY_USER_META` 和值= `[metadata_name]`，則會為使用者中繼資料建立查詢。 可用用戶元資料類型的當前清單：
      - `zip`  — 郵遞區號
      - `householdID`  — 家庭標識符。 如果MVPD不支援子帳戶，則會與 `userID`.
      - `maxRating`  — 用戶的最高父母分級
      - `userID`  — 使用者識別碼。 如果MVPD支援子帳戶，且使用者不是主帳戶，
      - `channelID`  — 使用者有權檢視的管道清單

程式設計師可用的實際用戶元資料取決於MVPD提供的內容。  當新中繼資料可供使用並新增至Adobe Primetime驗證系統時，此清單將會進一步擴充。

**已觸發回呼：** [`setMetadataStatus()`](#setMetadaStatus)

**更多資訊：** [使用者中繼資料](#setmetadatastatus)

</br>

### setMetadataStatus {#setMetadaStatus}

**說明：** 由Access Enabler觸發的回調，該啟用程式通過 *getMetadata()* 呼叫。

| **回撥：元資料檢索請求的結果** |
| --- |
| ```public void setMetadataStatus(MetadataKey key, MetadataStatus result)``` |

**可用性：** v1.0+

**參數：**

- *key*:MetadataKey物件，包含要求中繼資料值的索引鍵和相關參數（如需參考實作，請參閱示範應用程式）。
- *結果*:包含所請求元資料的複合對象。 物件有下列欄位：
   - *simpleResult*:代表提出驗證TTL、授權TTL或裝置ID要求時中繼資料值的字串。 如果對用戶元資料提出請求，則此值為null。

   - *userMetadataResult*:包含JSON使用者中繼資料裝載的Java表示的物件。 例如：

      ```json
      {
      "street": "Main Avenue",
      "buildings": ["150", "320"]
      }
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

- *加密*:指定是否加密檢索的元資料的布爾值。 此參數只對使用者中繼資料請求有顯著意義，對於一律未加密接收的靜態中繼資料（例如驗證TTL）則沒有意義。 如果此參數設定為True，則由程式設計師通過使用白名單私鑰執行RSA解密來獲取未加密的用戶元資料值(用於在 [`setRequestor`](#setRequestor) 呼叫)。

**觸發者：** [`getMetadata()`](#getMetadata)

**更多資訊：** [使用者中繼資料](/help/authentication/user-metadata.md)

</br>

## getVersion {#getVersion}

**說明：** 使用此方法檢索AccessEnabler當前版本  

| **API呼叫：獲取AccessEnabler版本** |
| --- |
| ```public static String getVersion()``` |

## 追蹤事件 {#tracking}

Access Enabler會觸發與權限流程不一定相關的附加回調。 實作事件追蹤回呼函式，命名為 *sendTrackingData()* 是可選的，但它使應用程式能夠跟蹤特定事件並編譯統計資訊，如成功/失敗的身份驗證/授權嘗試次數。 以下是 *sendTrackingData()* 回呼：

### sendTrackingData {#sendTrackingData}

**說明：** 由Access Enabler向應用程式發出信號時觸發的回調，該信號會發生各種事件，如驗證/授權流的完成/失敗。 sendTrackingData()還報告了設備類型、Access Enabler客戶端類型和作業系統。

>[!WARNING]
>
> 裝置類型和作業系統是透過使用公用Java程式庫(http://java.net/projects/user-agent-utils)和使用者代理字串衍生而來。 請注意，此資訊僅作為將操作量度劃分為裝置類別的粗略方式提供，但該Adobe對錯誤的結果不負責。 請據此使用新功能。

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
   - `tvos`
   - `android`
   - `firetv`

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

以下是解譯 *資料* 陣列：

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

**觸發者：** `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`
