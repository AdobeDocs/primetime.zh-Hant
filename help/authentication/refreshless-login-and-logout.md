---
title: 不需重新整理的登入和登出
description: 不需重新整理的登入和登出
exl-id: 3ce8dfec-279a-4d10-93b4-1fbb18276543
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 0%

---

# 不需重新整理的登入和登出 {#tefresh-less-login-and-logout}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 概觀 {#overview}

針對Web應用程式，您必須考慮驗證和登出使用者的某些不同可能情況。  MVPD要求使用者登入MVPD的網頁以進行驗證，並且會涉及到以下其他因素：

- 有些MVPD需要從您的網站完全重新導向至其登入頁面
- 有些MVPD會要求您在網站上開啟iFrame，以顯示MVPD的登入頁面
- 有些瀏覽器無法妥善處理iFrame案例，因此對於這些瀏覽器，更好的選擇是使用快顯視窗而非iFrame

在Adobe Primetime 2.7驗證之前，所有這些驗證使用者的案例都會涉及程式設計師頁面的完整頁面重新整理。對於2.7和後續版本，Adobe Primetime驗證團隊改善了這些流程，讓使用者不必在登入和登出期間在您的應用程式上體驗頁面重新整理。  


## 詳細說明 {#detailed_description}

讓我們從原始驗證和登出流程的摘要開始，然後接著改進驗證和登出流程。 請注意，前四個區段會處理一般MVPD （非TempPass），而最後一個區段則說明需要套用至TempPass的特殊實作：

