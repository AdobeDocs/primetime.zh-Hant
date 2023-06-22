---
title: Amazon FireOS SDK與Dynamic Client註冊
description: Amazon FireOS SDK與Dynamic Client註冊
exl-id: 27acf3f5-8b7e-4299-b0f0-33dd6782aeda
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 0%

---

# Amazon FireOS SDK與Dynamic Client註冊 {#amazon-fireos-sdk-with-dynamic-client-registration}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

</br>

## <span id=""></span>簡介 {#Intro}

已修改適用於FireTV的FireOS AccessEnabler SDK，以啟用驗證而不使用工作階段Cookie。 隨著越來越多的瀏覽器限制對Cookie的存取，需要另一種方法來允許驗證。

**FireOS SDK 3.0.4** 以簽署的請求者ID和工作階段Cookie驗證，取代目前的應用程式註冊機制 [動態使用者端註冊](/help/authentication/dynamic-client-registration.md).
 

## API變更 {#API}

### Factory.getInstance

**說明：** 具現化Access Enabler物件。 每個應用程式執行個體應有一個存取啟用程式執行個體。

| API呼叫：建構函式 |
| --- |
| 公用靜態AccessEnabler getInstance(Context appContext、String softwareStatement、String redirectUrl)<br>        擲回AccessEnablerException |

**可用性：** v3.0+

**引數：**

- *appContext*：Android應用程式內容
- *軟體陳述式*：從TVE控制面板或取得的值 *null* 如果在strings.xml中設定&quot;software\_statement&quot;
- *redirectUrl* ：對於FireTV實作，此引數應該為Null。 將忽略此屬性上的任何設定。 

**附註**

- 無效的softwareStatement將導致應用程式無法初始化AccessEnabler或註冊Adobe Pass驗證和授權的應用程式
- FireTV的redirectUrl引數由SDK設定為adobepass://android.app ，因為驗證是由唯一的AccessEnabler執行個體處理。

### setRequestor

**說明：** 建立管道的身分。 每個管道在為Adobe Primetime驗證系統向Adobe註冊後都會獲得一個唯一的ID。 處理SSO和遠端Token時，驗證狀態會在應用程式於背景時變更，當應用程式進入前景時可再次呼叫setRequestor，以便與系統狀態同步（如果SSO已啟用，請擷取遠端Token，如果同時發生登出，請刪除本機Token）。

伺服器回應包含MVPD清單，以及附加到通道身分識別的一些設定資訊。 伺服器回應由Access Enabler程式碼在內部使用。 只有作業的狀態（即SUCCESS/FAIL）會透過setRequestorComplete()回呼顯示給您的應用程式。

如果 *url* 不會使用引數，因此產生的網路呼叫會鎖定預設服務提供者URL：Adobe發行生產環境。

如果提供的值用於 *url* 引數，則所產生的網路呼叫會鎖定中提供的所有URL *url* 引數。 所有設定請求都在不同的執行緒中同時觸發。 第一個回應者在編譯MVPD清單時優先。 對於清單中的每個MVPD，「存取啟用程式」會記住相關服務提供者的URL。 所有後續的軟體權利檔案要求都會導向至與設定階段期間與目標MVPD配對的服務提供者相關聯的URL。

| API呼叫：要求者設定 |
| --- |
| 公用void setRequestor(String requestorId) |

**可用性：** v3.0+

| API呼叫：要求者設定 |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**可用性：** v3.0+

**引數：**

