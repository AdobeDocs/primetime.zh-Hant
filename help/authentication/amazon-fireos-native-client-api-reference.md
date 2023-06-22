---
title: Amazon FireOS Native Client API參考
description: Amazon FireOS Native Client API參考
exl-id: 8ac9f976-fd6b-4b19-a80d-49bfe57134b5
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '3416'
ht-degree: 0%

---

# Amazon FireOS Native Client API參考 {#amazon-fireos-native-client-api-reference}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

</br>

## 簡介 {#intro}

本檔案詳細說明Amazon FireOS SDK針對Adobe Primetime驗證(支援Adobe Primetime驗證)所公開的方法和回呼。</span> 此處說明的方法和回呼函式在AccessEnabler.h和EntitlementDelegate.h標頭檔案中定義。

請參閱 <https://tve.zendesk.com/hc/en-us/articles/115005561623-fire-TV-Native-AccessEnabler-Library> 以取得最新的Amazon FireOS AccessEnabler SDK。 

**注意：** Adobe Primetime驗證團隊鼓勵您僅使用Adobe Primetime驗證 *公共* API：

- 公用API可供使用 *經過完整測試* 在所有支援的使用者端型別上。 對於任何公用功能，我們確定每個使用者端型別都有相關方法的對應版本。
- 公開API必須儘可能穩定，以支援回溯相容性，並確保合作夥伴整合不會中斷。 但是，對於 *非* — 公用API，我們保留在未來任何時候變更其簽名的權利。 如果您遇到無法透過目前公用Adobe Primetime驗證API呼叫的組合支援的特定流程，最好的方法就是讓我們知道。 根據您的需求，我們可以修改公用API，並提供未來穩定的解決方案。

## Amazon FireOS SDK API {#api}

