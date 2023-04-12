---
title: 無刷新登錄和註銷
description: 無刷新登錄和註銷
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 0%

---


# 無刷新登錄和註銷 {#tefresh-less-login-and-logout}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 概述 {#overview}

對於Web應用程式，您必須說明一些不同的可能情況，以驗證和註銷用戶。  MVPD需要使用者登入MVPD的網頁以進行驗證，同時還有下列其他因素會生效：

- 有些MVPD需要從您的網站完整重新導向至其登入頁面
- 有些MVPD會要求您在網站上開啟iFrame，以顯示MVPD的登入頁面
- 有些瀏覽器無法妥善處理iFrame案例，因此對於這些瀏覽器而言，更好的替代方案是使用快顯視窗，而非iFrame

在Adobe Primetime身份驗證2.7之前，所有用於驗證用戶的方案都涉及程式設計師頁面的全頁刷新。對於2.7版和後續版本，Adobe Primetime身份驗證團隊改進了這些流程，使得用戶在登錄和註銷期間無需在您的應用程式上經歷頁面刷新。  


## 詳細說明 {#detailed_description}

我們先從原始驗證和註銷流程的摘要開始，然後再從改進的驗證和註銷流程開始。 請注意，前四個區段會處理一般MVPD（非TempPass），而最後一個區段則說明需要套用至TempPass的特殊實施：