- *請求者ID*：與管道相關聯的唯一ID。 當您首次向Adobe Primetime驗證服務註冊時，請將Adobe指派的唯一ID傳遞至您的網站。
- *url*：選用引數；預設會使用Adobe服務提供者(http://sp.auth.adobe.com/)。 此陣列可讓您為Adobe提供的驗證和授權服務指定端點（不同的執行個體可用於偵錯）。 您可以使用此選項來指定多個Adobe Primetime驗證服務提供者執行個體。 如此一來，MVPD清單就會由所有服務提供者的端點組成。 每個MVPD都與最快的服務提供者相關聯，也就是首先回應並支援該MVPD的提供者。

已棄用：

- *signedRequestorID*：以私密金鑰數位簽署的請求者ID復本。 <!--For more details, see [Registering Native Clients](http://tve.helpdocsonline.com/registering-native-clients)-->.

**觸發的回呼：** `setRequestorComplete()`

</br>

### 登出

**說明：** 使用此方法可起始登出流程。 登出是一系列HTTP重新導向作業的結果，因為使用者需要同時從Adobe Primetime驗證伺服器和MVPD的伺服器登出。 因此，此流程將開啟ChromeCustomTab視窗以執行登出。

| API呼叫：起始登出流程 |
| --- |
| public void logout() |

**可用性：** v3.0+

**引數：** 無

**觸發的回呼：** `setAuthenticationStatus()`

## 程式設計師實作流程 {#Progr}

### **1. 註冊應用程式** 

1. 從Adobe Pass （ TVE控制面板）取得software\_statement
1. 您可透過兩個選項將這些值傳遞至Adobe Pass SDK：
   - 在strings.xml中新增： 

      ```
      <string name>"software\_statement">[softwarestatement value]</string>
      ```

   - 呼叫AccessEnabler.getInstance(appContext，softwareStatement， null)

 

### **2. 設定應用程式**

- a. setRequestor(requestor\_id) 

   SDK將執行下列操作： 

   - 註冊應用程式：使用 **software\_statement**，SDK將會取得 **client\_id， client\_secret， client\_id\_issued\_at， redirect\_uris， grant\_types**. 此資訊會儲存在應用程式的內部儲存空間中。
   - 取得 **access\_token** 使用client\_id、client\_secret和grant\_type=&quot;client\_credentials&quot; 。 此access\_token將用於SDK對Adobe Pass伺服器進行的每次呼叫。

| 權杖錯誤回應： |  |  |
|--- | --- | --- |
| HTTP 400 （錯誤請求） | {&quot;error&quot;： &quot;invalid\_request&quot;} | 請求缺少必要的引數、包含不受支援的引數值（授權型別除外）、重複引數、包含多個認證、使用多個機制來驗證使用者端，或格式錯誤。 |
| HTTP 400 （錯誤請求） | {&quot;error&quot;： &quot;invalid\_client&quot;} | 使用者端驗證失敗，因為使用者端不明。 SDK *必須* 再次向授權伺服器註冊。 |
| HTTP 400 （錯誤請求） | {&quot;error&quot;： &quot;unauthorized\_client&quot;} | 已驗證的使用者端無權使用此授權授予型別。 |

- 如果MVPD需要被動驗證，則會開啟WebView以使用該MVPD執行被動驗證，並在完成後關閉

- b. checkAuthorization()

   - *true* ：前往授權
   - *false* ：前往選取MVPD

- c. getAuthentication ：SDK將包含 **access_token** 在呼叫引數中 

   - 記憶的mvpd ：前往setSelectedProvider(mvpd\_id)
   - 未選取mvpd ： displayProviderDialog
   - 已選取mvpd ：前往setSelectedProvider(mvpd\_id)

- d. setSelectedProvider

   - mvpd\_id驗證url已載入ChromeCustomTabs中
   - 登入成功： delegate.setAuthenticationStatus ( SUCCESS )
   - 登入已取消：重設MVPD選擇
   - URL配置會建立為「adobepass://android.app」，以便在驗證完成時擷取

- e. get/checkAuthorization ： SDK將在標頭中包含**access\_token **as Authorization： Bearer **access\_token**

- 如果授權成功，將會呼叫以取得媒體權杖

- f.登出： 

   - SDK將會刪除目前請求者的有效Token （由其他應用程式取得而非透過SSO取得的驗證將保持有效）
   - SDK將開啟Chrome自訂標籤以存取mvpd\_id登出端點。 完成後，Chrome自訂標籤將關閉
   - URL配置會建立為「adobepass://logout」，以擷取登出完成時的時間
   - 登出將會觸發sendTrackingData(new Event(EVENT\_LOGOUT，USER\_NOT\_AUTHENTICATED\_ERROR)和回呼：setAuthenticationStatus(0，&quot;Logout&quot;)

 

**注意：** 因為每個呼叫都需要 **access_token**，下列可能的錯誤碼會在SDK中處理。 

| 錯誤回應 |  |  |
|--- | --- | --- |
| invalid_request | 400 | 要求的格式錯誤。 SDK應停止執行對伺服器的呼叫。 |
| invalid_client | 403 | 不再允許使用者端ID執行要求。 sdk必須再次執行使用者端註冊。 |
| access_denied | 401 | access_token無效。 sdk必須要求新的access_token。 |