- [getInstance](#getInstance)
- [setOptions](#fire_setOption)
- [setRequestor](#setRequestor)
- [setRequestorComplete](#setRequestorComplete)
- [checkAuthentication](#checkAuthN)
- [getAuthentication](#getAuthN)
- [displayProviderDialog](#displayProviderDialog)
- [setselectedProvider](#setSelectedProvider)
- [navigateToUrl](#navigagteToUrl)
- [getAuthenticationToken](#getAuthNToken)
- [setAuthenticationStatus](#setAuthNStatus)
- [checkPreauthorizedResources](#checkPreauth)
- [preauthorizedResources](#preauthResources)
- [checkAuthorization](#checkAuthZ)
- [getAuthorization](#getAuthZ)
- [setToken](#setToken)
- [tokenRequestFailed](#tokenRequestFailed)
- [登出](#logout)
- [getselectedprovider](#getSelectedProvider)
- [selectedprovider](#selectedProvider)
- [getMetadata](#getMetadata)
- [setmetadataStatus](#setMetadaStatus)
- [getVersion](#getVersion)

</br>

### Factory.getInstance {#getInstance}

**說明：** 具現化Access Enabler物件。 每個應用程式執行個體應有一個存取啟用程式執行個體。

| API呼叫：建構函式 |
| --- |
| ```public static AccessEnabler getInstance(Context appContext, String softwareStatement, String redirectUrl)<br>        throws AccessEnablerException```<br><br> |
| ```public static AccessEnabler getInstance(Context appContext, String env_url, String softwareStatement, String redirectUrl) throws AccessEnablerException``` |

**可用性：** v3.0+


**引數：**

- *appContext*：Amazon Fire OS應用程式內容。
- 軟體陳述式
- redirectUrl ：若是FireOS，則會忽略引數值並設為預設值：adobepass://android.app
- env_url：若要使用Adobe測試環境進行測試，env\_url可設為&quot;sp.auth-staging.adobe.com&quot;

**已棄用：**

```java
    public static AccessEnabler getInstance(Context appContext)
        throws AccessEnablerException
```
 

### setRequestor {#setRequestor}

**說明：** 建立程式設計師的身分。 每位程式設計師在為Adobe Primetime驗證系統註冊Adobe後，都會獲得一個唯一的ID。 此設定只應在應用程式的生命週期中執行一次。

伺服器回應包含MVPD清單，以及附加至程式設計師身分的某些設定資訊。 伺服器回應由Access Enabler程式碼在內部使用。 只有作業的狀態（即SUCCESS/FAIL）會透過setRequestorComplete()回呼顯示給您的應用程式。

如果 *url* 不會使用引數，因此產生的網路呼叫會鎖定預設服務提供者URL：Adobe版本/生產環境。

如果提供的值用於 *url* 引數，則所產生的網路呼叫會鎖定中提供的所有URL *url* 引數。 所有設定請求都在不同的執行緒中同時觸發。 第一個回應者在編譯MVPD清單時優先。 對於清單中的每個MVPD，「存取啟用程式」會記住相關服務提供者的URL。 所有後續的軟體權利檔案要求都會導向至與設定階段期間與目標MVPD配對的服務提供者相關聯的URL。

| API呼叫：要求者設定 |
| --- |
| ```public void setRequestor(String requestorId)``` |


**可用性：**v 3.0+


| API呼叫：要求者設定 |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**可用性：** v3.0+


**引數：**

- *請求者ID*：與程式設計師相關聯的唯一ID。 當您首次向Adobe Primetime驗證服務註冊時，請將Adobe指派的唯一ID傳遞至您的網站。
- *url*：選用引數；預設會使用Adobe服務提供者(http://sp.auth.adobe.com/)。 此陣列可讓您為Adobe提供的驗證和授權服務指定端點（不同的執行個體可用於偵錯）。 您可以使用此選項來指定多個Adobe Primetime驗證服務提供者執行個體。 如此一來，MVPD清單就會由所有服務提供者的端點組成。 每個MVPD都與最快的服務提供者相關聯，也就是首先回應並支援該MVPD的提供者。

**觸發的回呼：** `setRequestorComplete()`

 

**已棄用：**

```
    public void setRequestor(String requestorId, String signedRequestorId)

    public void setRequestor(String requestorId, String signedRequestorId, ArrayList<String> urls)
```
 
</br>


### setRequestorComplete {#setRequestorComplete}

**說明：** 由Access Enabler觸發的回呼，通知您的應用程式設定階段已完成。 這是應用程式可以開始發出權益要求的訊號。 在設定階段完成之前，應用程式無法發出任何權益請求。

| 回呼：要求者設定完成 |
| --- |
| ```public void setRequestorComplete(int status)``` |

**可用性：** v1.0+

**引數：**

- *狀態*：可以取下列其中一個值：
   - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS`  — 設定階段已成功完成
   - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR`  — 設定階段失敗

**觸發者：** `setRequestor()`

</br> 


### setOptions {#fire_setOption}

**說明：** 設定全域SDK選項。 它接受 **對應\&lt;string string=&quot;&quot;>** 作為引數。 對應中的值會連同SDK發出的每個網路呼叫一起傳遞至伺服器。

這些值將會傳遞至伺服器，不受目前流量（驗證/授權）影響。 如果您想要變更值，可以隨時呼叫此方法。

 

| API呼叫： setOptions |
| --- |
| ```public void setOptions(HashMap<String,String> options)``` |

**可用性：** v3.0+

**引數：**

- *選項*：地圖\&lt;string string=&quot;&quot;> 包含全域SDK選項。 目前提供下列選項：
   - **applicationProfile**  — 可用於根據此值進行伺服器設定。
   - **ap\_vi** - visitorIDMarketing Cloud。 此值稍後可用於進階分析報表。
   - **device\_info**  — 裝置資訊，如所述 **傳遞裝置資訊逐步指南**

</br>

### checkAuthentication {#checkAuthN}

**說明：** 檢查驗證狀態。 其做法是在本機權杖儲存空間中搜尋有效的驗證權杖。 呼叫此方法不會執行任何網路呼叫。 應用程式會使用它來查詢使用者的驗證狀態並相應地更新UI （即更新登入/登出UI）。 驗證狀態會透過 [*setAuthenticationStatus()*](#setAuthNStatus) callback。

如果MVPD支援「每位請求者的驗證」功能，則多個驗證Token可以儲存在裝置上。 

| API呼叫：檢查驗證狀態 |
| --- |
| ```public void checkAuthentication()``` |

**可用性：** v1.0+

**引數：** 無

**觸發的回呼：** `setAuthenticationStatus()`

</br>

### getAuthentication {#getAuthN}

**說明：** 啟動完整驗證工作流程。 首先檢查驗證狀態。 如果尚未驗證，則會啟動驗證流程狀態機器：

- 如果上次驗證嘗試成功，則會略過MVPD選取階段，而WebView控制項會向使用者顯示MVPD的登入頁面。
- 如果上次驗證嘗試不成功，或使用者明確登出， [*displayProviderDialog()*](#displayProviderDialog) 已觸發回呼。 您的應用程式使用此回呼來顯示MVPD選擇UI。 此外，您的應用程式也需要透過以下方式向Access Enabler程式庫通知使用者的MVPD選擇，以繼續驗證流程： [setSelectedProvider()](#setSelectedProvider) 方法。

如果MVPD支援「每位請求者的驗證」功能，則多個驗證Token可以儲存在裝置上（每位程式設計師一個）。

最後，驗證狀態會透過 *setAuthenticationStatus()* callback。

| API呼叫：起始驗證流程 |
| --- |
| ```public void getAuthentication()``` |

**可用性：** v1.0+

| API呼叫：起始驗證流程 |
| --- |
| ```public void getAuthentication(boolean forceAuthN, Map<String, Object> genericData)``` |

**可用性：** v1.0+

**引數：**

- *forceAuthn*：指定是否應啟動驗證流程的旗標，無論使用者是否已驗證。
- *資料*：包含要傳送至Pay-TV Pass服務的機碼值組的對應。 Adobe可使用此資料來啟用未來的功能，而不需變更SDK。

**觸發的回呼：** `setAuthenticationStatus(), displayProviderDialog(), sendTrackingData()`

</br>

### displayProviderDialog {#displayProviderDialog}

**說明** 由Access Enabler觸發的回呼，通知應用程式需要具現化適當的UI元素，以允許使用者選取所需的MVPD。 回呼會提供MVPD物件清單，內含其他資訊，可協助您正確建立選取專案UI面板（例如指向MVPD標誌的URL、好記的顯示名稱等）

一旦使用者選取了所需的MVPD，上層應用程式就需呼叫，以恢複驗證流程 *setSelectedProvider()* ，並向其傳遞與使用者選取專案相對應的MVPD ID。\
 

| **回呼：顯示MVPD選擇UI** |
| --- |
| ```public void displayProviderDialog(ArrayList<Mvpd> mvpds)``` |

**可用性：** v1.0+

**引數**：

- *mvpds*：包含MVPD相關資訊的MVPD物件清單，應用程式可將其用於建立MVPD選取UI元素。

**觸發者：** `getAuthentication(), getAuthorization()`

</br>

### setselectedProvider {#setSelectedProvider}

**說明：** 您的應用程式會呼叫此方法，通知Access Enabler使用者的MVPD選擇。 傳遞時 *null* Access Enabler會將目前的MVPD重設為null值，作為引數。

| **API呼叫：設定目前選取的提供者** |
| --- |
| ```public void setSelectedProvider(String mvpdId)``` |


**可用性：**v 1.0+

**引數：** 無

**觸發的回呼：** `setAuthenticationStatus(), sendTrackingData()`
</br>

### navigateToUrl {#navigagteToUrl}

**說明：** Android SDK上的Access Enabler觸發的回呼。 在Amazon FireOS SDK上應忽略它。

| **回呼：顯示MVPD登入頁面** |
| --- |
| ```public void navigateToUrl(String url)``` |

**可用性：** v1.0+

**引數：**

- *url*：指向MVPD登入頁面的URL

**觸發者：** `getAuthentication(), setSelectedProvider()`

</br>

### getAuthenticationToken {#getAuthNToken}

**說明：** 從後端伺服器要求驗證Token，以完成驗證流程。 

| **API呼叫：擷取驗證Token** |
| --- |
| ```public void getAuthenticationToken(String cookies)``` |

**可用性：** v1.0+

**引數：**

- *Cookie*：在目標網域上設定的Cookie （請參閱SDK中的示範應用程式以瞭解參考實作）。

**觸發的回呼：** `setAuthenticationStatus(), sendTrackingData()`

</br>

### setAuthenticationStatus {#setAuthNStatus}

**說明：** 由Access Enabler觸發的回呼，通知應用程式驗證狀態。 在許多地方，驗證流程可能會因為使用者的互動或其他未預見的情況（例如網路連線問題等）而失敗。 此回呼會通知應用程式驗證的成功/失敗狀態，同時也會在需要時提供有關失敗原因的其他資訊。

此回呼也會在登出流程完成時發出訊號。

| **回呼：報告驗證流程的狀態** |
| --- |
| ```public void setAuthenticationStatus(int status, String errorCode)``` |

**可用性：** v1.0+

**引數：**

- *狀態*：可以取下列其中一個值：
   - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS`  — 驗證流程已成功完成
   - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR`  — 驗證流程失敗
   - `AccessEnabler.ACCESS_ENABLER_STATUS_LOGOUT`  — 登出
- *程式碼*：顯示狀態的原因。 若 *狀態* 是 `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS`，則 *程式碼* 為空字串(即由 `AccessEnabler.USER_AUTHENTICATED` 常數)。 如果未驗證，此引數可以有下列其中一個值：
   - `AccessEnabler.USER_NOT_AUTHENTICATED_ERROR`  — 未驗證使用者。 回應 *checkAuthentication()* 當本機權杖快取中沒有有效的驗證權杖時，方法呼叫。
   - `AccessEnabler.PROVIDER_NOT_SELECTED_ERROR` - AccessEnabler在上層應用程式通過後，已重設驗證狀態機器 *null* 至 `setSelectedProvider()` 以中止驗證流程。  使用者可能已取消驗證流程（即按下「上一步」按鈕）。
   - `AccessEnabler.GENERIC_AUTHENTICATION_ERROR`  — 驗證流程因網路無法使用或使用者明確取消驗證流程等原因而失敗。
   - `AccessEnabler.LOGOUT`  — 由於登出動作，使用者未獲得驗證。 

**觸發者：** `checkAuthentication(), getAuthentication(), checkAuthorization()`

</br>

### checkPreauthorizedResources {#checkPreauth}

**說明：** 應用程式會使用此方法來判斷使用者是否已獲授權檢視特定的受保護資源。 此方法的主要用途是擷取資訊以用於裝飾UI （例如，使用鎖定和解鎖圖示來指示存取狀態）。

| **API呼叫：設定目前選取的提供者** |
| --- |
| ```public void checkPreauthorizedResources(ArrayList<String> resources)``` |

**可用性：** v1.0+

**&lt;parameters: span=&quot;&quot; id=&quot;1&quot; translate=&quot;no&quot; /> 此 `resources` parameter是應檢查其授權的資源陣列。**&#x200B;清單中的每個元素都應是代表資源ID的字串。 資源ID的限制與 `getAuthorization()` 呼叫，也就是說，它應該是程式設計師和MVPD或媒體RSS片段之間建立的議定值。

**已觸發回呼：** `preauthorizedResources()`

</br>

### preauthorizedResources {#preauthResources}

**說明：** checkPreauthorizedResources()觸發的回呼。 提供使用者已獲授權檢視的資源清單。

| **API呼叫：設定目前選取的提供者** |
| --- |
| ```public void checkPreauthorizedResources(ArrayList<String> resources)``` |

**可用性：**v 1.0+

**引數：** 此 `resources` parameter是使用者已被授權檢視的資源陣列。

**觸發者：** `checkPreauthorizedResources()`

<br>

### checkAuthorization {#checkAuthZ}

**說明：** 應用程式使用此方法來檢查授權狀態。 首先檢查驗證狀態。 如果未驗證， *setTokenRequestFailed()* 會觸發callback，而方法會結束。 如果使用者已通過驗證，它也會觸發授權流程。 欲知詳情，請參閱 *getAuthorization()* 方法。

| **API呼叫：檢查授權狀態** |
| --- |
| ```public void checkAuthorization(String resourceId)``` |

**可用性：** v1.0+

| **API呼叫：檢查授權狀態** |
| --- |
| ```public void checkAuthorization(String resourceId, Map<String, Object> genericData)``` |

**可用性：** v1.0+

**引數：**

- *resourceId*：使用者要求授權的資源ID。
- *資料*：包含要傳送至Pay-TV Pass服務的機碼值組的對應。 Adobe可使用此資料來啟用未來的功能，而不需變更SDK。

**觸發的回呼：** `tokenRequestFailed(), setToken(), sendTrackingData(), setAuthenticationStatus()`

</br>

### getAuthorization {#getAuthZ}

**說明：** 應用程式會使用此方法來起始授權流程。 如果使用者尚未驗證，它也會啟動驗證流程。 如果使用者通過驗證，Access Enabler會繼續發出授權權杖（如果本機權杖快取中不存在有效的授權權杖）和短期媒體權杖的請求。 取得短媒體權杖後，授權流程即視為完成。 此 *setToken()* 系統會觸發callback，並將簡短媒體權杖作為引數傳送至應用程式。 如果由於任何原因，授權失敗， *tokenRequestFailed()* 會觸發回呼，並提供錯誤碼和詳細資料。

| **API呼叫：起始授權流程** |
| --- |
| ```public void getAuthorization(String resourceId)``` |

**可用性：** v1.0+

| **API呼叫：起始授權流程** |
| --- |
| ```public void getAuthorization(String resourceId, Map<String, Object> genericData)``` |

**可用性：** v1.0+

**引數：**

- *resourceId*：使用者要求授權的資源ID。
- *資料*：包含要傳送至Pay-TV Pass服務的機碼值組的對應。 Adobe可使用此資料來啟用未來的功能，而不需變更SDK。 

**觸發的回呼：** `tokenRequestFailed(), setToken(), sendTrackingData()`

|  |  |
| --- | --- |
| ![](http://learn.adobe.com/wiki/images/icons/emoticons/warning.gif) | **已觸發其他回呼**  <br>此方法也可以觸發下列回呼（如果同時啟動驗證流程）： _setAuthenticationStatus()_， _displayProviderDialog()_ |

**注意：請儘可能使用checkAuthorization()而非getAuthorization()。 getAuthorization()方法將啟動完整的驗證流程（如果使用者未驗證），這可能會導致程式設計人員方面的複雜實施。**

</br>

### setToken {#setToken}

**說明：** 由Access Enabler觸發的回呼，通知您的應用程式授權流程已成功完成。 短期媒體代號也會作為引數傳遞。

| **回呼：授權流程已成功完成** |
| --- |
| ```public void setToken(String token, String resourceId)``` |

**可用性：**v 1.0+

**引數：**

- *token*：短期媒體權杖
- *resourceId*：取得授權的資源

**觸發者：** `checkAuthorization(), getAuthorization()`

<br>

### tokenRequestFailed {#tokenRequestFailed}

**說明：** 由Access Enabler觸發的回呼，通知上層應用程式授權流程失敗。

| **回呼：授權流程失敗** |
| --- |
| ```public void tokenRequestFailed(String resourceId, <br>        String errorCode, String errorDescription)``` |

**可用性：** v1.0+

**引數：**

- *resourceId*：取得授權的資源
- *errorCode*：與失敗案例相關聯的錯誤代碼。 可能的值：
   - `AccessEnabler.USER_NOT_AUTHORIZED_ERROR`  — 使用者無法授權指定的資源
- *errorDescription*：有關失敗情況的其他詳細資訊。 如果此描述性字串因任何原因而無法使用，Adobe Primetime驗證會傳送空白字串>**(「」)**.  MVPD可使用此字串來傳遞自訂錯誤訊息或銷售相關訊息。 例如，如果拒絕訂閱者對資源的授權，MVPD會傳送訊息，例如：「您目前無法在封裝中存取此通道。 如果您想要升級套件，請按這裡。」 Adobe Primetime驗證會透過此回呼將訊息傳遞給程式設計師，程式設計師可以選擇顯示或忽略訊息。 Adobe Primetime驗證也可以使用此引數來提供可能導致錯誤的狀況通知。 例如，「與提供者的授權服務通訊時發生網路錯誤。」

**觸發者：** `checkAuthorization(), getAuthorization()`

</br>

### 登出 {#logout}

**說明：** 使用此方法可起始登出流程。 登出是一系列HTTP重新導向作業的結果，因為使用者需要同時從Adobe Primetime驗證伺服器和MVPD的伺服器登出。 

| **API呼叫：起始登出流程** |
| --- |
| ```public void logout()``` |

**可用性：** v1.0+

**引數：** 無

**觸發的回呼：** 無

</br>

### getselectedprovider {#getSelectedProvider}

**說明：** 使用此方法可判斷目前選取的提供者。

| **API呼叫：判斷目前選取的MVPD** |
| --- |
| ```public void getSelectedProvider()``` |

**可用性：** v1.0+

**引數：** 無

**觸發的回呼：** `selectedProvider()`

</br>

### selectedprovider {#selectedProvider}

**說明：** 由Access Enabler觸發的回呼，將目前所選MVPD的相關資訊傳送給應用程式。

| **回呼：目前所選MVPD的相關資訊** |
| --- |
| ```public void selectedProvider(Mvpd mvpd)``` |

**可用性：** v1.0+

**引數：**

- *mvpd*：包含目前所選MVPD相關資訊的物件

**觸發者：** `getSelectedProvider()`

</br>

### getMetadata {#getMetadata}

**說明：** 使用此方法可擷取Access Enabler程式庫公開為中繼資料的資訊。 應用程式可提供複合MetadataKey物件，以存取此資訊。

| **API呼叫：查詢AccessEnabler以取得中繼資料** |
| --- |
| ```public void getMetadata(MetadataKey metadataKey)``` |

**可用性：** v1.0+

程式設計師可以使用兩種中繼資料型別：

- 靜態中繼資料（驗證權杖TTL、授權權杖TTL和裝置ID） 
- 使用者中繼資料（使用者特定資訊，例如使用者ID和郵遞區號；在驗證和/或授權流程期間，從MVPD傳遞至使用者的裝置）

**引數：**

- *metadataKey*：封裝索引鍵和args變數的資料結構，其含義如下：
   - 如果索引鍵為 `METADATA_KEY_TTL_AUTHN` 然後進行查詢以取得驗證權杖到期時間。
   - 如果索引鍵為 `METADATA_KEY_TTL_AUTHZ` 和引數包含名稱為=的SerializableNameValuePair物件 `METADATA_ARG_RESOURCE_ID` 和值= `[resource_id]`，則會執行查詢以獲取與指定資源相關聯的授權權杖的到期時間。
   - 如果索引鍵為 `METADATA_KEY_DEVICE_ID` 接著會進行查詢以取得目前的裝置id。 請注意，此功能預設為停用，程式設計師應聯絡Adobe以取得有關啟用和費用的資訊。
   - 如果索引鍵為 `METADATA_KEY_USER_META` 和引數包含名稱為=的SerializableNameValuePair物件 `METADATA_KEY_USER_META` 和值= `[metadata_name]`，則會針對使用者中繼資料進行查詢。 目前可用的使用者中繼資料型別清單：
      - `zip`  — 郵遞區號
      - `householdID`  — 家庭識別碼。 如果MVPD不支援附屬帳戶，這將會與 `userID`.
      - `maxRating`  — 使用者的父母最高分級
      - `userID`  — 使用者識別碼。 如果MVPD支援附屬帳戶，且使用者不是主要帳戶，
      - `channelID`  — 使用者有權檢視的管道清單

程式設計師可用的實際使用者中繼資料取決於MVPD提供的內容。  此清單將隨著新的中繼資料可用並新增至Adobe Primetime驗證系統而進一步擴充。

**觸發的回呼：** [`setMetadataStatus()`](#setMetadaStatus)

**更多資訊：** [使用者中繼資料](#setmetadatastatus)

</br>

### setmetadataStatus {#setMetadaStatus}

**說明：** 由Access Enabler觸發的回呼，透過傳遞請求的中繼資料 *getMetadata()* 呼叫。

| **回撥：中繼資料擷取請求的結果** |
| --- |
| ```public void setMetadataStatus(MetadataKey key, MetadataStatus result)``` |

**可用性：** v1.0+

**引數：**

- *金鑰*：此MetadataKey物件包含要求中繼資料值的索引鍵和相關聯的引數（如需參考實作，請參閱示範應用程式）。
- *結果*：包含請求中繼資料的複合物件。 物件有以下欄位：
   - *simpleResult*：代表要求驗證TTL、授權TTL或裝置ID時中繼資料值的字串。 如果對使用者中繼資料提出要求，則此值為null。

   - *userMetadataResult*：一個物件，包含JSON使用者中繼資料裝載的Java表示法。 例如：

      ```json
      {
      "street": "Main Avenue",
      "buildings": ["150", "320"]
      }
      ```

      會翻譯成Java，如下所示： 

      ```java
      Map("street" -> "Main Avenue", "buildings" -> List("150", "320")))
      ```

      **使用者中繼資料物件的實際結構類似於以下內容：**

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
 

請求簡單中繼資料（驗證TTL、授權TTL或裝置ID）時，此值為空。

- *已加密*：指定是否加密擷取的中繼資料的布林值。 此引數僅對使用者中繼資料請求有意義，對始終未加密接收的靜態中繼資料（例如驗證TTL）沒有意義。 如果此引數設為True，則由程式設計師決定是否使用白名單私密金鑰（在中用於簽署請求者ID的相同私密金鑰）執行RSA解密，以取得未加密的使用者中繼資料值。 [`setRequestor`](#setRequestor) 呼叫)。

**觸發者：** [`getMetadata()`](#getMetadata)

**更多資訊：** [使用者中繼資料](/help/authentication/user-metadata.md)

</br>

## getVersion {#getVersion}

**說明：** 使用此方法擷取AccessEnabler目前版本  

| **API呼叫：取得AccessEnabler版本** |
| --- |
| ```public static String getVersion()``` |

## 追蹤事件 {#tracking}

Access Enabler會觸發其他回呼，而此回呼不一定與權益流程相關。 實作事件追蹤回呼函式命名為 *sendTrackingData()* 是選用專案，但此專案可讓應用程式追蹤特定事件並編譯統計資料，例如成功/失敗的驗證/授權嘗試次數。 以下是 *sendTrackingData()* 回撥：

### sendTrackingData {#sendTrackingData}

**說明：** Access Enabler所觸發的回呼，會向應用程式發出各種事件的發生訊號，例如驗證/授權流程完成/失敗。 sendTrackingData()也會報告裝置型別、Access Enabler使用者端型別和作業系統。

>[!WARNING]
>
> 裝置型別和作業系統衍生自使用公用Java程式庫(http://java.net/projects/user-agent-utils)和使用者代理程式字串。 請注意，此資訊僅以粗略的方式提供，以將運作量度劃分為裝置類別，但該Adobe對錯誤結果概不負責。 請據以使用新功能。

- 裝置型別的可能值：
   - `computer`
   - `tablet`
   - `mobile`
   - `gameconsole`
   - `unknown`

- Access Enabler使用者端型別的可能值：
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

**引數：**

- *事件*：正在追蹤的事件。 追蹤事件型別共有三種：
   - **authorizationDetection：** 每當授權權杖請求傳回時(事件型別為 `EVENT_AUTHZ_DETECTION`)
   - **authenticationdetection：** 每當驗證檢查發生時(事件型別為 `EVENT_AUTHN_DETECTION`)
   - **mvpdSelection：** 當使用者在MVPD選擇表單中選取MVPD時(事件型別為 `EVENT_MVPD_SELECTION`)
- *資料*：與已報告事件相關聯的其他資料。 此資料會以值清單的形式呈現。

以下為解譯「 」中值的指示 *資料* 陣列：

- 對於事件型別 *`EVENT_AUTHN_DETECTION`：*
   - **0**  — 權杖要求是否成功(true/false)，如果上述為true：
   - **1** - MVPD ID字串
   - **2** - GUID （md5雜湊）
   - **3**  — 權杖已存在於快取中(true/false)
   - **4**  — 裝置型別
   - **5**  — 存取啟用程式使用者端型別
   - **6**  — 作業系統型別

- 對於事件型別 `EVENT_AUTHZ_DETECTION`
   - **0**  — 權杖要求是否成功(true/false)，如果成功：
   - **1** - MVPD ID
   - **2** - GUID （md5雜湊）
   - **3**  — 權杖已存在於快取中(true/false)
   - **4**  — 錯誤
   - **5**  — 詳細資料
   - **6**  — 裝置型別
   - **7**  — 存取啟用程式使用者端型別
   - **8**  — 作業系統型別

- 對於事件型別 `EVENT_MVPD_SELECTION`
   - **0**  — 目前所選MVPD的ID
   - **1**  — 裝置型別
   - **2**  — 存取啟用程式使用者端型別
   - **3**  — 作業系統型別

**觸發者：** `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`
