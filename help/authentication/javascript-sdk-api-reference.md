---
title: JavaScript SDK API參考
description: JavaScript SDK API參考
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2835'
ht-degree: 0%

---


# JavaScript SDK API參考 {#javascript-sdk-api-reference}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## API參考 {#api-reference}

這些函式會起始與MVPD互動的請求。 所有呼叫均為非同步；您必須實作 [回撥](#callbacks) 若要處理回應：

- [setRequestor()](#setReq)
- [getAuthorization()](#getAuthZ)
- [getAuthentication()](#getAuthN)
- [checkAuthentication()](#checkAuthN)
- [checkAuthorization()](#checkAuthZ)
- [checkPreauthorizedResources()](#checkPreauthRes)
- [getMetadata()](#getMeta)
- [setSelectedProvider()](#setSelProv)
- [logout()](#logout)


## setRequestor(inRequestorID, endpoints, options){#setrequestor(inRequestorID,endpoints,options)}

**說明：** 識別請求的來源網站。  您必須先進行此呼叫，才能進行通訊工作階段中的任何其他API呼叫。 

**參數：**

- *inRequestorID*  — 註冊期間指派給原始網站的Adobe唯一識別碼。

- *端點*  — 此參數為選用。 可以是下列其中一個值：

   - 允許您為Adobe提供的驗證和授權服務指定端點的陣列（不同實例可能用於調試）。 若提供多個URL，則MVPD清單會由來自所有服務提供者的端點組成。 每個MVPD都與最快的服務提供商相關聯；即第一個回應且支援該MVPD的提供者。 依預設（若未指定值），會使用Adobe服務提供者(<http://sp.auth.adobe.com/>)。

   範例：
   - `setRequestor("IFC", ["http://sp.auth-dev.adobe.com/adobe-services"])`


- *選項*  — 包含「應用程式ID」值、「訪客ID」值無重新整理設定（背景登入登出）和MVPD設定(iFrame)的JSON物件。 所有值均為選用。
   1. 若已指定，則會在程式庫執行的所有網路呼叫上報告Experience CloudvisitorID。 值稍後可用於進階分析報表。
   2. 如果指定了應用程式的唯一標識符 — `applicationId`  — 值會新增至應用程式後續進行的所有呼叫，作為X-Device-Info HTTP標題的一部分。 此值稍後可從中擷取 [ESM](/help/authentication/entitlement-service-monitoring-overview.md) 使用正確查詢來報告。

   **注意：** 所有JSON索引鍵均區分大小寫。

    範例：

```JSON
   setRequestor("IFC", {
      "visitorID": "THE_ECID_VALUE",
      "applicationId": "APP_ID_VALUE"
  })
```

- 程式設計人員可以覆寫在Adobe Primetime驗證中設定的MVPD設定，方法是指定登入是否需要iFrame(*iFrameRequired* 索引鍵)和iFrame維度(*iFrameWidth* 和 *iFrameHeight* 鍵)。 JSON物件具有下列範本：

```JSON
    {  
       "visitorID": <string>,
       "backgroundLogin": <boolean>,
       "backgroundLogout": <boolean>,
       "mvpdConfig":{  
          "MVPD_ID_1":{  
             "iFrameRequired": <boolean>,
             "iFrameWidth": <integer>,
             "iFrameHeight": <integer>
          },
          ...
          "MVPD_ID_N":{  
             "iFrameRequired": <boolean>,
             "iFrameWidth": <integer>,
             "iFrameHeight": <integer>
          }
       }
    }
```
 

上述範本中的所有頂層索引鍵均為選用，且具有預設值(*backgroundLogin*, *backgroundLogut*&#x200B;預設為false，而mvpdConfig為null — 表示沒有覆寫任何MVPD設定)。

 
- **附註**:為上述參數指定無效值/類型將導致未定義行為。

 

以下是下列案例的設定範例：啟用無刷新登入和登出，將MVPD1變更為完整頁面重新導向登入（非iFrame），並將MVPD2變更為iFrame登入，寬度=500且高度=300:

```JSON
    {  
       "backgroundLogin": true,
       "backgroundLogout": true,
       "mvpdConfig":{  
          "MVPD1":{  
             "iFrameRequired": false
          },
          "MVPD2":{  
             "iFrameRequired": true,
             "iFrameWidth": 500,
             "iFrameHeight": 300
          }
       }
    }
```


**已觸發回呼：** [setConfig()](#setconfigconfigxml-setconfigconfigxml)
</br>

[返回頁首](#top)

</br>

## getAuthorization(inResourceID, redirect_url) {#getauthorization(inresourceid,redirect_url)}

**說明：** 請求指定資源的授權。 每當客戶嘗試訪問可授權資源時，請調用此函式，從Access Enabler獲取短期授權令牌。 資源ID與提供授權的MVPD商定。

使用目前客戶的快取驗證Token。 如果找不到此類令牌，請先啟動驗證進程，然後繼續進行授權。\
 
**參數：**

- `inResourceID`  — 用戶向其請求授權的資源ID。
- `redirect_url`  — 可選擇提供重新導向URL，讓MVPD的授權程式將使用者傳回該頁面，而非起始授權的頁面。


**已觸發回呼：** [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken) 成功時， [tokenRequestFailed](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage) 失敗

>[!CAUTION]
>
>請盡可能使用checkAuthorization()，而不是getAuthorization()。 getAuthorization()方法將啟動完整身份驗證流（如果用戶未通過身份驗證），這可能導致程式設計師端的複雜實現。

</b>

[返回頁首](#top)

</br>

## getAuthentication(redirect_url) {#getauthentication(redirect_url}

**說明：** 請求當前客戶的驗證。 通常會因應點按登入按鈕而呼叫。 檢查目前客戶的快取驗證Token。 如果找不到此類代號，則啟動驗證過程。 這會叫用預設或自訂的提供者選取對話方塊，然後使用選取的提供者來重新導向至MVPD的登入介面。

成功時，會建立並儲存使用者的驗證Token。 如果驗證失敗，提供者會傳回適當的錯誤訊息給您的 [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode) 回呼。

**參數：**

- redirect_url — 選擇性地提供重新導向URL，以便MVPD的驗證程式將使用者傳回至該頁面，而非起始驗證的頁面。

 **已觸發回呼：** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode), [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[返回頁首](#top)

</br>

## checkAuthN {#checkauthn}

**說明：** 檢查當前客戶的當前驗證狀態。  未與任何UI關聯。

**已觸發回呼：** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

[返回頁首](#top)

</br>

## checkAuthorization(inResourceID) {#checkauthorization(inresourceid)}

**說明：** 應用程式使用此方法來檢查目前客戶和指定資源的授權狀態。 首先檢查驗證狀態。 若未驗證，則會觸發tokenRequestFailed()回呼，方法會退出。 如果使用者已驗證，也會觸發授權流程。 請參閱 [getAuthorization()](#getAuthZ方法。

>[!TIP]
>
> **使用檢查狀態函式**  在請求授權之前，您不需要檢查驗證或授權的狀態。 例如，您可以呼叫這些函式，以更新您自己的狀態顯示。 若需要任何使用者互動，請勿使用。

**參數：**

- `inResourceID`  — 用戶向其請求授權的資源ID。

 
**已觸發回呼：**
[setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken), [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata), [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

## checkPreauthorizedResources(resources) {#checkPreauthorizedResources(resources)}

**說明：** 請求「預檢」授權狀態以取得資源清單。

**參數：**

- *資源*:資源參數是應檢查授權的資源陣列。 清單中的每個元素都應是代表資源ID的字串。 資源ID受與 `getAuthorization()` 呼叫，即是程式設計師和MVPD或媒體RSS片段之間建立的協定值。 

</br>

## checkPreauthorizedResources(resources-cache=true) {#checkPreauthorizedResources(resources-cache=true)}

此API變體可從JS SDK 4.0版開始提供使用


**參數：**

- *資源*:資源參數是應檢查授權的資源陣列。 清單中的每個元素都應是代表資源ID的字串。 資源ID受與 `getAuthorization()` 呼叫，即是程式設計師和MVPD或媒體RSS片段之間建立的協定值。 

- *快取*:檢查預授權資源時是否使用內部快取。 此為選用參數，預設為 **true**. 如果為true，則行為與上述API相同，表示後續對此函式的呼叫將使用內部快取來解析預先授權的資源。 傳遞 **false** 針對此參數，會停用內部快取，導致每次 **checkPreauthorizedResources** 呼叫API。

**已觸發回呼：** [preauthorizedResources()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)
 
</br>

[返回頁首](#top)
</br>

## getMetadata(Key) {#getMetadata}

**說明：** 檢索Access Enabler庫作為元資料公開的資訊。

中繼資料有兩種類型： 

- **靜態** （驗證Token TTL、授權Token TTL和裝置ID） 
- **使用者中繼資料** （這包括在驗證和/或授權流程期間從MVPD傳遞至使用者裝置的使用者特定資訊）

**更多資訊：** [使用者中繼資料](#UserMetadata)

**參數：**

- *key*:指定所請求元資料的ID:
   - 如果鍵為 `"TTL_AUTHN",` 然後進行查詢以取得驗證Token過期時間。

   - 如果鍵為 `"TTL_AUTHZ"` 而params是包含資源id的字串的陣列，然後進行查詢以獲得與指定資源相關聯的授權令牌的到期時間。

   - 如果鍵為 `"DEVICEID"` 然後進行查詢以取得目前的裝置id。 請注意，此功能預設為停用，程式設計人員應聯絡Adobe，以取得啟用和費用的相關資訊。

   - 如果索引鍵來自下列使用者中繼資料類型清單，則會將包含對應使用者中繼資料的JSON物件傳送至 [`setMetadataStatus()`](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata) 回呼函式：

   - `"zip"`  — 郵遞區號

   - `"encryptedZip"`  — 加密的郵遞區號

   - `"householdID"`  — 家庭標識符。 如果MVPD不支援子帳戶，則會與userID相同。

   - `"maxRating"`  — 用戶的最高父母分級

   - `"userID"`  — 使用者識別碼。 若MVPD支援子帳戶，且使用者不是主帳戶，則userID會與housedyID不同。

   - `"channelID"`  — 使用者有權檢視的管道清單

   - `"is_hoh"`  — 標識使用者是否為戶主的旗標

   - `"encryptedZip"`  — 加密的郵遞區號

   - `"typeID"`  — 用於標識用戶帳戶是否為主/次帳戶的標誌

   - `"primaryOID"`  — 家庭標識符

   - `"postalCode"`  — 類似郵遞區號

   - `"acctID"`  — 帳戶ID

   - `"acctParentID"`  — 帳戶父ID
   **附註**:程式設計師可用的實際用戶元資料取決於MVPD提供的內容。  請參閱 [使用者中繼資料](#UserMetadata) ，查看當前可用用戶元資料清單。


例如：

```JSON
    // Assume that a reference to the AccessEnabler has been previously 
    // obtained and stored in the "ae" variable
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
        if (status ==  1) {
            //user is authenticated, request metadata
            ae.getMetadata("zip");
            ae.getMetadata("maxRating");
        } else {
            ...
      }
    }
```
 

**已觸發回呼：** [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)

</br>

[返回頁首](#top)

</br>


## setSelectedProvider(providerid) {#setSelectedProvider}

**說明：** 當用戶從提供程式選擇UI中選擇了MVPD，以便將提供程式選擇發送到Access Enabler，或調用此函式（使用null參數），以備用戶不選擇提供程式而關閉提供程式選擇UI時使用。 

**已觸發回呼：**[ setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[返回頁首](#top)

</br>

## getSelectedProvider() {#getSelectedProvider}

**說明：** 在提供者選取對話方塊中擷取客戶選取的結果。 這可在初始驗證檢查後的任何時間使用。

此函式為非同步，會將其結果傳回給 `selectedProvider()` 回呼函式。

- **MVPD** 當前選擇的MVPD；如果未選擇MVPD，則為null。
- **AE_State** 目前客戶的驗證結果，其中「新使用者」、「使用者未驗證」或「使用者已驗證」

 **已觸發回呼：** [selectedProvider()](#getselectedprovider-getselectedprovider)

</br>

[返回頁首](#top)

</br>

## 註銷 {#logout}

**說明：** 註銷當前客戶，清除該用戶的所有身份驗證和授權資訊。 從客戶的系統中刪除所有authN和authZ代號。

 **已觸發回呼：** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)
</br> 

[返回頁首](#top)

</br>

## 回呼定義 {#calllback-definitions}

您必須實作這些回呼來處理非同步請求呼叫的回應：

- [entitlementLoaded()](#entitlementloaded-entitlementloaded)
- [setConfig()](#setconfigconfigxml-setconfigconfigxml)
- [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders)
- [createIFrame()](#createiframe-createiframeinwidthminheight)
- [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)
- [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)
- [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken)
- [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage)
- [preauthorizedResources()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)
- [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)
- [selectedProvider()](#selectedproviderresult-selectedprovider)

</br>

## entitlementLoaded() {#entitlementLoaded}

**說明：** 當Access Enabler完成初始化並準備好接收請求時觸發。 實作此回呼以知道何時可以開始與Access Enabler API通信。
</br>

[返回頁首](#top)

</br>

## setConfig(configXML) {#setconfig(configXML)}

**說明：** 實作此回呼以接收設定資訊和MVPD清單。

**參數：**

- *configXML*:xml物件，其中包含目前REQUESTOR（包括MVPD清單）的設定。

 
**觸發者：** [setRequestor()](#setrequestor-inrequestorid-endpoints-optionssetreq)

</br>

[返回頁首](#top)

</br>

## displayProviderDialog(providers) {#displayproviderdialog(providers)}

**說明：** 實作此回呼以叫您自己的自訂提供者選取UI。 您的對話方塊應使用顯示名稱（和選用標誌）來提供客戶的選擇。 當客戶做出選擇並關閉對話方塊時，請在呼叫中將所選提供者的相關聯ID傳送至 *setSelectedProvider()*.

**參數：**

- *提供者*  — 表示請求MVPD的對象陣列：

```JSON
    var mvpd = {
        ID: "someprov",
        displayName: "Some Provider",
        logoURL: "http://www.someprov.com/images/logo.jpg"
    }
```

**觸發者：** [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>[返回頁首](#top)

</br>

## createIFrame(inWidth, inHeight) {#createIFrame(inWidth,inHeight)}

**說明：** 如果使用者選取的MVPD需要iFrame來顯示其驗證登入頁面UI，請實作此回呼。

**觸發者：**[ setSelectedProvider()](#setselectedproviderproviderid-setselectedprovider)

</br> [返回頁首](#top)

</br>

## setAuthenticationStatus(isAuthenticated, errorCode) {#set-authn-status-isauthn-error}

**說明：** 如果嘗試判斷驗證狀態時發生任何錯誤（檢查成功完成時出現空白字串），請實作此回呼以接收驗證狀態（1=authenticated或0=not authenticated）和描述性錯誤訊息。

>[!NOTE]
> 
>如果您使用目前 [進階錯誤報告](/help/authentication/error-reporting.md) 系統中，您可以忽略發送到此函式的errorCode參數。  不過， isAuthenticated旗標仍可用於追蹤權限流程中使用者的驗證狀態


**參數：**

- *isAuthenticated*  — 提供身份驗證狀態：1（已驗證）或0（未驗證）。
- *errorCode*  — 確定身份驗證狀態時發生的任何錯誤。 空字串（若無）。

 
**觸發者：** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid)

</br>

[返回頁首](#top)

</br>

## sendTrackingData(trackingEventType, trackingData) {#sendTrackingData(trackingEventType,trackingData)}

>[!CAUTION]
>
>裝置類型和作業系統是透過使用公用Java程式庫(<http://java.net/projects/user-agent-utils>)和使用者代理字串。 請注意，此資訊僅作為將操作量度劃分為裝置類別的粗略方式提供，但該Adobe對錯誤的結果不負責。 請據此使用新功能。

**說明：** 實作此回呼以在特定事件發生時接收追蹤資料。 例如，您可以使用它來追蹤有多少使用者已使用相同的憑證登入。 目前無法設定追蹤。 使用Adobe Primetime驗證1.6, `sendTrackingData()` 還報告了有關設備、Access Enabler客戶端和作業系統類型的資訊。 此 `sendTrackingData()` 回呼仍回溯相容。\
 
- 設備類型的可能值：
   - 電腦
   - 平板電腦
   - 行動
   - 遊戲
   - 未知

- Access Enabler客戶端類型的可能值：
   - html5
   - ios
   - android


傳遞事件類型和相關資訊的陣列。 事件類型包括：

| mvpdSelection | 使用者在提供者選取對話方塊中選取了MVPD。 |
| ----------------------- | --------------------------------------------------------- |
| authenticationDetection | 驗證檢查已完成。 |
| authorizationDetection | 授權請求已完成。 |

</br>
資料是每種事件類型專屬的：
</br>

| 事件類型（字串） | 資料（陣列） |
|:--- | :--- |
| mvpdSelection | 0:所選MVPD |
|  | 1:裝置類型 |
|  | 2:Access Enabler客戶端類型 |
|  | 3:作業系統 |
| authenticationDetection | 0:Token要求是否成功(true/false) |
|  | 1:MVPD ID |
|  | 2:GUID |
|  | 3:快取中的Token(true/false) |
|  | 4:裝置類型 |
|  | 5:Access Enabler客戶端類型 |
|  | 6:作業系統 |
| authorizationDetection | 0:Token要求是否成功(true/false) |
|  | 1:MVPD ID |
|  | 2:GUID |
|  | 3:快取中的Token(true/false) |
|  | 4:錯誤 |
|  | 5:詳細資料 |
|  | 6:裝置類型 |
|  | 7:Access Enabler客戶端類型 |
|  | 8:作業系統 |


**觸發者：** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>

[返回頁首](#top)

</br>

## setToken(inRequestedResourceID, inToken) {#setToken(inRequestedResourceID,inToken)}

**說明：** 實作此回呼以接收已提出授權要求或檢查授權要求且已成功完成之資源(inRequestedResourceID)的短期媒體Token(inToken)和ID。

**觸發者：** [checkAuthorization()](#checkAuthZ), [getAuthorization()](#getAuthZ)
</br>

[返回頁首](#top)

</br>

## tokenRequestFailed(inRequestedResourceID, inRequestErrorCode, inRequestDetailedErrorMessage) {#token-request-failed-error-msg}

**說明：** 實作此回呼以在授權或檢查授權要求失敗時發出信號。 MVPD可以選擇使用來提供要由程式設計師顯示的自定義消息。

>[!IMPORTANT]
>
>此回呼函式是舊版原始Primetime驗證錯誤報告系統的一部分。 它會保留以供回溯相容，但如果您已使用目前的進階錯誤報告系統實作自己的回呼，則完全不需要使用此函式。 較新的錯誤報告系統提供了關於授權（或其他操作）失敗的原因的更詳細資訊，以及針對每種錯誤或警告類型的建議操作過程。

**參數：**

- *inRequestedResourceID*  — 提供授權請求上使用的資源ID的字串。
- *inRequestErrorCode*  — 顯示Adobe Primetime驗證錯誤碼的字串，指出失敗的原因；可能的值是「用戶未驗證錯誤」和「用戶未授權錯誤」；如需詳細資訊，請參閱下方的「回呼錯誤碼」。
- *inRequestDetailedErrorMessage*  — 適合顯示的其他描述性字串。 如果此描述性字串因任何原因無法使用，Adobe Primetime驗證會傳送空字串 **(&quot;&quot;)**.  MVPD可使用此MVPD傳遞自訂錯誤訊息或銷售相關訊息。 例如，如果訂閱者被拒絕對資源進行授權，MVPD可以使用 `*inRequestDetailedErrorMessage*` 例如： **「您目前在套件中無法存取此管道。 如果要升級包，請按一下\*這裡\*。」** 該消息由Adobe Primetime身份驗證通過此回調傳遞到程式設計師站點。 然後程式設計師可以選擇顯示或忽略它。 Adobe Primetime驗證也可以使用 `*inRequestDetailedErrorMessage*` 通知程式設計師可能導致錯誤的條件。 例如， **&quot;與提供商的授權服務通信時發生網路錯誤&quot;。**

 

**觸發者：**  [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)
</br>

[返回頁首](#top)

</br>


## preauthorizedResources(authorizedResources) {#preauthorizedResources(authorizedResources)}

**說明：** 由Access Enabler觸發的回調，該啟用程式提供在調用後返回的授權資源清單 `checkPreauthorizedResources()`.

**參數：**

- *authorizedResources*：授權資源的清單。

**觸發者：** [checkPreauthorizedResources()](#checkPreauthRes)
</br>

[返回頁首](#top)

</br>

## setMetadataStatus(key, encrypted, data) {#setMetadataStatus(key,encrypted,data)}

**說明：** 由Access Enabler觸發的回調，該啟用程式通過 `getMetadata()` 呼叫。

**更多資訊：** [使用者中繼資料](#userMetadata)

**參數：**

- *索引鍵（字串）*:提出請求的中繼資料的索引鍵。
- *加密（布林值）*:表示「值」是否已加密的標幟。 如果此值為「true」，則「value」實際上會是實際值的JSON網頁加密表示法。 
- *資料（JSON物件）*:表示中繼資料的JSON物件。適用於簡單要求(「`TTL_AUTHN`&#39;, &#39;`TTL_AUTHZ`&#39;, &#39;`DEVICEID`&#39;)，結果為字串（代表驗證TTL、授權TTL或裝置ID）。 若是使用者中繼資料請求，結果可以是代表中繼資料裝載的基元或JSON物件。 JSON使用者中繼資料物件的實際結構類似下列：

```JSON
    {
        updated: 1334243471,
        encrypted: ["encryptedProp"],
        data: {
            zip: ["12345", "34567"],
            maxrating: { 
                "MPAA": "PG-13",
                "VCHIP": "TV-Y", 
                "URL": "http://exam.pl/e/manage/ratings"
            },
            householdid: "3456",
            uid: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
            channelID: ["channel-1", "channel-2"]
    }
```
 

例如：

```JSON
    // Implement the setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
        if (encrypted) {
            //the metadata value is encrypted
            //needs to be decrypted by the programmer
            data = decrypt(data);
        }
        alert(key + "=" + data);
    }
```
 

**觸發者：** [`getMetadata()`](#getmetadatakey-getmetadata)
</br>
[返回頁首](#top)

</br>

## selectedProvider(result) {#selectedProvider(result)}

**說明：** 實作此回呼以接收目前選取的MVPD和包裝在 `result` 參數。 此 `result` 參數是物件，具有下列屬性：

- **MVPD** 當前選擇的MVPD；如果未選擇MVPD，則為null。
- **AE\_State** 目前使用者（「新使用者」、「使用者未驗證」或「使用者已驗證」其中之一）的驗證結果

 **觸發者：** [getSelectedProvider()](#getSelProv)

</br>

[返回頁首](#top)

</br>

### 回撥錯誤代碼 {#callback-error-codes}

| 一般錯誤 |  |
|:--- | :--- | 
| 內部錯誤 | 嘗試處理請求時發生系統錯誤。 |
| 未選擇提供程式錯誤 | 在提供者選擇對話方塊中取消時發生 |
| 提供程式不可用錯誤 | 當沒有提供程式時發生。 |

| 驗證錯誤 |  |
|:--- | :--- | 
| 一般驗證錯誤 | 當原因未知或無法發佈時傳回。 |
| 內部驗證錯誤 | 嘗試驗證時出現系統錯誤。 |
| 用戶未驗證錯誤 | 未驗證用戶。 |
| 多個驗證請求錯誤 | 在第一個驗證請求完成之前收到了其他驗證請求。 |

| 授權錯誤 |  |
|:--- | :--- | 
| 一般授權錯誤 | 當原因未知或無法發佈時傳回。 |
| 內部授權錯誤 | 嘗試授權時發生系統錯誤。 |
| 用戶未授權錯誤 | 客戶無權查看請求的內容。 |

<!--

### Related Information {#Related-Infornation}

* [JavaScript SDK Overview](/help/authentication/javascript-sdk-overview.md)
* [JavaScript SDK Cookbook](/help/authentication/javascript-sdk-cookbook.md)
* **JavaScript Code Samples**
* [Error Reporting](/help/authentication/error-reporting.md)
* [Understanding Tokens](#understanding_tokens)
* **Tracking Data in Adobe Primetime authentication**
-->

[返回頁首](#top)