- [原始驗證流程](#orig_authn)
- [原始登出流程](#orig_logout)
- [已改善驗證流程](#improved_authn)
- [已改善登出流程](#improved_logout)
- [TempPass流程](#improved_temppass)

</br>

## 原始驗證/登出流程 {#orig_authn}

**驗證**

Adobe Primetime驗證Web使用者端有兩種驗證方式，具體取決於MVPD的需求：

1. **整頁重新導向 —** 使用者從程式設計師網站上的MVPD選擇器選取提供者（設定了全頁重新導向）後， `setSelectedProvider(<mvpd>)` 會在AccessEnabler上叫用，使用者會被重新導向至MVPD的登入頁面。 使用者提供有效認證後，系統會將他重新導向回程式設計師的網站。 AccessEnabler已初始化，而且驗證權杖是從Adobe Primetime驗證期間擷取 `setRequestor`.
1. **iFrame/彈出式視窗 —** 使用者選取提供者（以iFrame設定）後， `setSelectedProvider(<mvpd>)` 會在AccessEnabler上叫用。 此動作會觸發 `createIFrame(width, height)` 回呼，通知程式設計師以名稱建立iFrame （或快顯視窗，視瀏覽器/偏好設定而定） `"mvpdframe"` 以及提供的維度。 建立iFrame/彈出式視窗後，AccessEnabler會在iFrame/彈出式視窗中載入MVPD的登入頁面。 使用者提供有效的認證，而iFrame/快顯視窗會重新導向至Adobe Primetime驗證，而後者會傳回JS程式碼片段，進而關閉iFrame/快顯視窗並重新載入上層頁面（程式設計人員網站）。 與流程1類似，驗證權杖是在以下期間擷取： `setRequestor`. 

此 `displayProviderDialog` 回呼(觸發者： `getAuthentication`/`getAuthorization`)會傳回MVPD清單及其適當的設定。 此 `iFrameRequired` MVPD的屬性可讓程式設計師知道它應該啟動流程1還是流程2。 請注意，程式設計師僅需對流程2採取額外動作（建立iFrame/快顯視窗）。

**取消驗證**

此外，在某些情況下，使用者會關閉登入頁面，以明確取消驗證流程。 以下是案例和給程式設計人員的建議解決方案：

1. **整頁重新導向 —** 登入頁面關閉時，使用者需要再次導覽至程式設計師的網站，並從頭開始啟動整個流程。 在此案例中，程式設計人員不需要執行任何明確的動作。
1. **iFrame -** 建議程式設計師將iFrame託管於 `div` （或類似的UI元件）附加了關閉按鈕。 當使用者按下「關閉」按鈕時，程式設計師會毀壞iFrame及相關聯的UI並執行 `setSelectedProvider(null)`. 此呼叫可讓AccessEnabler清除其內部狀態，並讓使用者啟動後續驗證流程。 `setAuthenticationStatus` 和 `sendTrackingData(AUTHENTICATION_DETECTION...)` 將會觸發，以指出失敗的驗證流程（兩者皆開啟） `getAuthentication` 和 `getAuthorization`)。
1. **快顯視窗 —** 有些瀏覽器無法準確偵測視窗關閉事件，因此這裡需要採取不同的方法（與上述iFrame流程相反）。 Adobe建議程式設計師初始化計時器，定期驗證登入快顯視窗是否存在。 如果視窗不存在，程式設計師可以確定使用者手動取消登入流程，並且程式設計師可以繼續呼叫 `setSelectedProvider(null)`. 觸發的回呼與上面流程2中的相同。

</br>

## 原始登出流程 {#orig_logout}

AccessEnabler的登出API會清除程式庫的本機狀態，並在目前的索引標籤/視窗中載入MVPD的登出URL。 瀏覽器會導覽至MVPD的登出端點，在程式完成後，會將使用者重新導向回程式設計人員的網站。 使用者唯一需要執行的動作是按下「登出」按鈕/連結並起始流程；MVPD的登出端點上不需要使用者互動。

**具有頁面重新整理的原始驗證/登出流程**

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AE_with_refresh_web.png)

</br>

## 改善（不需重新整理）驗證 {#improved_authn}

>[!NOTE]
>
>改良的免重新整理登入和登出流程需要瀏覽器支援現代化的HTML5技術，包括網頁傳訊。

上述驗證（登入）和登出流程都可在每個流程完成後重新載入首頁面，以提供類似的使用者體驗。  目前的功能旨在提供不需重新整理（背景）的登入和登出，以改善使用者體驗。 程式設計師可以透過傳遞兩個布林值旗標(`backgroundLogin` 和 `backgroundLogout`)重新命名為 `configInfo` 的引數 `setRequestor` API。 預設會停用背景登入/登出（這樣可提供與先前實作的相容性）。

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

以下幾點說明原始驗證流程與改進流程之間的轉變：

1. 全頁重新導向會以執行MVPD登入的新瀏覽器標籤取代。 程式設計師必須建立新標籤(透過 `window.open`)已命名 `mvpdwindow` 當使用者選取MVPD時(使用 `iFrameRequired = false`)。 然後程式設計師執行 `setSelectedProvider(<mvpd>)`，可讓AccessEnabler在新標籤中載入MVPD登入URL。 使用者提供有效認證後，Adobe Primetime驗證將關閉索引標籤，並傳送window.postMessage至程式設計師的網站，以通知AccessEnabler驗證流程已完成。 系統會觸發下列回呼：

   - 如果流程是由以下人員啟動： `getAuthentication`： `setAuthenticationStatus` 和 `sendTrackingData(AUTHENTICATION_DETECTION...)` 將會觸發，以表示驗證成功/失敗。

   - 如果流程是由以下人員啟動： `getAuthorization`： `setToken/tokenRequestFailed` 和 `sendTrackingData(AUTHORIZATION_DETECTION...)` 將會觸發，以表示授權成功/失敗。

1. iFrame/彈出式視窗流程大多保持不變，差異在於使用者提供有效認證後，不會重新載入上層頁面。 iFrame/快顯視窗會在登入後自動關閉，而且 `window.postMessage` 會傳送至上層頁面，通知AccessEnabler流程已完成。 會觸發與上一個流程相同的回呼， **加上下列新回呼： `destroyIFrame`**. 此 `destroyIFrame` callback可讓程式設計師移除任何相關聯的iFrame/輔助元件，例如UI裝飾。 舊驗證流程中不需要存在此回呼，因為在登入完成後，Adobe Primetime驗證會重新載入程式設計人員的頁面，因此會摧毀該頁面上的所有UI元件。

</br>     

>[!IMPORTANT]
> 
>您必須將MVPD登入iFrame或彈出式視窗載入為包含AccessEnabler執行個體的頁面的直接子系。 如果MVPD登入iFrame或彈出式視窗在包含AccessEnabler執行個體的頁面下方巢狀內嵌兩個或多個層級，則流程可能會擱置。 例如，如果您在主要頁面和MVPD iFrame (Page =\> iFrame =\> MVPD iFrame)之間有iFrame，登入流程可能會失敗。

</br>

 **取消驗證**

以下是取消驗證的流程：

1. **瀏覽器索引標籤 —** 由於索引標籤基本上是新視窗，因此擷取其關閉事件的限制與情境3中從舊驗證流程討論的限制相同。 此外，這裡無法使用計時器方法，因為無法區分使用者手動關閉的標籤和在登入流程結束時自動關閉的標籤。 此處的解決方案是讓AccessEnabler在使用者取消流程時保持「無訊息」（不觸發回呼）。 此外，程式設計師不需要採取任何特定動作。 使用者將能夠啟動另一個驗證流程，而不會收到「多個驗證請求錯誤」錯誤（此錯誤已在背景登入的AccessEnabler中停用）。

1. **iFrame -** 程式設計師可以從舊的驗證流程（從iFrame建立包裝函式UI和觸發的相關「關閉」按鈕）中採取情境2中討論的方法 `setSelectedProvider(null)`. 雖然此方法已不再是強烈的要求（如上述情境1所述，背景登入允許多個驗證流程），但Adobe仍建議使用。

1. **快顯視窗 —** 這等同於上方的「瀏覽器」索引標籤流程。

</br>

## 已改善登出流程 {#improved_logout}

新的登出流程將在隱藏的iFrame中執行，因此會消除完整頁面重新導向。  這是可行的，因為使用者不需要在MVPD的登出頁面上採取特定動作。

登出流程完成後，系統會將iFrame重新導向至自訂Adobe Primetime驗證端點。 這會提供執行 `window.postMessage` 通知父系，通知AccessEnabler登出已完成。 系統會觸發下列回呼： `setAuthenticationStatus()` 和 `sendTrackingData(AUTHENTICATION_DETECTION ...)`，表示使用者已不再驗證。 

下圖顯示不需重新整理的流程，此流程可讓使用者登入其MVPD，而不需重新整理應用程式的首頁：

**改善（不需重新整理）驗證/登出流程**

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AE_with_no_refresh_web.png)

</br>

## TempPass流程 {#improved_temppas}

不需重新整理的登入方式會針對TempPass型別的MVPD採取不同方法。

由於TempPass流程需要自動建立視窗，並在沒有明確使用者互動的情況下關閉，因此可能會對某些瀏覽器（快顯視窗封鎖程式）造成問題。 因此，AccessEnabler會在幕後實作登入階段，而不需要程式設計師建立的Web容器。

以下為程式設計師在實作TempPass以進行不需重新整理的登入和登出時需要注意的事項：

- 在開始驗證之前，只需要為非TempPass MVPD建立iFrame或快顯視窗。 程式設計師可藉由讀取 `tempPass` MVPD物件的屬性(傳回 `setConfig()` / `displayProviderDialog()`)。

- 此 `createIFrame()` callback必須包含TempPass的檢查，且僅在MVPD不是TempPass時執行其邏輯。

- 此 `destroyIFrame()` callback必須包含TempPass的檢查，且僅在MVPD不是TempPass時執行其邏輯。

- 此 `setAuthenticationStatus()` 和 `sendTrackingData()` 在驗證完成後叫用回呼（與正常MVPD的無重新整理流程完全相同）。

>[!NOTE]
>
>此流程僅適用於無重新整理的TempPass。 對於重新整理流程，需要明確處理TempPass （當TempPass需要iFrame/快顯視窗時）

</br>

下列程式碼範例示範如何處理程式設計師網站上的MVPD視窗（適用於一般MVPD和TempPass）：

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
