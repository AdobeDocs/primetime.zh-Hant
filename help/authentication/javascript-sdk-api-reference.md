---
title: JavaScript SDK API參考
description: JavaScript SDK API參考
exl-id: 48d48327-14e6-46f3-9e80-557f161acd8a
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '2835'
ht-degree: 0%

---

# JavaScript SDK API參考 {#javascript-sdk-api-reference}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## API參考 {#api-reference}

這些函式啟動與MVPD交互的請求。 所有呼叫都是非同步的；必須 [回調](#callbacks) 要處理響應：

- [setRequestor()](#setReq)
- [getAuthorization()](#getAuthZ)
- [getAuthentication()](#getAuthN)
- [checkAuthentication()](#checkAuthN)
- [checkAuthorization()](#checkAuthZ)
- [checkPreauthorizedResources()](#checkPreauthRes)
- [getMetadata()](#getMeta)
- [setSelectedProvider()](#setSelProv)
- [註銷()](#logout)


## setRequestor（inRequestorID、終結點、選項）{#setrequestor(inRequestorID,endpoints,options)}

**描述：** 標識請求的來源站點。  必須在通信會話中進行任何其他API調用之前進行此調用。 

**參數：**

- *inRequestorID* -Adobe在註冊期間分配給始發站點的唯一標識符。

- *端點*  — 此參數是可選的。 它可以是以下值之一：

   - 允許您為Adobe提供的驗證和授權服務指定端點的陣列（不同實例可能用於調試）。 如果提供了多個URL，則MVPD清單由來自所有服務提供商的端點組成。 每個MVPD都與最快速的服務提供商相關聯；即，首先響應的提供程式，並且支援該MVPD。 預設情況下（如果未指定值），將使用Adobe服務提供程式(<http://sp.auth.adobe.com/>)。

   示例：
   - `setRequestor("IFC", ["http://sp.auth-dev.adobe.com/adobe-services"])`


- *選項*  — 包含應用程式ID值、訪問者ID值無刷新設定（後台登錄註銷）和MVPD設定(iFrame)的JSON對象。 所有值都是可選的。
   1. 如果指定，將報告庫執行的所有網路調用的Experience Cloud訪問者ID。 該值稍後可用於高級分析報告。
   2. 如果指定了應用程式的唯一標識符 — `applicationId`  — 值將作為X-Device-Info HTTP標頭的一部分添加到應用程式進行的所有後續調用中。 以後可以從中提取此值 [ESM](/help/authentication/entitlement-service-monitoring-overview.md) 使用正確的查詢報告。

   **注：** 所有JSON鍵都區分大小寫。

    示例：

```JSON
   setRequestor("IFC", {
      "visitorID": "THE_ECID_VALUE",
      "applicationId": "APP_ID_VALUE"
  })
```

- 程式設計師可以覆蓋在Adobe Primetime驗證中配置的MVPD設定，方法是指定登錄是否需要iFrame(*需要iFrame* 鍵)和iFrame尺寸(*iFrameWidth* 和 *iFrameHeight* 鍵)。 JSON對象具有以下模板：

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
 

上面模板中的所有頂級鍵都是可選的，並且具有預設值(*後台登錄*。 *背景Logut*&#x200B;預設為false，而mvpdConfig為null — 表示未覆蓋MVPD設定)。

 
- **注釋**:為上述參數指定無效值/類型將導致未定義的行為。

 

下面是以下方案的一個配置示例：激活無刷新登錄和註銷，將MVPD1更改為全頁重定向登錄（非iFrame），將MVPD2更改為iFrame登錄，寬度=500，高度=300:

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


**觸發的回調：** [setConfig()](#setconfigconfigxml-setconfigconfigxml)
</br>

[返回頂部](#top)

</br>

## getAuthorization(inResourceID, redirect_url) {#getauthorization(inresourceid,redirect_url)}

**描述：** 請求對指定資源的授權。 每次客戶嘗試訪問可授權資源時，都調用此函式以從Access Enabler獲取短時間授權令牌。 資源ID與提供授權的MVPD商定。

使用當前客戶的快取身份驗證令牌。 如果找不到此類令牌，則首先啟動驗證過程，然後繼續授權。\
 
**參數：**

- `inResourceID`  — 用戶請求授權的資源的ID。
- `redirect_url`  — 可選地提供重定向URL，以便MVPD的授權進程將用戶返回該頁，而不是啟動授權的頁。


**觸發的回調：** [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken) 成功， [tokenRequestFailed](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage) 失敗

>[!CAUTION]
>
>請盡可能使用checkAuthorization()而不是getAuthorization()。 getAuthorization()方法將啟動完全身份驗證流（如果用戶未經身份驗證），這可能導致程式設計師方面的複雜實現。

</b>

[返回頂部](#top)

</br>

## getAuthentication(redirect_url) {#getauthentication(redirect_url}

**描述：** 請求當前客戶的身份驗證。 通常為響應按一下登錄按鈕而調用。 檢查當前客戶的快取身份驗證令牌。 如果找不到此類令牌，則啟動驗證過程。 此操作將調用預設或自定義提供程式選擇對話框，然後使用選定的提供程式重定向到MVPD的登錄介面。

成功後，建立並儲存用戶的驗證令牌。 如果驗證失敗，提供程式將向您返回相應的錯誤消息 [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode) 回叫。

**參數：**

- redirect_url — 可選地提供重定向URL，以便MVPD的驗證進程將用戶返回該頁，而不是啟動驗證的頁。

 **觸發的回調：** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)。 [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders)。 [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[返回頂部](#top)

</br>

## checkAuthN {#checkauthn}

**描述：** 檢查當前客戶的當前身份驗證狀態。  未與任何UI關聯。

**觸發的回調：** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

[返回頂部](#top)

</br>

## checkAuthorization(inResourceID) {#checkauthorization(inresourceid)}

**描述：** 應用程式使用此方法檢查當前客戶和給定資源的授權狀態。 首先檢查身份驗證狀態。 如果未通過身份驗證，則觸發tokenRequestFailed()回調，並且該方法退出。 如果用戶被認證，則它還觸發授權流。 請參閱 [getAuthorization()](#getAuthZ方法)。

>[!TIP]
>
> **使用check-status函式**  在請求授權之前，您無需檢查身份驗證或授權的狀態。 例如，您可以調用這些函式來更新自己的狀態顯示。 在需要任何用戶交互時，不要使用它們。

**參數：**

- `inResourceID`  — 用戶請求授權的資源的ID。

 
**觸發的回調：**
[setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken)。 [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage)。 [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)。 [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

## checkPreauthorizedResources（資源） {#checkPreauthorizedResources(resources)}

**描述：** 請求資源清單的「印前檢查」授權狀態。

**參數：**

- *資源*:資源參數是應檢查其授權的資源陣列。 清單中的每個元素都應是表示資源ID的字串。 資源ID受與 `getAuthorization()` 呼叫，即是程式設計師和MVPD之間建立的約定值，或媒體RSS片段。 

</br>

## checkPreauthorizedResources(resources-cache=true) {#checkPreauthorizedResources(resources-cache=true)}

此API變型可從JS SDK版本4.0開始使用


**參數：**

- *資源*:資源參數是應檢查其授權的資源陣列。 清單中的每個元素都應是表示資源ID的字串。 資源ID受與 `getAuthorization()` 呼叫，即是程式設計師和MVPD之間建立的約定值，或媒體RSS片段。 

- *快取*:檢查預授權資源時是否使用內部快取。 這是可選參數，預設為 **真**。 如果為true，則行為與上述API相同，這意味著後續對此函式的調用將使用內部快取來解析預授權資源。 傳遞 **假** 對於此參數，將禁用內部快取，導致每次 **checkPreauthorizedResources** 調用API。

**觸發的回調：** [預授權資源()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)
 
</br>

[返回頂部](#top)
</br>

## getMetadata（密鑰） {#getMetadata}

**描述：** 檢索Access Enabler庫以元資料形式公開的資訊。

元資料有兩種類型： 

- **靜態** （驗證令牌TTL、授權令牌TTL和設備ID） 
- **用戶元資料** （這包括在驗證和/或授權流程期間從MVPD傳遞到用戶設備的用戶特定資訊）

**更多資訊：** [用戶元資料](#UserMetadata)

**參數：**

- *鍵*:一個ID，它指定請求的元資料：
   - 如果鍵為 `"TTL_AUTHN",` 然後進行查詢以獲得認證令牌過期時間。

   - 如果鍵為 `"TTL_AUTHZ"` params是包含資源id作為字串的陣列，然後進行查詢以獲得與指定資源相關聯的授權令牌的過期時間。

   - 如果鍵為 `"DEVICEID"` 然後進行查詢以獲取當前設備id。 請注意，此功能預設為禁用，程式設計師應與Adobe聯繫，以獲取有關啟用和費用的資訊。

   - 如果鍵來自以下用戶元資料類型清單，則將包含相應用戶元資料的JSON對象發送到 [`setMetadataStatus()`](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata) 回調函式：

   - `"zip"`  — 郵遞區號

   - `"encryptedZip"`  — 加密的郵遞區號

   - `"householdID"`  — 家庭標識。 如果MVPD不支援子帳戶，則這將與userID相同。

   - `"maxRating"`  — 用戶的最高家長評級

   - `"userID"`  — 用戶標識符。 如果MVPD支援子帳戶，而用戶不是主帳戶，則userID將不同於houselID。

   - `"channelID"`  — 用戶有權查看的頻道清單

   - `"is_hoh"`  — 標識用戶是否是戶主的標誌

   - `"encryptedZip"`  — 加密的郵遞區號

   - `"typeID"`  — 標識用戶帳戶是主/次帳戶的標誌

   - `"primaryOID"`  — 家庭標識

   - `"postalCode"`  — 類似於郵遞區號

   - `"acctID"`  — 帳戶ID

   - `"acctParentID"`  — 帳戶父ID
   **注釋**:程式設計師可用的實際用戶元資料取決於MVPD提供的內容。  請參閱 [用戶元資料](#UserMetadata) 當前可用用戶元資料清單。


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
 

**觸發的回調：** [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)

</br>

[返回頂部](#top)

</br>


## setSelectedProvider(providerid) {#setSelectedProvider}

**描述：** 當用戶從提供方選擇UI中選擇了MVPD以將提供方選擇發送到Access Enabler時調用此函式，或者使用空參數調用此函式，以防用戶在不選擇提供方的情況下取消提供方選擇UI。 

**觸發的回調：**[ setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)。 [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[返回頂部](#top)

</br>

## getSelectedProvider() {#getSelectedProvider}

**描述：** 在提供商選擇對話框中檢索客戶選擇的結果。 在初始身份驗證檢查後，可以隨時使用此選項。

此函式是非同步的，並將其結果返回給 `selectedProvider()` 回調函式。

- **MVPD** 當前選定的MVPD，如果未選擇MVPD，則為空。
- **AE狀態** 當前客戶的驗證結果為「新用戶」、「用戶未驗證」或「用戶已驗證」

 **觸發的回調：** [selectedProvider()](#getselectedprovider-getselectedprovider)

</br>

[返回頂部](#top)

</br>

## 註銷 {#logout}

**描述：** 註銷當前客戶，清除該用戶的所有身份驗證和授權資訊。 從客戶的系統中刪除所有authN和authZ令牌。

 **觸發的回調：** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)
</br> 

[返回頂部](#top)

</br>

## 回調定義 {#calllback-definitions}

您必須實施這些回調來處理對非同步請求調用的響應：

- [entiletLoaded()](#entitlementloaded-entitlementloaded)
- [setConfig()](#setconfigconfigxml-setconfigconfigxml)
- [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders)
- [createIFrame()](#createiframe-createiframeinwidthminheight)
- [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)
- [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)
- [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken)
- [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage)
- [預授權資源()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)
- [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)
- [selectedProvider()](#selectedproviderresult-selectedprovider)

</br>

## entiletLoaded() {#entitlementLoaded}

**描述：** 當Access Enabler完成初始化並準備接收請求時觸發。 實施此回調，以瞭解何時可以啟動與Access Enabler API的通信。
</br>

[返回頂部](#top)

</br>

## setConfig(configXML) {#setconfig(configXML)}

**描述：** 實施此回調以接收配置資訊和MVPD清單。

**參數：**

- *configXML*:xml對象，用於保存當前REQUESTOR（包括MVPD清單）的配置。

 
**觸發者：** [setRequestor()](#setrequestor-inrequestorid-endpoints-optionssetreq)

</br>

[返回頂部](#top)

</br>

## displayProviderDialog（提供程式） {#displayproviderdialog(providers)}

**描述：** 實現此回調以調用您自己的自定義提供程式選擇UI。 對話框應使用顯示名稱（和可選徽標）來提供客戶的選擇。 當客戶選擇並取消對話框後，將呼叫中所選提供商的關聯ID發送給 *setSelectedProvider()*。

**參數：**

- *提供商*  — 表示請求的MVPD的對象陣列：

```JSON
    var mvpd = {
        ID: "someprov",
        displayName: "Some Provider",
        logoURL: "http://www.someprov.com/images/logo.jpg"
    }
```

**觸發者：** [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl)。 [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>[返回頂部](#top)

</br>

## createIFrame(inWidth, inHeight) {#createIFrame(inWidth,inHeight)}

**描述：** 如果用戶選擇了MVPD，而該MVPD需要iFrame來顯示其驗證登錄頁UI，則實施此回調。

**觸發者：**[ setSelectedProvider()](#setselectedproviderproviderid-setselectedprovider)

</br> [返回頂部](#top)

</br>

## setAuthenticationStatus(isAuthenticated, errorCode) {#set-authn-status-isauthn-error}

**描述：** 實施此回調以接收身份驗證狀態（1=authenticated或0=not authenticated），如果嘗試確定身份驗證狀態時出現任何錯誤，則會收到描述性錯誤消息（檢查成功完成時為空字串）。

>[!NOTE]
> 
>如果你用的是當前， [高級錯誤報告](/help/authentication/error-reporting.md) 系統，可以忽略發送到此函式的errorCode參數。  但是，isAuthenticated旗幟仍用於跟蹤權利流中用戶的身份驗證狀態


**參數：**

- *已驗證*  — 提供身份驗證狀態：1（已驗證）或0（未驗證）。
- *錯誤代碼*  — 確定身份驗證狀態時發生的任何錯誤。 空字串（如果沒有）。

 
**觸發者：** [checkAuthentication()](#checkauthn-checkauthn)。 [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl)。 [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid)

</br>

[返回頂部](#top)

</br>

## sendTrackingData(trackingEventType, trackingData) {#sendTrackingData(trackingEventType,trackingData)}

>[!CAUTION]
>
>設備類型和作業系統是通過使用公共Java庫(<http://java.net/projects/user-agent-utils>)和用戶代理字串。 請注意，提供此資訊只是一種將操作度量細分為設備類別的粗略方法，但Adobe不能對不正確的結果負責。 請相應地使用新功能。

**描述：** 實施此回調以在發生特定事件時接收跟蹤資料。 例如，您可以使用此功能跟蹤使用相同憑據登錄的用戶數。 當前無法配置跟蹤。 使用Adobe Primetime驗證1.6, `sendTrackingData()` 還報告有關設備、Access Enabler客戶端和作業系統類型的資訊。 的 `sendTrackingData()` 回調仍然向後相容。\
 
- 設備類型的可能值：
   - 電腦
   - 片
   - 移動
   - 遊戲
   - 未知

- Access Enabler客戶端類型的可能值：
   - html5
   - is
   - 安卓


傳遞事件類型和關聯資訊陣列。 事件類型包括：

| mvpd選擇 | 用戶在提供程式選擇對話框中選擇了MVPD。 |
| ----------------------- | --------------------------------------------------------- |
| 驗證檢測 | 驗證檢查已完成。 |
| 授權檢測 | 授權請求已完成。 |

</br>
資料特定於每個事件類型：
</br>

| 事件類型（字串） | 資料（陣列） |
|:--- | :--- |
| mvpd選擇 | 0:所選MVPD |
|  | 1:設備類型 |
|  | 2:Access Enabler客戶端類型 |
|  | 3:作業系統 |
| 驗證檢測 | 0:令牌請求是否成功(true/false) |
|  | 1:MVPD ID |
|  | 2:GUID |
|  | 3:快取中已有的令牌(true/false) |
|  | 4:設備類型 |
|  | 5:Access Enabler客戶端類型 |
|  | 6:作業系統 |
| 授權檢測 | 0:令牌請求是否成功(true/false) |
|  | 1:MVPD ID |
|  | 2:GUID |
|  | 3:快取中已有的令牌(true/false) |
|  | 4:錯誤 |
|  | 5:詳細資訊 |
|  | 6:設備類型 |
|  | 7:Access Enabler客戶端類型 |
|  | 8:作業系統 |


**觸發者：** [checkAuthentication()](#checkauthn-checkauthn)。 [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl)。 [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid)。 [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>

[返回頂部](#top)

</br>

## setToken(inRequestedResourceID, inToken) {#setToken(inRequestedResourceID,inToken)}

**描述：** 實施此回調以接收已發出授權請求或檢查授權請求且已成功完成的資源(inRequestedResourceID)的短時間媒體令牌(inToken)和ID。

**觸發者：** [checkAuthorization()](#checkAuthZ)。 [getAuthorization()](#getAuthZ)
</br>

[返回頂部](#top)

</br>

## tokenRequestFailed(inRequestedResourceID, inRequestErrorCode, inRequestDetailedErrorMessage) {#token-request-failed-error-msg}

**描述：** 在授權或檢查授權請求失敗時實現此回調。 MVPD可以選擇使用它來提供要由程式設計師顯示的自定義消息。

>[!IMPORTANT]
>
>此回調函式是舊版Mighine驗證錯誤報告系統的一部分。 保留它是為了向後相容，但如果您已使用當前的高級錯誤報告系統實現了自己的回調，則完全不需要使用此函式。 較新的錯誤報告系統提供了有關授權（或其他操作）失敗原因的更詳細資訊，以及針對每種錯誤或警告類型的建議操作過程。

**參數：**

- *inRequestedResourceID*  — 提供授權請求上使用的資源ID的字串。
- *inRequestErrorCode*  — 一個字串，顯示Adobe Primetime驗證錯誤代碼，指明故障原因；可能的值為「User Not Authenticated Error（用戶未驗證錯誤）」和「User Not Authorized Error（用戶未授權錯誤）」；有關詳細資訊，請參閱下面的「回調錯誤代碼」。
- *inRequestDetailedErrorMessage*  — 適用於顯示的附加描述性字串。 如果此描述性字串因任何原因不可用，則Adobe Primetime身份驗證將發送一個空字串 **(&quot;&quot;)**。  MVPD可以使用此功能傳遞自定義錯誤消息或與銷售相關的消息。 例如，如果拒絕訂閱者對資源的授權，MVPD可以使用 `*inRequestDetailedErrorMessage*` 例如： **「您目前沒有訪問您包中的此頻道的權限。 如果要升級軟體包，請按一下\*此處\*。&quot;** 該消息由Adobe Primetime身份驗證通過此回調傳遞到程式設計師站點。 然後程式設計師可以選擇顯示或忽略它。 Adobe Primetime認證也可以 `*inRequestDetailedErrorMessage*` 通知程式設計師可能導致錯誤的條件。 比如說， **&quot;與提供商的授權服務通信時發生網路錯誤&quot;。**

 

**觸發者：**  [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid)。 [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)
</br>

[返回頂部](#top)

</br>


## preauthorizedResources(authorizedResources) {#preauthorizedResources(authorizedResources)}

**描述：** 由Access Enabler觸發的回調，該啟用程式提供在調用後返回的授權資源清單 `checkPreauthorizedResources()`。

**參數：**

- *授權資源*：授權資源清單。

**觸發者：** [checkPreauthorizedResources()](#checkPreauthRes)
</br>

[返回頂部](#top)

</br>

## setMetadataStatus(key, encrypted, data) {#setMetadataStatus(key,encrypted,data)}

**描述：** 由Access Enabler觸發的回調，該啟用程式通過 `getMetadata()` 呼叫。

**更多資訊：** [用戶元資料](#userMetadata)

**參數：**

- *鍵（字串）*:請求所針對的元資料的鍵。
- *加密（布爾型）*:表示是否加密&quot;value&quot;的標誌。 如果為&quot;true&quot;，則&quot;value&quot;實際上將是實際值的JSON Web加密表示。 
- *資料（JSON對象）*:具有元資料表示形式的JSON對象。對於簡單請求(&#39;`TTL_AUTHN`&#39;, &#39;`TTL_AUTHZ`&#39;, &#39;`DEVICEID`&#39;)，結果是字串（表示驗證TTL、授權TTL或設備ID）。 在用戶元資料請求的情況下，結果可以是表示元資料負載的基元對象或JSON對象。 JSON用戶元資料對象的實際結構與以下類似：

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
[返回頂部](#top)

</br>

## selectedProvider（結果） {#selectedProvider(result)}

**描述：** 實施此回調以接收當前選定的MVPD和包裝在 `result` 的下界。 的 `result` 參數是具有以下屬性的對象：

- **MVPD** 當前選定的MVPD，如果未選擇MVPD，則為空。
- **AE\_狀態** 當前用戶、「新用戶」、「用戶未驗證」或「用戶已驗證」之一的驗證結果

 **觸發者：** [getSelectedProvider()](#getSelProv)

</br>

[返回頂部](#top)

</br>

### 回調錯誤代碼 {#callback-error-codes}

| 一般錯誤 |  |
|:--- | :--- | 
| 內部錯誤 | 嘗試處理請求時發生系統錯誤。 |
| 提供程式未選擇錯誤 | 在提供商選擇對話框中取消時發生 |
| 提供程式不可用錯誤 | 當沒有提供程式時發生。 |

| 驗證錯誤 |  |
|:--- | :--- | 
| 常規身份驗證錯誤 | 當原因未知或無法發佈時返回。 |
| 內部身份驗證錯誤 | 嘗試驗證時發生系統錯誤。 |
| 用戶未驗證錯誤 | 未驗證用戶。 |
| 多個身份驗證請求錯誤 | 在完成第一個身份驗證請求之前，已收到其他身份驗證請求。 |

| 授權錯誤 |  |
|:--- | :--- | 
| 常規授權錯誤 | 當原因未知或無法發佈時返回。 |
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

[返回頂部](#top)