- [原始驗證流程](#orig_authn)
- [原始註銷流程](#orig_logout)
- [改進驗證流程](#improved_authn)
- [改善登出流程](#improved_logout)
- [TempPass流](#improved_temppass)

</br>

## 原始驗證/註銷流程 {#orig_authn}

**驗證**

Adobe Primetime驗證Web用戶端有兩種驗證方式，視MVPD需求而定：

1. **全頁重新導向 —** 當用戶從程式設計師網站的MVPD選擇器中選擇提供程式（配置了全頁重定向）後， `setSelectedProvider(<mvpd>)` 在AccessEnabler上叫用，然後將用戶重定向到MVPD的登錄頁。 在用戶提供有效憑據後，將他重定向回程式設計師網站。 AccessEnabler已初始化，並且在Adobe Primetime驗證期間從AccessEnabler中檢索驗證令牌 `setRequestor`.
1. **iFrame /快顯視窗 —** 使用者選取提供者後（以iFrame設定）, `setSelectedProvider(<mvpd>)` 在AccessEnabler上調用。 此動作會觸發 `createIFrame(width, height)` 回撥，通知程式設計師建立一個名稱為的iFrame（或彈出窗口，取決於瀏覽器/首選項） `"mvpdframe"` 和提供的尺寸。 建立iFrame/popup後，AccessEnabler會在iFrame/popup中載入MVPD的登入頁面。 使用者提供有效的認證，而iFrame/popup會重新導向至Adobe Primetime驗證，此驗證會傳回JS程式碼片段，關閉iFrame/popup並重新載入上層頁面（程式設計人員網站）。 與流程1類似，驗證Token也會在 `setRequestor`. 

此 `displayProviderDialog` 回呼(由 `getAuthentication`/`getAuthorization`)會傳回MVPD及其適當設定的清單。 此 `iFrameRequired` MVPD的屬性使程式設計師能夠知道它應該激活流1還是流2。 請注意，程式設計師只需要對流2採取額外的操作（建立iFrame/popup）。

**取消驗證**

此外，使用者也會關閉登入頁面來明確取消驗證流程。 以下是面向程式設計師的方案和建議的解決方案：

1. **全頁重新導向 —** 當登錄頁被關閉時，用戶需要再次導航到程式設計師的網站，並從頭開始整個流程。 在此情況下，程式設計師無需執行任何明確的操作。
1. **iFrame -** 建議程式設計師將iFrame托管在 `div` （或類似的UI元件），其上會附加「關閉」按鈕。 當用戶按下「關閉」按鈕時，程式設計師將銷毀iFrame以及相關的UI並執行 `setSelectedProvider(null)`. 此調用允許AccessEnabler清除其內部狀態，並使用戶能夠啟動後續的驗證流。 `setAuthenticationStatus` 和 `sendTrackingData(AUTHENTICATION_DETECTION...)` 將觸發，以發出驗證流失敗的信號(兩者皆在 `getAuthentication` 和 `getAuthorization`)。
1. **快顯視窗 —** 有些瀏覽器無法準確偵測視窗關閉事件，因此此處需採用不同的方法（與上方的iFrame流量不同）。 Adobe建議程式設計師初始化定期驗證登錄彈出式窗口是否存在的計時器。 如果該窗口不存在，程式設計師可以確保用戶手動取消登錄流程，程式設計師可以繼續調用 `setSelectedProvider(null)`. 觸發回呼與上述流程2中相同。

</br>

## 原始註銷流程 {#orig_logout}

AccessEnabler的註銷API會清除庫的本地狀態，並在當前頁簽/窗口中載入MVPD的註銷URL。 瀏覽器導航到MVPD的註銷終結點，在該過程完成後，將用戶重定向回程式設計師的網站。 代表使用者需要的唯一動作是按下「登出」按鈕/連結，並啟動流程；在MVPD的登出端點上不需要任何使用者互動。

**頁面重新整理時的原始驗證/登出流程**

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AE_with_refresh_web.png)

</br>

## 改進（無刷新）身份驗證 {#improved_authn}

>[!NOTE]
>
>改良的無刷新登入和登出流程要求瀏覽器支援包括Web訊息在內的現代HTML5技術。

上述驗證（登入）和登出流程都會在每個流程完成後重新載入首頁面，以提供類似的使用者體驗。  目前的功能旨在提供無重新整理（背景）登入和登出，以改善使用者體驗。 程式設計師可以通過傳遞兩個布爾標誌(`backgroundLogin` 和 `backgroundLogout`) `configInfo` 參數 `setRequestor` API。 依預設，系統會停用背景登入/登出（這提供與先前實作的相容性）。

**範例：**

```JSON
    var configInfo = {
        callSetConfig: true,
        backgroundLogin: true,
        backgroundLogout: true
    };
    accessEnabler.setRequestor(REQUESTOR_ID, null, configInfo);
```

**驗證**

以下幾點說明原始驗證流程和改進流程之間的轉換：

1. 全頁重新導向會以新的瀏覽器標籤取代，其中會執行MVPD登入。 程式設計師需要建立新頁簽(通過 `window.open`)命名 `mvpdwindow` 使用者選取MVPD時(使用 `iFrameRequired = false`)。 然後程式設計師執行 `setSelectedProvider(<mvpd>)`，允許AccessEnabler在新索引標籤中載入MVPD登入URL。 在用戶提供有效憑據後，Adobe Primetime身份驗證將關閉該頁簽，並向程式設計師網站發送window.postMessage，該網站向AccessEnabler發出驗證流程已完成的信號。 會觸發下列回呼：

   - 如果流由 `getAuthentication`: `setAuthenticationStatus` 和 `sendTrackingData(AUTHENTICATION_DETECTION...)` 會觸發，以發出驗證成功/失敗的訊號。

   - 如果流由 `getAuthorization`: `setToken/tokenRequestFailed` 和 `sendTrackingData(AUTHORIZATION_DETECTION...)` 會觸發，以發出授權成功/失敗的訊號。

1. iFrame/快顯視窗流程大致維持不變，差異在於使用者提供有效認證後，上層頁面將不會重新載入。 iFrame/快顯視窗在登入後會自動關閉，而 `window.postMessage` 將發送到父頁，並通知AccessEnabler流已完成。 觸發的回呼與前一個流量相同， **加上下列新回呼： `destroyIFrame`**. 此 `destroyIFrame` callback允許程式設計師刪除任何與iFrame相關聯/輔助元件，如UI裝飾。 舊的驗證流中不需要存在此回調，因為登錄完成後，Adobe Primetime驗證將重新載入程式設計師的頁面，從而銷毀其上的所有UI元件。

</br>     

>[!IMPORTANT]
> 
>您必須將MVPD登入iFrame或快顯視窗載入為包含AccessEnabler實例的頁面的直接子項。 如果MVPD登錄iFrame或彈出窗口在包含AccessEnabler實例的頁面下方嵌套了兩個或多個級別，則流可能會掛起。 例如，如果首頁面和MVPD iFrame之間有iFrame(Page =\> iFrame =\> MVPD iFrame)，登入流程可能會失敗。

</br>

 **取消驗證**

以下是取消驗證的流程：

1. **瀏覽器標籤 —** 由於索引標籤基本上是新視窗，因此擷取其關閉事件有與舊驗證流程中案例3中討論的相同限制。 此外，在此處無法使用計時器方法，因為無法區分由使用者手動關閉的標籤和在登入流程結束時自動關閉的標籤。 此處的解決方案是，當用戶取消流時，AccessEnabler保持「靜默」（不觸發回叫）。 此外，程式設計師無需採取任何具體操作。 用戶將能夠啟動另一個身份驗證流，而不會收到「多個身份驗證請求錯誤」錯誤（此錯誤已在AccessEnabler中禁用以進行後台登錄）。

1. **iFrame -** 程式設計師可以從舊的驗證流中採用方案2中討論的方法(從iFrame中建立包裝函式UI並觸發相關的「關閉」按鈕 `setSelectedProvider(null)`. 雖然此方法不再是強大需求（如上方案例1所述，允許多個驗證流程進行背景登入），但Adobe仍建議使用此方法。

1. **快顯視窗 —** 這與上方的瀏覽器標籤流程相同。

</br>

## 改善登出流程 {#improved_logout}

新的登出流程將在隱藏的iFrame中執行，從而消除整個頁面重新導向。  這是可能的情況，因為使用者不需要在MVPD的登出頁面上採取特定動作。

登出流程完成後，會將iFrame重新導向至自訂Adobe Primetime驗證端點。 這會提供執行 `window.postMessage` 通知AccessEnabler註銷完成。 會觸發下列回呼： `setAuthenticationStatus()` 和 `sendTrackingData(AUTHENTICATION_DETECTION ...)`，發出使用者不再驗證的信號。 

下圖顯示的無重新整理流程，可讓使用者不重新整理應用程式的首頁，即可登入其MVPD:

**改進（無刷新）驗證/註銷流程**

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AE_with_no_refresh_web.png)

</br>

## TempPass流 {#improved_temppas}

對於TempPass類型的MVPD，不需重新整理的登入會採取不同的方式。

由於TempPass流程要求自動建立視窗並在沒有明確使用者互動的情況下關閉視窗，因此可能會對某些瀏覽器（快顯封鎖程式）造成問題。 因此，AccessEnabler在幕後執行登錄階段，而不需要由程式設計師建立的Web容器。

以下是在實施TempPass以進行無刷新的登錄和註銷時，程式設計師需要注意的方面：

- 開始驗證之前，只需為非TempPass MVPD建立iFrame或快顯視窗。 程式設計師可以通過讀取 `tempPass` MVPD對象的屬性(由 `setConfig()` / `displayProviderDialog()`)。

- 此 `createIFrame()` 回呼必須包含TempPass的檢查，並僅在MVPD為NOT TempPass時執行其邏輯。

- 此 `destroyIFrame()` 回呼必須包含TempPass的檢查，並僅在MVPD為NOT TempPass時執行其邏輯。

- 此 `setAuthenticationStatus()` 和 `sendTrackingData()` 驗證完成後會叫用回呼（完全等同於一般MVPD的無重新整理流程）。

>[!NOTE]
>
>此流僅適用於無刷新的TempPass。 對於重新整理流程，需要明確處理TempPass（當TempPass需要iFrame /快顯視窗時）

</br>

下列程式碼範例示範如何處理程式設計人員網站上的MVPD視窗（適用於一般MVPD和TempPass）:

```javascript
    var aeHostname = "https://entitlement.auth.adobe.com";
    var mvpdWindow = null;
    var mvpd = <mvpd_object_from_displayProviderDialog>;
    var useIframeLogin = <boolean_depending_on_browser_or_Programmer_preferences>;
    var backgroundLogin = <boolean_depending_on_Programmer_preferences>;
     
    // Do not create any windows for refreshless and temp pass
    if (!(backgroundLogin && mvpd.tempPass)) {
        if (backgroundLogin && !mvpd.popup) {
            mvpdWindow = window.open(aeHostname, "mvpdwindow");
        } else if (mvpd.popup && !useIframeLogin) {
            var width = mvpd.width;
            var height = mvpd.height;
            // Center on screen
            var top = (document.all) ? window.screenTop : window.screenY + 100;
            var left = (document.all) ? window.screenLeft : window.screenX + window.innerWidth / 2 - width / 2;
        
            mvpdWindow = window.open(aeHostname, "mvpdframe",
                           "width=" + width + ",height=" + height + ",top=" + top + ",left=" + left);
            // Monitor the mvpd popup for close
            if (!backgroundLogin) {
                clearInterval(cancelTimer);
                cancelTimer = setInterval(function () {
                    if (mvpdWindow && mvpdWindow.closed) {
                        clearInterval(cancelTimer);
                        $('#mvpddiv').hide();
                        accessEnablerAPI.setSelectedProvider(null);
                    }
                }, 200);
            }
        }
    }
```

