---
title: 帶動態客戶端註冊的Android SDK
description: 帶動態客戶端註冊的Android SDK
exl-id: 8d0c1507-8e80-40a4-8698-fb795240f618
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 0%

---

# 帶動態客戶端註冊的Android SDK {#android-sdk-with-dynamic-client-registration}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 導言 {#Intro}

Android AccessEnabler SDK已修改，以啟用身份驗證，而不使用會話cookie。 隨著越來越多的瀏覽器限制對Cookie的訪問，需要使用另一種方法來允許身份驗證。

對於Android，使用Chrome自定義頁籤會限制從其他應用程式訪問Cookie。

>**Android SDK 3.0.0** 介紹：

- 動態客戶端註冊取代基於簽名請求者ID和會話cookie驗證的當前應用註冊機制
- 驗證流的Chrome自定義頁籤

>[!NOTE]
>
>對於不支援Chrome自定義頁籤的較舊Android版本，將使用與較舊AccessEnabler SDK版本類似的WebView身份驗證。


## 動態客戶端註冊 {#DCR}

Android SDK v3.0+將使用中定義的動態客戶端註冊過程 [動態客戶端註冊](/help/authentication/dynamic-client-registration.md)。


## 功能演示 {#Demo}

請看 [本網路研討會](https://my.adobeconnect.com/pzkp8ujrigg1/) 它提供了功能的更多上下文，並包含一個演示，介紹如何使用TVE Dashboard管理軟體語句，以及如何使用Adobe作為Android SDK的一部分提供的演示應用程式test生成的語句。

## API更改 {#API}


### Factory.getInstance

**描述：** 實例化Access Enabler對象。 每個應用程式實例應有一個Access Enabler實例。

| API調用：建構子 |
| --- |
| 公共靜態AccessEnabler getInstance(Context appContext、String softwareStatement、String redirectUrl)<br>        引發AccessEnablerException |


**可用性：** v3.0+

**參數：**

- *應用上下文*:Android應用程式上下文
- softwareStatement（軟體語句）:從TVE儀表板或 *空* 如果在strings.xml中設定「software\_statement」
- 重定向URL:唯一url,TVE儀表板或TVE儀表板中顯式添加的反向順序的域之一 *空* 如果在strings.xml中設定「redirect\_uri」

注：無效的softwareStatement或redirectUrl將導致應用程式無法初始化AccessEnabler或註冊應用程式以進行Adobe Pass身份驗證和授權
</br>
注：redirectUrl參數或strings.xml中的redirect\_uri應是在TVE儀表板中為應用程式添加的以反向順序排列的域的值(例如：對於TVE儀表板中添加的域「adobe.com」，redirectUrl應為「com.adobe」。
 

### setRequestor

**描述：** 確定渠道的標識。 在向Adobe PrimetimeAdobe系統註冊時，每個通道都分配了唯一的ID。 在處理SSO和遠程令牌時，當應用程式處於後台時，驗證狀態可能會更改，當應用程式進入前台時，可以再次調用setRequestor以與系統狀態同步（如果啟用了SSO，則提取遠程令牌；如果同時發生註銷，則刪除本地令牌）。

伺服器響應包含MVPD清單以及附加到通道標識的某些配置資訊。 伺服器響應由Access Enabler代碼在內部使用。 只有操作的狀態（即SUCCESS/FAIL）通過setRequestorComplete()回調顯示給您的應用程式。

如果 *URL* 未使用參數，生成的網路呼叫目標為預設服務提供商URL:Adobe版本/生產環境。

如果為 *URL* 參數，生成的網路調用針對中提供的所有URL *URL* 的下界。 所有配置請求都在單獨的線程中同時觸發。 編譯MVPD清單時，第一響應程式優先。 對於清單中的每個MVPD,Access Enabler會記住關聯服務提供商的URL。 所有後續權利請求都指向在配置階段與目標MVPD配對的與服務提供商關聯的URL。

| API調用：請求者配置 |
| --- |
| ```public void setRequestor(String requestorId)``` |

**可用性：** v3.0+

| API調用：請求者配置 |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**可用性：** v3.0+

**參數：**

- *請求者ID*:與通道關聯的唯一ID。 在首次向Adobe PrimetimeAdobe服務註冊時，將通過驗證分配的唯一ID傳遞到您的站點。
- *URL*:可選參數；預設情況下，使用Adobe服務提供程式 [http://sp.auth.adobe.com/](http://sp.auth.adobe.com/)。 此陣列允許您為Adobe提供的身份驗證和授權服務指定端點（可能會將不同的實例用於調試目的）。 您可以使用它指定多個Adobe Primetime身份驗證服務提供程式實例。 執行此操作時，MVPD清單由來自所有服務提供商的端點組成。 每個MVPD都與最快速的服務提供商相關聯；即，首先響應的提供程式，並且支援該MVPD。

已棄用：

- *簽名請求者ID*:用您的私鑰進行數字簽名的請求者ID的副本。 <!--For more details, see [Registering Native Clients](http://tve.helpdocsonline.com/registering-native-clients)-->。

**觸發的回調：** `setRequestorComplete()`

### 註銷

**描述：** 使用此方法啟動註銷流。 註銷是一系列HTTP重定向操作的結果，因為用戶需要從Adobe Primetime認證伺服器和MVPD伺服器註銷。 因此，此流將開啟ChromeCustomTab窗口以執行註銷。

| API調用：啟動註銷流 |
| --- |
| 公共void logout() |

**可用性：** v3.0+

**參數：** 無

**觸發的回調：** `setAuthenticationStatus()`
</br></br>

## 程式設計師實施流程 {#Progr}

### **1. 註冊應用程式** 

a.從Adobe Pass獲取軟體\_語句並重定向\_uri（TVE儀表板）

b.將這些值傳遞給Adobe PassSDK有兩種選項：

在strings.xml add中： 

```XML
<string name="software_statement">[softwarestatement value]</string>
<string name="redirect_uri">application_url.com</string>
```

調用AccessEnabler.getInstance(appContext,softwareStatement, redirectUrl)


### 2.配置應用程式

a.setRequestor(requestor\_id) 

SDK將執行以下操作： 

- 註冊應用程式：使用 **軟體\_語句**, SDK將獲取 **客戶端\_id，客戶端\_secret, client\_id\_issued\_at, redirect\_uris，授予\_types**。 此資訊將儲存在應用程式的內部儲存中。

- 獲得 **訪問\_令牌** 使用客戶端\_id、客戶端\_secret和grant\_type=&quot;客戶端\_credentials&quot;。 此訪問\_token將用於SDK對Adobe Pass伺服器進行的每次調用 

**令牌錯誤響應：**

| 錯誤響應 |  |  |
| --- | --- | --- |
| HTTP 400（錯誤請求） | {「error」（錯誤）:&quot;無效\_請求&quot; | 該請求缺少所需參數、包括不受支援的參數值（除授予類型外）、重複參數、包括多個憑據、使用多個機制來驗證客戶端，或者格式不正確。 |
| HTTP 400（錯誤請求） | {「error」（錯誤）:&quot;無效\_client&quot;} | 客戶端身份驗證失敗，因為客戶端未知。 SDK必須再次向授權伺服器註冊。 |
| HTTP 400（錯誤請求） | {「error」（錯誤）:&quot;未授權\_客戶端&quot;} | 已驗證的客戶端無權使用此授權授權類型。 |

- 如果MVPD需要「被動驗證」，則「Chrome自定義」頁籤將開啟以使用該MVPD執行被動，並在完成後關閉

b. checkAuthentication()

- 真：轉到授權
- 假：轉至選擇MVPD

c.getAuthentication :SDK將包括 **訪問令牌** 調用參數 

- mvpd記住：轉到setSelectedProvider(mvpd_id)
- 未選擇mvpd:displayProviderDialog
- mvpd選定：轉到setSelectedProvider(mvpd_id)

d.setSelectedProvider

- mvpd\_id驗證url載入到ChromeCustomTabs中
- 登錄成功：delegate.setAuthenticationStatus(SUCCESS)
- 登錄已取消：重置MVPD選擇
- URL方案建立為「adobepass://redirect_uri」，以在驗證完成時捕獲

e.get/checkAuthorization :SDK將包括 **訪問令牌** 在頭中作為授權：持 **訪問令牌**

- 如果授權成功，則將進行呼叫以獲取媒體令牌

f註銷： 

- SDK將刪除當前請求者的有效令牌（由其他應用程式獲取且未通過SSO進行的身份驗證將保持有效）
- SDK將開啟「Chrome自定義頁籤」以訪問mvpd_id註銷終結點。 完成後，將關閉Chrome自定義頁籤
- 將URL方案建立為「adobepass://logout」以捕獲註銷完成時的時間
- 註銷將觸發sendTrackingData(new Event(EVENT_LOGOUT,USER_NOT_AUTHENTICATED_ERROR)和回調：setAuthenticationStatus（0,&quot;註銷&quot;）

**注：** 因為每次呼叫都需要 **access_token,** 在SDK中處理以下可能的錯誤代碼。 


| 錯誤響應 |  |  |
| --- | ---|--- |
| 無效請求 | 400 | 請求格式不正確。 SDK應停止對伺服器執行調用。 |
| 無效的客戶端 | 403 | 不再允許客戶端ID執行請求。 SDK必須再次執行客戶端註冊。 |
| 拒絕訪問 | 401 | 訪問\_token無效。 SDK必須請求新的access_token。 |
