---
title: AmazonFireOS Native Client API參考
description: AmazonFireOS Native Client API參考
exl-id: 8ac9f976-fd6b-4b19-a80d-49bfe57134b5
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '3416'
ht-degree: 0%

---

# AmazonFireOS Native Client API參考 {#amazon-fireos-native-client-api-reference}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>

## 導言 {#intro}

本文檔詳細介紹了AmazonFireOS SDK為Adobe Primetime身份驗證而公開的方法和回調，該身份驗證受Adobe Primetime身份驗證支援。</span> 此處描述的方法和回調函式在AccessEnabler.h和EntitlementDelegate.h標頭檔中定義。

請參閱 <https://tve.zendesk.com/hc/en-us/articles/115005561623-fire-TV-Native-AccessEnabler-Library> 最新的AmazonFireOS AccessEnabler SDK。 

**注：** Adobe Primetime身份驗證團隊鼓勵您只使用Adobe Primetime身份驗證 *公共* API:

- 公共API可用 *經過充分測試* 所有支援的客戶端類型。 對於任何公共功能，我們確保每個客戶端類型都具有相關方法的相應版本。
- 公共API必須盡可能穩定，以支援向後相容性，並確保合作夥伴整合不會中斷。 但是， *非*-public API，我們保留在將來任何時刻更改其簽名的權利。 如果遇到當前公共Adobe Primetime身份驗證API調用的組合所無法支援的特定流，最好的方法是讓我們知道。 考慮到您的需要，我們可以修改公共API並提供一個穩定的解決方案。

## AmazonFireOS SDK API {#api}

