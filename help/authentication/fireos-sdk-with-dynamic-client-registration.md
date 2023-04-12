---
title: Amazon FireOS SDK與Dynamic Client註冊
description: Amazon FireOS SDK與Dynamic Client註冊
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 0%

---


# Amazon FireOS SDK與Dynamic Client註冊 {#amazon-fireos-sdk-with-dynamic-client-registration}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

</br>

## <span id=""></span>簡介 {#Intro}

FireTV適用的FireOS AccessEnabler SDK已修改為啟用驗證，而不使用工作階段Cookie。 隨著越來越多的瀏覽器限制對Cookie的存取，需要另一種方法來允許驗證。

**FireOS SDK 3.0.4** 以取代目前應用程式註冊機制，此機制會根據簽署的請求者ID和工作階段cookie驗證 [動態客戶端註冊](/help/authentication/dynamic-client-registration.md).
 

## API變更 {#API}

### Factory.getInstance

**說明：** 實例化Access Enabler對象。 每個應用程式實例應有一個Access Enabler實例。

| API呼叫：建構函式 |
| --- |
| 公用靜態AccessEnabler getInstance(ContextAppContext, String softwareStatement, String redirectUrl)<br>        擲回AccessEnablerException |

**可用性：** v3.0+

**參數：**

- *appContext*:Android應用程式內容
- *softwareStatement*:從TVE儀表板或 *null* 如果在strings.xml中設定&quot;software\_statement&quot;
- *redirectUrl* :若為FireTV實作，此參數應為null。 此屬性上的任何設定都將被忽略。 

**附註**

- 無效的softwareStatement會導致應用程式不初始化AccessEnabler或註冊應用程式以進行Adobe Pass驗證和授權
- FireTV的redirectUrl參數由SDK設定為adobepass://android.app as驗證由唯一的AccessEnabler實例處理。

### setRequestor

**說明：** 建立管道的身分。 向Adobe Primetime驗證系統的Adobe註冊時，每個管道都會獲派唯一ID。 處理SSO和遠端代號時，當應用程式在背景時，驗證狀態可能會改變，當應用程式進入前景時，可再次呼叫setRequestor以與系統狀態同步（如果啟用SSO，則擷取遠端代號，若同時發生登出，則刪除本機代號）。

伺服器回應包含MVPD清單，以及附加至通道身分的部分設定資訊。 伺服器響應由Access Enabler代碼在內部使用。 只會透過setRequestorComplete()回呼向您的應用程式顯示操作狀態（即SUCCESS/FAIL）。

若 *url* 參數，則產生的網路呼叫會鎖定預設服務提供者URL:Adobe發行生產環境。

如果為 *url* 參數，產生的網路呼叫會鎖定 *url* 參數。 所有配置請求都在單獨的線程中同時觸發。 編譯MVPD清單時，第一回應者優先。 對於清單中的每個MVPD,Access Enabler會記住相關服務提供商的URL。 所有後續的權限請求都會導向至在設定階段與目標MVPD成對之服務提供者相關聯的URL。

| API呼叫：請求者設定 |
| --- |
| public void setRequestor(String requestorId) |

**可用性：** v3.0+

| API呼叫：請求者設定 |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**可用性：** v3.0+

**參數：**

