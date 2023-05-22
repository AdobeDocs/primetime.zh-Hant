---
title: JavaScript SDK指南
description: JavaScript SDK指南
exl-id: d57f7a4a-ac77-4f3c-8008-0cccf8839f7c
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# JavaScript SDK指南 {#javascript-sdk-cookbook}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 導言(#intro)

本文檔介紹程式設計師的高級應用程式為與Adobe Primetime身份驗證服務整合JavaScript而實施的權利工作流。 到JavaScript API Reference的連結貫穿整個過程。

另請注意 [相關資訊](#related) 節包括指向一組JavaScript代碼示例的連結。

## 權利流(#entitlement)

1. [先決條件](#prereq)
2. [啟動流](#startup)
3. [驗證流](#authn)
4. [授權流](#authz)
5. [查看媒體流](#logout)

</br>

![](assets/javascript-flows.png)


## 先決條件(#prereq)

**依賴項：**

- Adobe Primetime身份驗證庫(AccessEnabler)，與您的Adobe Primetime身份驗證客戶經理合作安排。
- 有效的Adobe Primetime驗證請求者ID，請與Adobe Primetime驗證帳戶經理合作安排。

建立回調函式：

- `entitlementLoaded`

</br>

**觸發器：** AccessEnabler已載入並完成初始化。

- `displayProviderDialog(mvpds)`

   **觸發器：** `getAuthentication(),` 僅當用戶尚未選擇提供程式(MVPD)且尚未驗證時mvpds參數是用戶可用的提供程式陣列。

- `setAuthenticationStatus(status, errorcode)`

   **觸發器：**
   - `checkAuthentication()`每次。
   - `getAuthentication()` 僅當用戶已經過身份驗證並已選擇提供程式時。

   返回的狀態為成功或失敗；錯誤代碼描述了故障類型。

- `createIFrame(width, height)`

   **觸發器：** `setSelectedProvider(providerID)`，僅當選定提供程式配置為在IFrame中顯示時。

   >[!NOTE]
   >
   >提供程式被配置為將其驗證螢幕呈現為重定向或iFrame，程式設計師需要考慮兩者。

- `sendTrackingData(event, data)`

   **觸發器：** `checkAuthentication(), getAuthentication(),checkAuthorization(), getAuthorization(), setSelectedProvider()`。  的 `event` 參數指示發生了哪些權利事件；這樣 `data` 參數是與事件相關的值清單。 
- `setToken(token, resource)`

   **觸發器：** `checkAuthorization()`和 `getAuthorization()` 在成功授權查看資源後。   的 `token` 參數是短壽命的媒體令牌；這樣 `resource` 參數是用戶有權查看的內容。

- `tokenRequestFailed(resource, code, description)`

   **觸發器：**`checkAuthorization()`&#x200B;和`getAuthorization()`  授權失敗。\
   的 `resource` 參數是用戶嘗試查看的內容；這樣 `code` 參數是錯誤代碼，指示出現了哪種類型的故障；這樣 `description` 參數描述與錯誤代碼相關的錯誤。

- `selectedProvider(mvpd)`

   **觸發器：** [`getSelectedProvider()`](#$getSelProv The `mvpd` 參數提供有關用戶選擇的提供程式的資訊。

- `setMetadataStatus(metadata, key, arguments)`

   **觸發器：** `getMetadata().`\
   的 `metadata` 參數提供您請求的特定資料；key參數是 `getMetadata()`請求；和 `arguments` 參數是傳遞給的同一字典 `getMetadata()`。


## 2.啟動流

**我。載入AccessEnabler JavaScript:**

**用於暫存配置檔案**

```JSON
<script type="text/javascript"         
src="https://entitlement.auth-staging.adobe.com/entitlement/v4/AccessEnabler.js">
</script>"
```

或……

**用於生產配置檔案**

```JSON
<script type="text/javascript"         
src="https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js">
</script>"
```

**觸發器：** 初始化完成後，Adobe Primetime驗證將調用 `entitlementLoaded()` 回調函式。 這是您的應用程式與AccessEnabler通信的入口點。 

 
**二。** 呼叫 `setRequestor()`確定程式設計師的身份；程式設計師 `requestorID` 和（可選）一組Adobe Primetime驗證端點。

**觸發器：** 無，但啟用 `displayProviderDialog()` 需要時被叫。


**三。** 呼叫 `checkAuthentication()` 檢查現有驗證而不啟動完整驗證 [認證流]。  如果此調用成功，則可以直接轉到 `authorization flow`。  否則，繼續 `authentication flow`。

**依賴關係：** 成功調用 `setRequestor()`（此依賴關係也適用於所有後續調用）。

 **觸發器：** `setAuthenticationStatus()` 回調

</br>

## 3.驗證流</span>


**依賴關係：** 成功調用 `setRequestor()`（此依賴關係也適用於所有後續調用）。


呼叫 `getAuthentication()` 獲取驗證狀態OR以觸發提供程式驗證流。

**Trigers:**

- `displayProviderDialog()`如果用戶尚未經過身份驗證
- `setAuthenticationStatus()` 如果已進行身份驗證

當AccessEnabler調用時，驗證流的完成 `setAuthenticationStatus()`與 `isAuthenticated == 1`。

## 4.授權流(#authz)

**依賴項：**

- 成功調用 `setRequestor()` （此依賴關係也適用於所有後續調用）。
- 與MVPD一致的有效資源ID。 請注意，資源ID應與在任何其他設備或平台上使用的ID相同，並且在MVPD上應相同。

呼叫 `getAuthorization()` 並傳遞所請求介質的ResourceID。 成功的呼叫將返回短媒體令牌，該令牌確認用戶有權查看請求的媒體。

- 如果呼叫通過：用戶具有有效的AuthN令牌，並且用戶有權監視請求的媒體。
- 如果呼叫失敗：檢查引發的異常以確定其類型（AuthN、AuthZ或其他）:
- 如果調用是AuthN錯誤，則重新啟動AuthN流。
- 如果調用是AuthZ錯誤，則用戶無權監視請求的媒體，應向用戶顯示某種錯誤消息。
- 如果出現其他錯誤（連接錯誤、網路錯誤等） 然後向用戶顯示相應的錯誤消息。

使用媒體令牌驗證器驗證從成功的 `getAuthorization()` 呼叫。

 
**依賴關係：** 短媒體令牌驗證器（隨AccessEnabler庫一起提供）

- 如果驗證通過：顯示/播放用戶請求的媒體。
- 如果失敗：AuthZ令牌無效，應拒絕媒體請求，並應向用戶顯示錯誤消息。

## 5.查看媒體流(#logout)

- 用戶選擇要查看的介質。
   - 介質是否受到保護？\
           — 你的應用會檢查媒體是否受到保護：
      - 如果媒體受到保護，則您的應用將啟動上面的授權(AuthZ)流。
      - 如果介質未受保護，則繼續查看介質流。
      - 播放媒體

## 配置訪問者ID(#visitorID)

配置 [Experience Cloud訪問者ID](https://marketing.adobe.com/resources/help/en_US/mcvid/) 從分析的角度來看，價值非常重要。 一旦設定了EC visitorID值，SDK將隨每個網路呼叫一起發送此資訊，而Adobe Primetime身份驗證服務將收集此資訊。 這樣，您將能夠將來自Adobe Primetime身份驗證服務的分析資料與來自其他應用程式或網站的任何其他分析報告相關聯。 有關如何設定EC visitorID的資訊可以找到 [這裡](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=en)。

 
>[!NOTE]
>
>請注意，從JS SDK 3.1.0版開始，可提供此功能支援。 

<!--
### Related Information (#related)

* [JavaScript SDK Overview](/help/authentication/javascript-sdk-overview.md)
* [JavaScript SDK API Reference](/help/authentication/javascript-sdk-api-reference.md)
* **JavaScript SDK Code Samples**
-->
