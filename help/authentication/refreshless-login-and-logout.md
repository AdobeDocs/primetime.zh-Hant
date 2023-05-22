---
title: 無刷新登錄和註銷
description: 無刷新登錄和註銷
exl-id: 3ce8dfec-279a-4d10-93b4-1fbb18276543
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 0%

---

# 無刷新登錄和註銷 {#tefresh-less-login-and-logout}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 概述 {#overview}

對於Web應用程式，您必須考慮一些不同的可能方案，以驗證和註銷用戶。  MVPD要求用戶登錄MVPD的網頁進行身份驗證，同時還要考慮以下附加因素：

- 某些MVPD需要從您的站點到其登錄頁的完全重定向
- 某些MVPD要求您在站點上開啟iFrame以顯示MVPD的登錄頁
- 有些瀏覽器不能很好地處理iFrame方案，因此對於這些瀏覽器來說，更好的選擇是使用彈出窗口而不是iFrame

在Adobe Primetime驗證2.7之前，所有用於驗證用戶的這些方案都涉及程式設計師頁面的全頁刷新。對於2.7和後續版本，Adobe Primetime驗證團隊改進了這些流程，使用戶在登錄和註銷期間無需在您的應用程式上經歷頁面刷新。  


## 詳細說明 {#detailed_description}

讓我們從原始驗證和註銷流的摘要開始，然後使用改進的驗證和註銷流進行。 請注意，前四個部分針對正常MVPD（非TempPass），而最後一個部分介紹需要為TempPass應用的特殊實現：