- *requestorID*:與管道相關聯的唯一ID。 在您首次向Adobe Primetime驗證服務註冊時，將Adobe指派的唯一ID傳遞至您的網站。
- *url*:選用參數；依預設，會使用Adobe服務提供者(http://sp.auth.adobe.com/)。 此陣列可讓您為Adobe提供的驗證和授權服務指定端點（可能會使用不同的執行個體進行除錯）。 您可以使用此ID來指定多個Adobe Primetime驗證服務提供者例項。 執行此操作時，MVPD清單由來自所有服務提供者的端點組成。 每個MVPD都與最快的服務提供商相關聯；即第一個回應且支援該MVPD的提供者。

已棄用：

- *signedRequestorID*:以您的私密金鑰進行數位簽署的要求者ID副本。 <!--For more details, see [Registering Native Clients](http://tve.helpdocsonline.com/registering-native-clients)-->.

**已觸發回呼：** `setRequestorComplete()`

</br>

### 註銷

**說明：** 使用此方法來啟動註銷流程。 登出是一系列HTTP重新導向操作的結果，因為使用者需要從Adobe Primetime驗證伺服器以及MVPD的伺服器登出。 因此，此流程將開啟ChromeCustomTab視窗以執行登出。

| API呼叫：啟動註銷流程 |
| --- |
| 公共撤消註銷() |

**可用性：** v3.0+

**參數：** 無

**已觸發回呼：** `setAuthenticationStatus()`

## 程式設計師實施流程 {#Progr}

### **1. 註冊應用程式** 

1. 從Adobe Pass（TVE儀表板）獲取software\_statement
1. 有兩個選項可將這些值傳遞至Adobe Pass SDK :
   - 在strings.xml add中： 

      ```
      <string name>"software\_statement">[softwarestatement value]</string>
      ```

   - 調用AccessEnabler.getInstance(appContext,softwareStatement, null)

 

### **2. 配置應用程式**

- a. setRequestor(requestor\_id) 

   SDK將執行下列操作： 

   - 註冊申請：使用 **軟體\_語句**，則SDK會取得 **client\_id, client\_secret, client\_id\_issued\_at, redirect\_uris, grant\_types**. 此資訊將儲存在應用程式的內部儲存中。
   - 取得 **access\_token** 使用client\_id、client\_secret和grant\_type=&quot;client\_credentials&quot; 。 SDK對Adobe Pass伺服器發出的每次呼叫都會使用此access\_token。

| 代號錯誤回應： |  |  |
|--- | --- | --- |
| HTTP 400(Bad Request) | {&quot;error&quot;:&quot;無效\_request&quot;} | 請求缺少必需的參數，包括不受支援的參數值（授權類型除外），重複參數，包括多個憑據，使用多個機制來驗證客戶端，或者其它錯誤。 |
| HTTP 400(Bad Request) | {&quot;error&quot;:&quot;無效\_client&quot;} | 客戶端身份驗證失敗，因為客戶端未知。 SDK *必須* 向授權伺服器重新註冊。 |
| HTTP 400(Bad Request) | {&quot;error&quot;:&quot;unauthorized\_client&quot;} | 已驗證的客戶端無權使用此授權授權類型。 |

- 如果MVPD需要被動驗證，則WebView會開啟以使用該MVPD執行被動，並會在完成時關閉

- b. checkAuthentication()

   - *true* :前往授權
   - *false* :前往選取MVPD

- c.getAuthentication :SDK將包含 **access_token** 在呼叫參數中 

   - mvpd已記得：前往setSelectedProvider(mvpd\_id)
   - 未選取mvpd :displayProviderDialog
   - 已選取mvpd:前往setSelectedProvider(mvpd\_id)

- d.setSelectedProvider

   - mvpd\_id驗證url已在ChromeCustomTabs中載入
   - 登入成功：delegate.setAuthenticationStatus(SUCCESS)
   - 已取消登入：重置MVPD選擇
   - URL配置會建立為「adobepass://android.app」，以在驗證完成時擷取

- e.get/checkAuthorization :SDK會在標題中**access\_token **作為授權：承載 **access\_token**

- 如果授權成功，則會呼叫以取得媒體代號

- f.登出： 

   - SDK會刪除目前要求者的有效Token（由其他應用程式取得，且非透過SSO取得的驗證將維持有效）
   - SDK會開啟Chrome自訂分頁以到達mvpd\_id登出端點。 完成後，將會關閉Chrome自訂分頁
   - URL配置會建立為「adobepass://logout」，以擷取登出完成的時刻
   - logout會觸發sendTrackingData(new Event(EVENT\_LOGOUT,USER\_NOT\_AUTHENTICATED\_ERROR)和回呼：setAuthenticationStatus(0,&quot;Logout&quot;)

 

**注意：** 因為每個呼叫都需要 **access_token**,SDK會處理下列可能的錯誤碼。 

| 錯誤回應 |  |  |
|--- | --- | --- |
| invalid_request | 400 | 請求的格式不正確。 SDK應停止對伺服器執行呼叫。 |
| invalid_client | 403 | 用戶端ID不再允許執行要求。 sdk必須重新執行用戶端註冊。 |
| access_denied | 401 | access_token無效。 sdk必須要求新的access_token。 |