- [getInstance](#getInstance)
- [setOptions](#fire_setOption)
- [setRequestor](#setRequestor)
- [setRequestorComplete](#setRequestorComplete)
- [checkAuthentication（檢查驗證）](#checkAuthN)
- [getAuthentication（獲取身份驗證）](#getAuthN)
- [displayProviderDialog](#displayProviderDialog)
- [setSelectedProvider](#setSelectedProvider)
- [導航至URL](#navigagteToUrl)
- [getAuthenticationToken](#getAuthNToken)
- [setAuthenticationStatus](#setAuthNStatus)
- [checkPreauthorizedResources](#checkPreauth)
- [預授權資源](#preauthResources)
- [checkAuthorization（檢查授權）](#checkAuthZ)
- [getAuthorization](#getAuthZ)
- [setToken](#setToken)
- [tokenRequestFailed](#tokenRequestFailed)
- [註銷](#logout)
- [getSelectedProvider](#getSelectedProvider)
- [選定提供程式](#selectedProvider)
- [getMetadata](#getMetadata)
- [setMetadataStatus](#setMetadaStatus)
- [getVersion](#getVersion)

</br>

### Factory.getInstance {#getInstance}

**描述：** 實例化Access Enabler對象。 每個應用程式實例應有一個Access Enabler實例。

| API調用：建構子 |
| --- |
| ```public static AccessEnabler getInstance(Context appContext, String softwareStatement, String redirectUrl)<br>        throws AccessEnablerException```<br><br> |
| ```public static AccessEnabler getInstance(Context appContext, String env_url, String softwareStatement, String redirectUrl) throws AccessEnablerException``` |

**可用性：** v3.0+


**參數：**

- *應用上下文*:AmazonFire OS應用程式上下文。
- 軟體語句
- 重定向URL:在FireOS中，將忽略參數值並將其設定為預設值：adobepass://android.app
- env_url:對於使用Adobe暫存環境進行測試，可將env\_url設定為「sp.auth-staging.adobe.com」

**已棄用：**

```java
    public static AccessEnabler getInstance(Context appContext)
        throws AccessEnablerException
```
 

### setRequestor {#setRequestor}

**描述：** 確定程式設計師的身份。 在向Adobe Primetime認證系統的Adobe註冊時，為每個程式設計師分配唯一的ID。 此設定應在應用程式的生命週期中僅執行一次。

伺服器響應包含MVPD清單以及附加到程式設計師身份的某些配置資訊。 伺服器響應由Access Enabler代碼在內部使用。 只有操作的狀態（即SUCCESS/FAIL）通過setRequestorComplete()回調顯示給您的應用程式。

如果 *URL* 未使用參數，生成的網路呼叫目標為預設服務提供商URL:Adobe版本/生產環境。

如果為 *URL* 參數，生成的網路調用針對中提供的所有URL *URL* 的下界。 所有配置請求都在單獨的線程中同時觸發。 編譯MVPD清單時，第一響應程式優先。 對於清單中的每個MVPD,Access Enabler會記住關聯服務提供商的URL。 所有後續權利請求都指向在配置階段與目標MVPD配對的與服務提供商關聯的URL。

| API調用：請求者配置 |
| --- |
| ```public void setRequestor(String requestorId)``` |


**可用性：**v 3.0+


| API調用：請求者配置 |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**可用性：** v3.0+


**參數：**

- *請求者ID*:與程式設計師關聯的唯一ID。 在首次向Adobe PrimetimeAdobe服務註冊時，將通過驗證分配的唯一ID傳遞到您的站點。
- *URL*:可選參數；預設情況下，使用Adobe服務提供程式(http://sp.auth.adobe.com/)。 此陣列允許您為Adobe提供的身份驗證和授權服務指定端點（可能會將不同的實例用於調試目的）。 您可以使用它指定多個Adobe Primetime身份驗證服務提供程式實例。 執行此操作時，MVPD清單由來自所有服務提供商的端點組成。 每個MVPD都與最快速的服務提供商相關聯；即，首先響應的提供程式，並且支援該MVPD。

**觸發的回調：** `setRequestorComplete()`

 

**已棄用：**

```
    public void setRequestor(String requestorId, String signedRequestorId)

    public void setRequestor(String requestorId, String signedRequestorId, ArrayList<String> urls)
```
 
</br>


### setRequestorComplete {#setRequestorComplete}

**描述：** 由Access Enabler觸發的回調通知您的應用程式配置階段已完成。 這是一個信號，表明應用可以開始發出權利請求。 在配置階段完成之前，應用程式不能發出任何權利請求。

| 回叫：請求者配置完成 |
| --- |
| ```public void setRequestorComplete(int status)``` |

**可用性：** v1.0+

**參數：**

- *狀態*:可以採用以下值之一：
   - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS`  — 配置階段已成功完成
   - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR`  — 配置階段失敗

**觸發者：** `setRequestor()`

</br> 


### setOptions {#fire_setOption}

**描述：** 配置全局SDK選項。 它接受 **映射\&lt;string string=&quot;&quot;>** 作為論據。 映射中的值將與SDK進行的每次網路調用一起傳遞到伺服器。

這些值將獨立於當前流（驗證/授權）傳遞給伺服器。 如果要更改值，可以在任何時間點調用此方法。

 

| API調用：setOptions |
| --- |
| ```public void setOptions(HashMap<String,String> options)``` |

**可用性：** v3.0+

**參數：**

- *選項*:地圖\&lt;string string=&quot;&quot;> 包含全局SDK選項。 當前可用的選項如下：
   - **應用程式配置檔案**  — 它可用於根據此值進行伺服器配置。
   - **ap\_vi** -Marketing Cloud訪客ID。 此值稍後可用於高級分析報告。
   - **設備\_資訊**  — 設備資訊（如所述） **傳遞設備資訊烹飪書**

</br>

### checkAuthentication（檢查驗證） {#checkAuthN}

**描述：** 檢查身份驗證狀態。 它通過在本地令牌儲存空間中搜索有效的身份驗證令牌來做到這一點。 調用此方法不執行網路調用。 應用程式使用它來查詢用戶的驗證狀態並相應地更新UI（即更新登錄/註銷UI）。 認證狀態通過 [*setAuthenticationStatus()*](#setAuthNStatus) 回叫。

如果MVPD支援「每請求者身份驗證」功能，則可以在設備上儲存多個身份驗證令牌。 

| API調用：檢查驗證狀態 |
| --- |
| ```public void checkAuthentication()``` |

**可用性：** v1.0+

**參數：** 無

**觸發的回調：** `setAuthenticationStatus()`

</br>

### getAuthentication（獲取身份驗證） {#getAuthN}

**描述：** 啟動完整身份驗證工作流。 首先檢查身份驗證狀態。 如果尚未進行身份驗證，則啟動身份驗證流狀態機：

- 如果上次驗證嘗試成功，則跳過MVPD選擇階段，WebView控制項將向用戶顯示MVPD的登錄頁。
- 如果上次身份驗證嘗試失敗或用戶明確註銷， [*displayProviderDialog()*](#displayProviderDialog) 觸發回調。 您的應用程式使用此回調來顯示MVPD選擇UI。 此外，還需要您的應用通過以下方式將用戶的MVPD選擇通知Access Enabler庫，以恢復身份驗證流： [setSelectedProvider()](#setSelectedProvider) 的雙曲餘切值。

如果MVPD支援「每個請求者的身份驗證」功能，則可以在設備上儲存多個身份驗證令牌（每個程式設計師一個）。

最後，通過該認證狀態將認證狀態傳送到該應用 *setAuthenticationStatus()* 回叫。

| API調用：啟動驗證流 |
| --- |
| ```public void getAuthentication()``` |

**可用性：** v1.0+

| API調用：啟動驗證流 |
| --- |
| ```public void getAuthentication(boolean forceAuthN, Map<String, Object> genericData)``` |

**可用性：** v1.0+

**參數：**

- *福爾森*:一個標誌，它指定是否應啟動驗證流，而不管用戶是否已經過驗證。
- *資料*:由要發送到付費電視通行服務的鍵值對組成的映射。 Adobe可以使用此資料來啟用將來的功能，而無需更改SDK。

**觸發的回調：** `setAuthenticationStatus(), displayProviderDialog(), sendTrackingData()`

</br>

### displayProviderDialog {#displayProviderDialog}

**說明** 由Access Enabler觸發的回調，用於通知應用程式需要實例化相應的UI元素，以允許用戶選擇所需的MVPD。 回調提供MVPD對象清單，其中包含有助於正確構建選擇UI面板的附加資訊（如指向MVPD徽標的URL、友好顯示名稱等）

一旦用戶選擇了所需的MVPD，則需要上層應用程式通過調用來恢複驗證流 *setSelectedProvider()* 並傳遞與用戶選擇對應的MVPD ID。\
 

| **回叫：顯示MVPD選擇UI** |
| --- |
| ```public void displayProviderDialog(ArrayList<Mvpd> mvpds)``` |

**可用性：** v1.0+

**參數**:

- *mvpd*:包含與MVPD相關資訊的MVPD對象清單，應用程式可以使用這些資訊構建MVPD選擇UI元素。

**觸發者：** `getAuthentication(), getAuthorization()`

</br>

### setSelectedProvider {#setSelectedProvider}

**描述：** 應用程式調用此方法以通知Access Enabler用戶的MVPD選擇。 過路時 *空* 作為參數，Access Enabler將當前MVPD重置為空值。

| **API調用：設定當前選定的提供程式** |
| --- |
| ```public void setSelectedProvider(String mvpdId)``` |


**可用性：**v 1.0+

**參數：** 無

**觸發的回調：** `setAuthenticationStatus(), sendTrackingData()`
</br>

### 導航至URL {#navigagteToUrl}

**描述：** 由Android SDK上的Access Enabler觸發的回調。 在AmazonFireOS SDK上應忽略它。

| **回叫：顯示MVPD登錄頁** |
| --- |
| ```public void navigateToUrl(String url)``` |

**可用性：** v1.0+

**參數：**

- *url*:指向MVPD登錄頁的URL

**觸發者：** `getAuthentication(), setSelectedProvider()`

</br>

### getAuthenticationToken {#getAuthNToken}

**描述：** 通過從後端伺服器請求驗證令牌來完成驗證流。 

| **API調用：檢索身份驗證令牌** |
| --- |
| ```public void getAuthenticationToken(String cookies)``` |

**可用性：** v1.0+

**參數：**

- *餅*:在目標域上設定的Cookie（有關參考實現，請參見SDK中的演示應用程式）。

**觸發的回調：** `setAuthenticationStatus(), sendTrackingData()`

</br>

### setAuthenticationStatus {#setAuthNStatus}

**描述：** 由Access Enabler觸發的回調，它通知應用程式驗證的狀態。 在許多地方，身份驗證流可能會因用戶交互或其他不可預見的情況（如網路連接問題等）而失敗。 此回調通知應用程式驗證的成功/失敗狀態，同時在需要時還提供有關失敗原因的附加資訊。

此回調還會在註銷流完成時發出信號。

| **回叫：報告驗證流的狀態** |
| --- |
| ```public void setAuthenticationStatus(int status, String errorCode)``` |

**可用性：** v1.0+

**參數：**

- *狀態*:可以採用以下值之一：
   - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS`  — 身份驗證流已成功完成
   - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR`  — 驗證流失敗
   - `AccessEnabler.ACCESS_ENABLER_STATUS_LOGOUT`  — 註銷
- *代碼*:呈現狀態的原因。 如果 *狀態* 是 `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS`，則 *代碼* 是空字串(即由 `AccessEnabler.USER_AUTHENTICATED` 常數)。 如果未通過身份驗證，此參數可以採用以下值之一：
   - `AccessEnabler.USER_NOT_AUTHENTICATED_ERROR`  — 用戶未經過身份驗證。 響應 *checkAuthentication()* 當本地令牌快取中沒有有效的驗證令牌時調用方法。
   - `AccessEnabler.PROVIDER_NOT_SELECTED_ERROR`  — 在上層應用程式通過後， AccessEnabler已重置身份驗證狀態機 *空* 至 `setSelectedProvider()` 中止驗證流。  用戶可能已取消驗證流（即按「後退」按鈕）。
   - `AccessEnabler.GENERIC_AUTHENTICATION_ERROR`  — 由於網路不可用或用戶明確取消了驗證流等原因，驗證流失敗。
   - `AccessEnabler.LOGOUT`  — 由於註銷操作，用戶未進行身份驗證。 

**觸發者：** `checkAuthentication(), getAuthentication(), checkAuthorization()`

</br>

### checkPreauthorizedResources {#checkPreauth}

**描述：** 應用程式使用此方法來確定用戶是否已獲得查看特定受保護資源的授權。 此方法的主要目的是檢索用於裝飾UI的資訊（例如，用鎖定和解鎖表徵圖指示訪問狀態）。

| **API調用：設定當前選定的提供程式** |
| --- |
| ```public void checkPreauthorizedResources(ArrayList<String> resources)``` |

**可用性：** v1.0+

**&lt;parameters: span=&quot;&quot; id=&quot;1&quot; translate=&quot;no&quot; /> 的 `resources` 參數是應檢查其授權的資源陣列。**&#x200B;清單中的每個元素都應是表示資源ID的字串。 資源ID受與 `getAuthorization()` 呼叫，即，它應是程式設計師與MVPD或媒體RSS片段之間所確定的商定值。

**觸發的回調：** `preauthorizedResources()`

</br>

### 預授權資源 {#preauthResources}

**描述：** 由checkPreauthorizedResources()觸發的回調。 提供已授權用戶查看的資源清單。

| **API調用：設定當前選定的提供程式** |
| --- |
| ```public void checkPreauthorizedResources(ArrayList<String> resources)``` |

**可用性：**v 1.0+

**參數：** 的 `resources` 參數是用戶已經有權查看的資源陣列。

**觸發者：** `checkPreauthorizedResources()`

<br>

### checkAuthorization（檢查授權） {#checkAuthZ}

**描述：** 此方法由應用程式用於檢查授權狀態。 首先檢查身份驗證狀態。 如果未通過身份驗證， *setTokenRequestFailed()* 回調被觸發，該方法退出。 如果用戶被認證，則它還觸發授權流。 請參閱 *getAuthorization()* 的雙曲餘切值。

| **API調用：檢查授權狀態** |
| --- |
| ```public void checkAuthorization(String resourceId)``` |

**可用性：** v1.0+

| **API調用：檢查授權狀態** |
| --- |
| ```public void checkAuthorization(String resourceId, Map<String, Object> genericData)``` |

**可用性：** v1.0+

**參數：**

- *資源ID*:用戶請求授權的資源的ID。
- *資料*:由要發送到付費電視通行服務的鍵值對組成的映射。 Adobe可以使用此資料來啟用將來的功能，而無需更改SDK。

**觸發的回調：** `tokenRequestFailed(), setToken(), sendTrackingData(), setAuthenticationStatus()`

</br>

### getAuthorization {#getAuthZ}

**描述：** 應用程式使用此方法啟動授權流。 如果用戶尚未經過身份驗證，它還會啟動身份驗證流。 如果用戶被驗證，Access Enabler將繼續發出授權令牌的請求（如果本地令牌快取中沒有有效的授權令牌）和短時間媒體令牌的請求。 一旦獲得了短媒體令牌，則認為授權流完成。 的 *setToken()* 觸發回調，並將短媒體令牌作為參數傳遞給應用程式。 如因任何原因授權失敗， *tokenRequestFailed()* 觸發回調，並提供錯誤代碼和詳細資訊。

| **API調用：啟動授權流** |
| --- |
| ```public void getAuthorization(String resourceId)``` |

**可用性：** v1.0+

| **API調用：啟動授權流** |
| --- |
| ```public void getAuthorization(String resourceId, Map<String, Object> genericData)``` |

**可用性：** v1.0+

**參數：**

- *資源ID*:用戶請求授權的資源的ID。
- *資料*:由要發送到付費電視通行服務的鍵值對組成的映射。 Adobe可以使用此資料來啟用將來的功能，而無需更改SDK。 

**觸發的回調：** `tokenRequestFailed(), setToken(), sendTrackingData()`

|  |  |
| --- | --- |
| ![](http://learn.adobe.com/wiki/images/icons/emoticons/warning.gif) | **觸發的其他回調**  <br>此方法還可以觸發以下回調（如果還啟動了驗證流）: _setAuthenticationStatus()_。 _displayProviderDialog()_ |

**注：請盡可能使用checkAuthorization()而不是getAuthorization()。 getAuthorization()方法將啟動完全身份驗證流（如果用戶未經身份驗證），這可能導致程式設計師方面的複雜實現。**

</br>

### setToken {#setToken}

**描述：** 由Access Enabler觸發的回調通知您的應用程式授權流已成功完成。 短壽命媒體令牌也作為參數傳遞。

| **回叫：授權流已成功完成** |
| --- |
| ```public void setToken(String token, String resourceId)``` |

**可用性：**v 1.0+

**參數：**

- *標籤*:短暫的媒體令牌
- *資源ID*:獲得授權的資源

**觸發者：** `checkAuthorization(), getAuthorization()`

<br>

### tokenRequestFailed {#tokenRequestFailed}

**描述：** 由Access Enabler觸發的回調通知上層應用程式授權流失敗。

| **回叫：授權流失敗** |
| --- |
| ```public void tokenRequestFailed(String resourceId, <br>        String errorCode, String errorDescription)``` |

**可用性：** v1.0+

**參數：**

- *資源ID*:獲得授權的資源
- *錯誤代碼*:與故障方案關聯的錯誤代碼。 可能的值：
   - `AccessEnabler.USER_NOT_AUTHORIZED_ERROR`  — 用戶無法授權給定資源
- *錯誤描述*:有關失敗方案的其他詳細資訊。 如果此描述性字串因任何原因不可用，則Adobe Primetime身份驗證將發送一個空字串>**(&quot;&quot;)**。  MVPD可以使用此字串傳遞自定義錯誤消息或與銷售相關的消息。 例如，如果拒絕訂閱者對資源的授權，則MVPD可以發送消息，如：「您目前在軟體包中沒有訪問此渠道的權限。 如果要升級軟體包，請按一下這裡。」 該消息通過Adobe Primetime身份驗證通過此回調傳遞給程式設計師，程式設計師可以選擇顯示或忽略它。 Adobe Primetime身份驗證還可以使用此參數來通知可能導致錯誤的情況。 例如，「與提供商的授權服務通信時發生網路錯誤。」

**觸發者：** `checkAuthorization(), getAuthorization()`

</br>

### 註銷 {#logout}

**描述：** 使用此方法啟動註銷流。 註銷是一系列HTTP重定向操作的結果，因為用戶需要從Adobe Primetime認證伺服器和MVPD伺服器註銷。 

| **API調用：啟動註銷流** |
| --- |
| ```public void logout()``` |

**可用性：** v1.0+

**參數：** 無

**觸發的回調：** 無

</br>

### getSelectedProvider {#getSelectedProvider}

**描述：** 使用此方法可確定當前選定的提供程式。

| **API調用：確定當前選定的MVPD** |
| --- |
| ```public void getSelectedProvider()``` |

**可用性：** v1.0+

**參數：** 無

**觸發的回調：** `selectedProvider()`

</br>

### 選定提供程式 {#selectedProvider}

**描述：** 由Access Enabler觸發的回調，該啟用程式將有關當前選定MVPD的資訊傳送到應用程式。

| **回叫：有關當前選定MVPD的資訊** |
| --- |
| ```public void selectedProvider(Mvpd mvpd)``` |

**可用性：** v1.0+

**參數：**

- *mvpd*:包含有關當前選定MVPD的資訊的對象

**觸發者：** `getSelectedProvider()`

</br>

### getMetadata {#getMetadata}

**描述：** 使用此方法可檢索Access Enabler庫以元資料形式公開的資訊。 應用程式可以通過提供複合MetadataKey對象來訪問此資訊。

| **API調用：查詢AccessEnabler以獲取元資料** |
| --- |
| ```public void getMetadata(MetadataKey metadataKey)``` |

**可用性：** v1.0+

程式設計師可使用兩種類型的元資料：

- 靜態元資料（驗證令牌TTL、授權令牌TTL和設備ID） 
- 用戶元資料（用戶特定資訊，如用戶ID和郵遞區號；在驗證和/或授權流程期間從MVPD傳遞到用戶設備）

**參數：**

- *元資料密鑰*:封裝鍵和args變數的資料結構，其含義如下：
   - 如果鍵為 `METADATA_KEY_TTL_AUTHN` 然後進行查詢以獲得認證令牌過期時間。
   - 如果鍵為 `METADATA_KEY_TTL_AUTHZ` args包含名為=的SerializableNameValuePair對象 `METADATA_ARG_RESOURCE_ID` 和值= `[resource_id]`，然後進行查詢以獲得與指定資源相關聯的授權令牌的到期時間。
   - 如果鍵為 `METADATA_KEY_DEVICE_ID` 然後進行查詢以獲取當前設備id。 請注意，此功能預設為禁用，程式設計師應與Adobe聯繫，以獲取有關啟用和費用的資訊。
   - 如果鍵為 `METADATA_KEY_USER_META` args包含名為=的SerializableNameValuePair對象 `METADATA_KEY_USER_META` 和值= `[metadata_name]`，然後對用戶元資料進行查詢。 可用用戶元資料類型的當前清單：
      - `zip`  — 郵遞區號
      - `householdID`  — 家庭標識。 如果MVPD不支援子帳戶，則與 `userID`。
      - `maxRating`  — 用戶的最高家長評級
      - `userID`  — 用戶標識符。 如果MVPD支援子帳戶，並且用戶不是主帳戶，
      - `channelID`  — 用戶有權查看的頻道清單

程式設計師可用的實際用戶元資料取決於MVPD提供的內容。  隨著新的元資料被提供並添加到Adobe Primetime認證系統中，該清單將進一步擴展。

**觸發的回調：** [`setMetadataStatus()`](#setMetadaStatus)

**更多資訊：** [用戶元資料](#setmetadatastatus)

</br>

### setMetadataStatus {#setMetadaStatus}

**描述：** 由Access Enabler觸發的回調，該啟用程式通過 *getMetadata()* 呼叫。

| **回叫：元資料檢索請求結果** |
| --- |
| ```public void setMetadataStatus(MetadataKey key, MetadataStatus result)``` |

**可用性：** v1.0+

**參數：**

- *鍵*:包含請求元資料值的鍵和關聯參數的MetadataKey對象（請參見演示應用程式以獲取參考實現）。
- *結果*:包含所請求元資料的複合對象。 對象具有以下欄位：
   - *簡單結果*:一個字串，它表示請求驗證TTL、授權TTL或設備ID時的元資料值。 如果為用戶元資料請求，則此值為空。

   - *userMetadataResult*:包含JSON用戶元資料負載的Java表示形式的對象。 例如：

      ```json
      {
      "street": "Main Avenue",
      "buildings": ["150", "320"]
      }
      ```

      將轉換為Java: 

      ```java
      Map("street" -> "Main Avenue", "buildings" -> List("150", "320")))
      ```

      **用戶元資料對象的實際結構與以下類似：**

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
 

對簡單元資料（驗證TTL、授權TTL或設備ID）發出請求時，此值為空。

- *加密*:用於指定是否加密檢索到的元資料的布爾值。 此參數僅對用戶元資料請求有重要意義，對始終未加密接收的靜態元資料（如驗證TTL）沒有意義。 如果此參數設定為True，則程式設計師需要使用白名單私鑰（用於在中籤名請求者ID的相同私鑰）執行RSA解密來獲取未加密的用戶元資料值 [`setRequestor`](#setRequestor) 呼叫)。

**觸發者：** [`getMetadata()`](#getMetadata)

**更多資訊：** [用戶元資料](/help/authentication/user-metadata.md)

</br>

## getVersion {#getVersion}

**描述：** 使用此方法檢索AccessEnabler當前版本  

| **API調用：獲取AccessEnabler版本** |
| --- |
| ```public static String getVersion()``` |

## 跟蹤事件 {#tracking}

Access Enabler會觸發與權利流不一定相關的附加回調。 實現名為的事件跟蹤回調函式 *sendTrackingData()* 是可選的，但它使應用程式能夠跟蹤特定事件並編譯統計資訊，如成功/失敗的身份驗證/授權嘗試次數。 下面是 *sendTrackingData()* 回調：

### sendTrackingData {#sendTrackingData}

**描述：** 由Access Enabler向應用程式發出的回調信號觸發了各種事件的發生，如驗證/授權流的完成/失敗。 sendTrackingData()還報告了設備類型、Access Enabler客戶端類型和作業系統。

>[!WARNING]
>
> 設備類型和作業系統是通過使用公共Java庫(http://java.net/projects/user-agent-utils)和用戶代理字串來派生的。 請注意，提供此資訊只是一種將操作度量細分為設備類別的粗略方法，但Adobe不能對不正確的結果負責。 請相應地使用新功能。

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

| 回叫：跟蹤事件 |
| --- |
| ```public void sendTrackingData(Event event, ArrayList<String> data)``` |

**可用性：** v1.0+

**參數：**

- *事件*:正在跟蹤的事件。 有三種可能的跟蹤事件類型：
   - **授權檢測：** 授權令牌請求返回時(事件類型為 `EVENT_AUTHZ_DETECTION`)
   - **驗證檢測：** 進行身份驗證檢查時(事件類型為 `EVENT_AUTHN_DETECTION`)
   - **mvpdSelection:** 當用戶在MVPD選擇表單中選擇MVPD時(事件類型為 `EVENT_MVPD_SELECTION`)
- *資料*:與報告的事件關聯的其他資料。 此資料以值清單的形式顯示。

以下是解釋中值的說明 *資料* 陣列：

- 對於事件類型 *`EVENT_AUTHN_DETECTION`:*
   - **0**  — 令牌請求是否成功(true/false)，如果上述是true:
   - **1** - MVPD ID字串
   - **2** - GUID（md5散列）
   - **3**  — 快取中已有的標籤(true/false)
   - **4**  — 設備類型
   - **5** - Access Enabler客戶端類型
   - **6**  — 作業系統類型

- 對於事件類型 `EVENT_AUTHZ_DETECTION`
   - **0**  — 令牌請求是否成功(true/false)，如果成功：
   - **1** - MVPD ID
   - **2** - GUID（md5散列）
   - **3**  — 快取中已有的標籤(true/false)
   - **4**  — 錯誤
   - **5**  — 詳細資訊
   - **6**  — 設備類型
   - **7** - Access Enabler客戶端類型
   - **8**  — 作業系統類型

- 對於事件類型 `EVENT_MVPD_SELECTION`
   - **0**  — 當前選定MVPD的ID
   - **1**  — 設備類型
   - **2** - Access Enabler客戶端類型
   - **3**  — 作業系統類型

**觸發者：** `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`