- [原始驗證流](#orig_authn)
- [原始註銷流](#orig_logout)
- [改進的驗證流](#improved_authn)
- [改進的註銷流](#improved_logout)
- [TempPass流](#improved_temppass)

</br>

## 原始驗證/註銷流 {#orig_authn}

**驗證**

根據MVPD的要求，Adobe Primetime驗證Web客戶端有兩種驗證方法：

1. **全頁重定向 —** 用戶從程式設計師網站的MVPD選取器中選擇提供程式（配置了全頁重定向）後， `setSelectedProvider(<mvpd>)` 在AccessEnabler上調用，並將用戶重定向到MVPD的登錄頁。 在用戶提供有效憑據後，他將重定向回程式設計師網站。 初始化AccessEnabler，在Adobe Primetime驗證期間從AccessEnabler中檢索驗證令牌 `setRequestor`。
1. **iFrame/彈出窗口 —** 在用戶選擇提供程式（配置了iFrame）後， `setSelectedProvider(<mvpd>)` 調用。 此操作將觸發 `createIFrame(width, height)` 回調，通知程式設計師使用名稱建立iFrame（或彈出窗口，具體取決於瀏覽器/首選項） `"mvpdframe"` 和所提供的尺寸。 建立iFrame/popup後，AccessEnabler將在iFrame/popup中載入MVPD的登錄頁。 用戶提供有效的憑據，並將iFrame/popup重定向到Adobe Primetime身份驗證，該身份驗證返回JS片段，該片段關閉iFrame/popup並重新載入父頁（程式設計師網站）。 與流1類似，在 `setRequestor`。 

的 `displayProviderDialog` 回調(觸發 `getAuthentication`/`getAuthorization`)返回MVPD及其相應設定的清單。 的 `iFrameRequired` MVPD的屬性允許程式設計師知道它應激活流1還是流2。 請注意，程式設計師必須僅對流2執行額外操作（建立iFrame/popup）。

**取消身份驗證**

還存在用戶通過關閉登錄頁顯式取消驗證流的情況。 以下是面向程式設計師的方案和建議的解決方案：

1. **全頁重定向 —** 當登錄頁面關閉時，用戶需要再次導航到程式設計師網站並從頭開始啟動整個流。 在此方案中，程式設計師方面不需要明確的操作。
1. **iFrame -** 建議程式設計師在 `div` （或類似的UI元件），其上附加了「關閉」按鈕。 當用戶按「關閉」按鈕時，程式設計師將銷毀iFrame和關聯的UI並執行 `setSelectedProvider(null)`。 此調用允許AccessEnabler清除其內部狀態，並允許用戶啟動後續的驗證流。 `setAuthenticationStatus` 和 `sendTrackingData(AUTHENTICATION_DETECTION...)` 將被觸發，以向失敗的身份驗證流發出信號(兩者都在 `getAuthentication` 和 `getAuthorization`)。
1. **彈出 —** 某些瀏覽器無法準確檢測窗口關閉事件，因此需要採用不同的方法（與上面的iFrame流相比）。 Adobe建議程式設計師初始化計時器，定期驗證登錄彈出窗口是否存在。 如果該窗口不存在，則程式設計師可以確保用戶手動取消登錄流，並且程式設計師可以繼續調用 `setSelectedProvider(null)`。 觸發的回調與上文的流2中相同。

</br>

## 原始註銷流 {#orig_logout}

AccessEnabler的註銷API將清除庫的本地狀態，並在當前頁籤/窗口中載入MVPD的註銷URL。 瀏覽器導航到MVPD的註銷終結點，並在該過程完成後，將用戶重定向回程式設計師網站。 代表用戶需要的唯一操作是按「註銷」按鈕/連結並啟動流；在MVPD的註銷終結點上不需要用戶交互。

**具有頁面刷新的原始驗證/註銷流**

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AE_with_refresh_web.png)

</br>

## 改進（無刷新）身份驗證 {#improved_authn}

>[!NOTE]
>
>改進的無刷新登錄和註銷流程要求瀏覽器支援包括web消息傳遞在內的現代HTML5技術。

上述驗證（登錄）和註銷流都通過在每個流完成後重新載入首頁，提供了類似的用戶體驗。  當前功能旨在通過提供無刷新（後台）登錄和註銷來改善用戶體驗。 程式設計師可以通過傳遞兩個布爾標誌(`backgroundLogin` 和 `backgroundLogout`) `configInfo` 參數 `setRequestor` API。 預設情況下，後台登錄/註銷會被禁用（這提供了與先前實現的相容性）。

**示例：**

```JSON
    var configInfo = {
        callSetConfig: true,
        backgroundLogin: true,
        backgroundLogout: true
    };
    accessEnabler.setRequestor(REQUESTOR_ID, null, configInfo);
```

**驗證**

以下幾點描述了原始驗證流和改進流之間的轉換：

1. 全頁重定向替換為執行MVPD登錄的新瀏覽器頁籤。 程式設計師需要建立新頁籤(通過 `window.open`已命名 `mvpdwindow` 當用戶選擇MVPD時(使用 `iFrameRequired = false`)。 然後程式設計師執行 `setSelectedProvider(<mvpd>)`，允許AccessEnabler在新頁籤中載入MVPD登錄URL。 在用戶提供有效憑據後，Adobe Primetime驗證將關閉該頁籤，並向程式設計師網站發送window.postMessage，該網站向AccessEnabler發出驗證流已完成的信號。 觸發以下回調：

   - 如果流由 `getAuthentication`: `setAuthenticationStatus` 和 `sendTrackingData(AUTHENTICATION_DETECTION...)` 將被觸發以發出成功/失敗驗證信號。

   - 如果流由 `getAuthorization`: `setToken/tokenRequestFailed` 和 `sendTrackingData(AUTHORIZATION_DETECTION...)` 將被觸發以發出成功/失敗授權信號。

1. iFrame /彈出窗口流基本保持不變，其區別在於，在用戶提供有效憑據後，將不重新載入父頁。 iFrame/彈出窗口將在登錄後自動關閉， `window.postMessage` 將發送到父頁，並通知AccessEnabler流已完成。 觸發的回調與前一個流相同， **加上以下新回調： `destroyIFrame`**。 的 `destroyIFrame` 回調允許程式設計師刪除任何與iFrame關聯的/輔助元件，如UI裝飾。 舊身份驗證流中不需要存在此回調，因為在登錄完成後，Adobe Primetime身份驗證將重新載入程式設計師頁面，從而破壞其上的所有UI元件。

</br>     

>[!IMPORTANT]
> 
>必須將MVPD登錄iFrame或彈出窗口作為包含AccessEnabler實例的頁的直接子窗口載入。 如果MVPD登錄iFrame或彈出窗口在包含AccessEnabler實例的頁面下方嵌套了兩個或兩個以上級別，則流可能會掛起。 例如，如果在首頁和MVPD iFrame之間有iFrame（頁=\> iFrame =\> MVPD iFrame），則登錄流可能會失敗。

</br>

 **取消身份驗證**

以下是取消身份驗證的流：

1. **瀏覽器頁籤 —** 由於該頁籤基本上是一個新窗口，因此捕獲其關閉事件具有與方案3中從舊身份驗證流中討論的相同限制。 此外，在此不可能採用計時器方法，因為無法區分用戶手動關閉的頁籤和登錄流結束時自動關閉的頁籤。 此處的解決方案是，當用戶取消流時，AccessEnabler保持「靜默」（未觸發回調）。 此外，程式設計師不需要採取任何具體行動。 用戶將能夠啟動另一個身份驗證流，而不會收到「多個身份驗證請求錯誤」錯誤（此錯誤已在AccessEnabler中禁用，用於後台登錄）。

1. **iFrame -** 程式設計師可以從舊的驗證流中採用方案2中討論的方法(從iFrame建立包裝器UI並使用觸發器的關聯關閉按鈕 `setSelectedProvider(null)`。 儘管此方法不再是一項強大要求（如上面的方案1所述，允許多身份驗證流用於後台登錄），但Adobe仍建議使用這種方法。

1. **彈出 —** 這與上面的「瀏覽器」頁籤流相同。

</br>

## 改進的註銷流 {#improved_logout}

新的註銷流將在隱藏的iFrame中執行，從而消除了全頁重定向。  這是可能的，因為用戶不需要在MVPD的註銷頁面上執行特定操作。

註銷流程完成後，它將將iFrame重定向到自定義Adobe Primetime身份驗證終結點。 這將提供執行 `window.postMessage` 通知AccessEnabler註銷已完成。 觸發以下回調： `setAuthenticationStatus()` 和 `sendTrackingData(AUTHENTICATION_DETECTION ...)`，指示用戶不再經過身份驗證。 

下圖顯示了無刷新流，該流使用戶能夠登錄到其MVPD而不刷新應用程式的首頁：

**改進（無刷新）驗證/註銷流**

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AE_with_no_refresh_web.png)

</br>

## TempPass流 {#improved_temppas}

對於TempPass類型的MVPD，無刷新登錄採用不同的方法。

由於TempPass流要求自動建立窗口，並在沒有顯式用戶交互的情況下關閉窗口，因此可能會對某些瀏覽器（彈出式攔截器）造成問題。 因此，AccessEnabler在幕後實現登錄階段，而不需要程式設計師建立的Web容器。

以下是在實施TempPass以進行無刷新登錄和註銷時程式設計師需要注意的方面：

- 在啟動身份驗證之前，只需為非TempPass MVPD建立iFrame或彈出窗口。 程式設計師可通過讀取 `tempPass` MVPD對象的屬性(返回者 `setConfig()` / `displayProviderDialog()`)。

- 的 `createIFrame()` 回調必須包含對TempPass的檢查，並且僅當MVPD為NOT TempPass時才執行其邏輯。

- 的 `destroyIFrame()` 回調必須包含對TempPass的檢查，並且僅當MVPD為NOT TempPass時才執行其邏輯。

- 的 `setAuthenticationStatus()` 和 `sendTrackingData()` 驗證完成後調用回調（與普通MVPD的無刷新流完全相同）。

>[!NOTE]
>
>此流僅可用於無刷新的TempPass。 對於刷新流，需要顯式處理TempPass（當TempPass需要iFrame /彈出窗口時）

</br>

以下代碼示例演示了如何處理程式設計師網站上的MVPD窗口（適用於普通MVPD和TempPass）:

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
