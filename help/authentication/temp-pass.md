---
title: 臨時通道
description: 臨時通道
exl-id: 1df14090-8e71-4e3e-82d8-f441d07c6f64
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '2210'
ht-degree: 0%

---

# 臨時通道 {#temp-pass}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 功能摘要 {#tempass-featur-summary}

臨時通行證允許程式設計師為沒有MVPD帳戶憑據的用戶提供對其受保護內容的臨時訪問。  臨時傳遞包括以下功能：

* 臨時通行證可配置為提供臨時訪問，以涵蓋各種情形，包括：
   * 程式設計師可以每天提供其一個站點的簡短（例如10分鐘的預覽）。
   * 程式設計師可以為大型體育賽事（如奧運會）或NCAA March Maxids提供單個、長時間的演示（例如，4小時）。
   * 程式設計師可以提供前兩種方案的組合；例如，在某一天開始的較長查看期間，然後是連續的短期間，每天重複某些後續天數。
* 程式設計師指定其臨時傳遞的持續時間（生存時間或TTL）。
* 每個請求者都運行臨時通過。  例如，NBC可以為請求者「NBCOlympics」設定4小時的Temp Pass。
* 程式設計師可以重置授予特定請求者的所有令牌。  用於實施臨時傳遞的「臨時MVPD」必須配置為啟用「每個請求者的身份驗證」。
* **向特定設備上的單個用戶授予臨時通過訪問權限**。 在用戶的臨時通過訪問過期後，該用戶將無法在同一設備上獲得臨時訪問，直到該用戶過期 [授權令牌](/help/authentication/glossary.md#authz-token) 已從Adobe Primetime驗證伺服器中清除。


>[!NOTE]
>
>臨時傳遞是高級工作流包的一部分。 如果有興趣使用此功能，請與您的黃金時段銷售代表聯繫。

## 功能詳細資訊 {#tempass-featur-details}

* **查看時間的計算方式**  — 臨時通行證的有效時間與用戶在程式設計師應用程式上查看內容所花費的時間無關。  在通過臨時通道對初始用戶進行授權請求時，通過將初始當前請求時間添加到由程式設計師指定的TTL來計算到期時間。 該過期時間與用戶的設備ID和程式設計師的請求者ID相關聯，並儲存在黃金時段驗證資料庫中。 每次用戶嘗試使用來自同一設備的臨時傳遞訪問內容時，黃金時段驗證將比較伺服器請求時間與與用戶設備ID和程式設計師請求者ID相關聯的過期時間。 如果伺服器請求時間小於到期時間，則授予授權；否則，將拒絕授權。
* **配置參數**  — 程式設計師可以指定以下Temp Pass參數以建立Temp Pass規則：
   * **令牌TTL**  — 允許用戶在不登錄MVPD的情況下觀看的時間。 此時間基於時鐘，並且無論用戶是否正在監視內容都會過期。
   >[!NOTE]
   >請求者ID不能有多個與其關聯的臨時通過規則。
* **驗證/授權**  — 在「臨時傳遞」流中，將MVPD指定為「臨時傳遞」。  黃金時間驗證不會與臨時傳遞流中的實際MVPD通信，因此「臨時傳遞」MVPD將授權任何資源。 程式設計師可以指定一個可使用Temp Pass訪問的資源，就像他們對其站點上的其他資源所做的那樣。 媒體驗證程式庫可以像往常一樣用於驗證臨時傳遞短媒體令牌並在播放前強制執行資源檢查。
* **跟蹤臨時通道流中的資料**  — 在臨時通過權利流程期間跟蹤資料的兩點：
   * 從黃金時段身份驗證傳遞到您的跟蹤ID **sendTrackingData()** 回調是設備ID的哈希。
   * 由於「臨時通過」流中使用的MVPD ID為「臨時通過」，因此相同的MVPD ID將傳回給 **sendTrackingData()**。 大多數程式設計師可能希望將Temp Pass度量與實際MVPD度量區別對待。 這需要在分析實施中做一些額外工作。

下圖顯示了「溫度通過」流：

![臨時通道流](assets/temp-pass-flow.png)

*圖：臨時通道流*

## 實施臨時通過 {#implement-tempass}

在黃金時段驗證端，通過向參與的程式設計師伺服器配置添加名為「TempPass」的偽MVPD來實現Temp Pass。  此偽MVPD的作用類似於臨時授予對程式設計師受保護內容的訪問權限的實際MVPD。

在程式設計師端，MVPD用於驗證的兩種方案將按照如下方式實現臨時通道：

* **程式設計師頁面上的iFrame**。 無論MVPD的身份驗證類型如何，臨時傳遞都有效，但對於iFrame方案，需要執行其他步驟來取消當前身份驗證流並使用臨時傳遞進行身份驗證。 這些步驟如 [iFrame登錄](/help/authentication/temp-pass.md) 下。
* **重定向到MVPD登錄頁**。 在較傳統的情況下，在使用MVPD啟動身份驗證之前顯示用於觸發臨時通道的UI，無需執行特殊步驟。 應將臨時通過視為常規MVPD。

以下幾點適用於兩個實施方案：

* 「臨時通過」只應顯示在MVPD選取器中，用於尚未請求臨時通過授權的用戶。 通過在Cookie上保留標誌，可以阻止後續請求的顯示。 只要用戶未清除瀏覽器快取，該操作就會生效。 如果用戶清除其瀏覽器快取，則「臨時通過」將再次顯示在選取器中，用戶將能夠再次請求。 僅當「臨時通過」時間尚未過期時，才授予訪問權限。
* 當用戶通過臨時傳遞請求訪問時，黃金時段身份驗證伺服器在身份驗證過程中將不會執行其通常的安全斷言標籤語言(SAML)請求。 相反，在令牌對設備有效時，每次調用驗證終結點時，該終結點將返回成功。
* 當臨時傳遞過期時，其用戶將不再被驗證，因為在臨時傳遞流中，驗證令牌和授權令牌具有相同的過期日期。 為了向用戶解釋其臨時通過已過期，程式設計師必須在調用後立即檢索所選MVPD `setRequestor()`，然後調用 `checkAuthentication()` 一如往常。 在 `setAuthenticationStatus()` 回調可以進行檢查，以確定auth狀態是否為0，這樣，如果所選MVPD為「TempPass」，則可以向其Temp Pass會話已過期的用戶顯示消息。
* 如果用戶在到期前刪除臨時傳遞令牌，則後續的權利檢查將生成一個TTL等於剩餘時間的令牌。
* 如果用戶在過期後刪除Temp Pass令牌，則後續權利檢查將返回「用戶未授權」。

請參閱中的示例 [示例代碼](/help/authentication/temp-pass.md#tempass-sample-code) 下面是如何對本節中介紹的實現詳細資訊進行編碼的示例。

## 示例代碼 {#tempass-sample-code}

以下各節說明如何調用黃金時段驗證API以實現臨時傳遞流：

* [iFrame登錄示例](/help/authentication/temp-pass.md#iframe-login-sample)
* [自動登錄示例](/help/authentication/temp-pass.md#auto-login-sample)

### iFrame登錄示例 {#iframe-login-sample}

此示例說明如何為MVPD支援iFrame整合的情況實施Temp Pass:

```HTML
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
        "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
    <title>Temp Pass Sample</title>
    <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
    <script type="text/javascript" src="https://raw.github.com/carhartl/jquery-cookie/master/jquery.cookie.js"></script>
    <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js"></script>
 
    <script type="text/javascript">
        var ae, ifrm, providersMenu, previousSelectedProvider;
        var tempassSelected = false;
 
        $(document).ready(function() {
            ifrm = $('#ifrm');
            swfobject.embedSWF("http://entitlement.auth.adobe.com/entitlement/AccessEnablerDebug.swf"
                    , "ae", "1", "1", "11.0.0", "expressinstall.swf", {}
                    , {wmode: "transparent", allowScriptAccess: "always"}
                    , {id: "accessEnabler", name: "accessEnabler"});
        });
 
        function swfLoaded() {
            ae = $('#accessEnabler')[0];
            ae.setProviderDialogURL("none");
            ae.setRequestor("sample_requestor_Id");
            previousSelectedProvider = ae.getSelectedProvider(); 
            ae.checkAuthentication();
        }
 
        function createIFrame() {
            providersMenu.hide();
 
            // If the user already used TempPass once, hide the button
            if ($.cookie("TPSelected") == "1"){
                $('#tempassBtn').hide();
            }
            ifrm.show();
        }
 
        function displayProviderDialog(providers) {
            if (tempassSelected) {
                // Remember in a cookie that the user selected temp pass
                $.cookie("TPSelected", "1", {expires: 366, path: '/'});
 
                // Authenticate with temp pass
                ae.setSelectedProvider("TempPass");
            } else {
                $('#loginBtn').hide();
                providersMenu = $('<select></select>');
 
                providersMenu.change(function(event){
                    ae.setSelectedProvider(event.target.value);
                });
 
                $.each(providers, function(k, v) {
                    // Add the MVPDs to the menu while making
                    //   sure that the Temp Pass entry is skipped
                    if(v.ID != "TempPass") {
                        providersMenu.append($('<option></option>', {value:v.ID}).text(v.displayName));                       
                    }
                });
                $('body').append(providersMenu);
            }
        }
 
        function setAuthenticationStatus(status, code) {
            loginBtn = $('#loginBtn');
            logoutBtn = $('#logoutBtn');
            console.log(previousSelectedProvider);
 
            if (status == 1) {
                $('#selectedProvider').text("Authenticated with " + ae.getSelectedProvider().MVPD + "   ");
                loginBtn.hide();
                logoutBtn.show();
 
                // Get authorization
                ae.getAuthorization("sample_requestor_Id");
            } else {
                // If selected provider is TempPass but the user is not authenticated,
                //   infer that the TempPass period has expired, so reset the MVPD selection
                if (previousSelectedProvider && previousSelectedProvider.MVPD == "TempPass") {
                    previousSelectedProvider = null;
                    ae.setSelectedProvider(null);
                    alert("Your Temp Pass has expired, please login with your regular cable provider!");
                }
                loginBtn.show();
                logoutBtn.hide();
            }
        }
 
        function selectTempPass() {
            ifrm.hide();
 
            // Signal the fact that the user selected temp pass
            tempassSelected = true;
 
            // Cancel the current authentication flow
            ae.setSelectedProvider(null);
 
            // Retry authentication
            ae.getAuthentication();
 
        }
    </script>
</head>
<body>
    <button id="loginBtn" style="display: none" onclick="ae.getAuthentication();">Login</button>
    <label id="selectedProvider" for="logoutBtn"></label><button id="logoutBtn"
           style="display: none" onclick="ae.logout()">Logout</button>
    <div id="ifrm"
         style="display: none; position: absolute; top: 50px; left:50px; width: 400px; height: 400px; border: 2px solid red;">
        <button id="tempassBtn"
           onclick="selectTempPass();"
             style="float:left">Don't know your credentials? Click here to get a Temp Pass.
        </button>
        <button onclick="window.location.reload()" style="float:right">X</button>
        <br />
        <hr />
        <iframe src="about:blank" id="mvpdframe" name="mvpdframe" width="90%" height="90%" frameborder="0"></iframe>
    </div>
    <br/>
    <div id="ae" style="display: none">
        <p>Loading Access Enabler...</p>
    </div>
</body>
</html>
```

#### iFrame登錄使用案例 {#iframe-login-use-cases}

**要首次請求臨時傳遞，請執行以下操作：**

1. 用戶訪問「程式設計師」頁面並按一下登錄連結。
1. MVPD選取器開啟，用戶從清單中選擇MVPD。
1. 將顯示驗證iFrame。 此iFrame包含「臨時通過」連結。
1. 用戶按一下「臨時通過」，因此程式設計師會向cookie添加一個標誌，以防止用戶在隨後訪問該頁面時看到「臨時通過」連結。
1. 臨時傳遞認證請求到達黃金時段認證伺服器，並且它們生成認證令牌。 TTL等於程式設計師為臨時通道設定的時間段。
1. 臨時通過授權請求到達黃金時段認證伺服器。
1. 黃金時段認證伺服器從請求中提取設備和請求者ID，並將它們連同到期時間一起儲存在資料庫中。 到期時間計算為：初始臨時傳遞請求時間加上TTL（由程式設計師指定）。
1. 黃金時段認證伺服器生成授權令牌。
1. 用戶訪問受保護的內容。

**要在返回的臨時通過用戶刪除瀏覽器cookie後再次請求臨時通過：**

1. 用戶訪問「程式設計師」頁面並按一下登錄連結。
1. MVPD選取器開啟，用戶從清單中選擇MVPD。
1. 將顯示驗證iFrame。 此iFrame包含一個「臨時通過」連結（用戶刪除了原始cookie，因此程式設計師不知道用戶之前是否按一下了「臨時通過」連結）。
1. 用戶再次按一下「臨時通過」，因此程式設計師會再次向cookie添加標誌，以防止用戶在隨後訪問該頁面時看到「臨時通過」連結。
1. 臨時傳遞認證請求到達黃金時段認證伺服器，其生成認證令牌。 TTL現在是臨時通道的剩餘時間（當前時間與與設備ID關聯的到期時間之差）。
1. 臨時通過授權請求到達黃金時段認證伺服器。
1. 黃金時段認證伺服器從請求中提取設備和請求者ID，並使用它們從黃金時段認證資料庫中檢索到期時間。 將當前時間與到期時間進行比較。
1. 如果用戶的臨時通過尚未過期，則黃金時段驗證伺服器將生成授權令牌。
1. 如果用戶的臨時通過未過期，則用戶將能夠訪問受保護的內容。

### 自動登錄示例 {#auto-login-sample}

以下示例說明了在訪問站點時用戶自動使用TempPass登錄的情況。 用戶可以隨時選擇使用常規MVPD登錄，如果TempPass已過期，將發出警告：

```HTML
<html>
<head>
    <title>Temp Pass Sample</title>
    <script type="text/javascript"
             src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
    <script type="text/javascript"
             src="https://raw.github.com/carhartl/jquery-cookie/master/jquery.cookie.js"></script>
    <script type="text/javascript"
             src="http://ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js"></script>
 
    <script type="text/javascript">
        var REQUESTOR = "REF";
        var RESOURCE = "sample_requestor_Id";
        var selectedProvider = null;
        var mvpds;
        var hasTempPassMVPD = false;
 
        // Used to cache the mvpd picker
        var picker;
 
        $(document).ready(function() {
            swfobject.embedSWF("http://entitlement.auth.adobe.com/entitlement/AccessEnablerDebug.swf"
                    , "ae", "1", "1", "11.0.0", "expressinstall.swf", {}
                    , {allowScriptAccess: "always"}
                    , {id: "accessEnabler", name: "accessEnabler"});
        });
 
        function swfLoaded(){
            console.log("AccessEnabler loaded");
            ae = $('#accessEnabler')[0];
 
            // Make sure the default picker is disabled
            ae.setProviderDialogURL("none");
 
            ae.setRequestor(REQUESTOR);
            ae.checkAuthentication();
        }
 
        /**
         * Callback received as a result of setRequestor()
         *
         * @param xml object holding the configuration for the current REQUESTOR
         * including the MVPD list
         */
        function setConfig(config) {
            // Save the mvpd list
            var mvpdList = $.parseXML(config);
            mvpds = $(mvpdList).find('mvpd');
 
            // Create the picker only once and cache it
            if(!picker) {
                picker = $('<div id="mvpdPicker"/>');
 
                var providersMenu = $('<select id="mvpdList" multiple></select>');
 
                $.each(mvpds, function(k, v) {
                    var mvpdID = $(v).find("id").text();
                    var mvpdName = $(v).find("displayName").text();
 
                    // Add the mvpd's to the menu while making
                    //   sure that the Temp Pass entry is skipped
                    if (mvpdID != "TempPass") {
                        providersMenu.append($('<option></option>', {value:mvpdID}).text(mvpdName));
                    } else {
                        hasTempPassMVPD = true;
                    }
                });
                picker.append(providersMenu);
                picker.append($('<br/>'));
                picker.append($('<input type="button" onclick="login()" value="login" />'));
                picker.append($('<input type="button" onclick="cancelPicker()" value="cancel" />'));                  
            }
 
            if (!hasTempPassMVPD) {
                $('#selectedProvider').html("FATAL ERROR: TempPass is not integrated with '" +
                  REQUESTOR + "'<br />This sample is valid only for sites integrated with TempPass !!!");             
            }
        }
 
        /**
         * Callback triggered for iFramed MVPD's
         */
        function createIFrame() {
            $('#mvpdPicker').remove();
            $('#ifrm').show();
        }
 
        /**
         * Hides the MVPD picker
         * when the user clicks "Cancel"
         */
        function cancelPicker() {
            $('#video').show();
            $('#mvpdPicker').remove();
            $('#loginBtn').show();
        }
 
        /**
         * Pops up the MVPD picker
         */
        function showPicker() {
            $('#video').hide();
            $('#loginBtn').hide();
            $('body').append(picker);
        }
 
        function logout() {
            $.removeCookie('tempPassUsed');
            ae.logout();
        }
 
        /**
         * Performs login with the selected MVPD
         */
        function login() {
            selectedProvider = $('#mvpdList').val()[0];
 
            // Make sure we clear out previously
            // selected. This is a must if we want to force
            // login with a real MVPD while still logged in with
            // TempPass, without doing an ae.logout()
            ae.setSelectedProvider(null);
            ae.getAuthentication();
        }

        /**
         * Callback triggered by AccessEnabler. This is usually
         * triggered in order to display the MVPD picker, but
         * since we already constructed, cached, and displayed the
         * picker, and the user already picked the MVPD, we don't need
         * to do anything here but state management
         */
        function displayProviderDialog() {
            // If the selected MVPD is TempPass
            // store this fact in a cookie,
            // otherwise clear it
            if (selectedProvider != 'TempPass') {
                $.removeCookie('tempPassUsed');
            } else {
                $.cookie("tempPassUsed", 1);
            }
 
            // Since the picker was already shown
            // and the user picked an MVPD,
            // just proceed to login
            ae.setSelectedProvider(selectedProvider);
        }
 
        function setAuthenticationStatus(status, code) {
            if (!hasTempPassMVPD) {
                $('#selectedProvider').html("FATAL ERROR: TempPass is not integrated with '" +
                  REQUESTOR + "'<br />This sample is valid only for sites integrated with TempPass !!!");
            } else if(status == 1) {
                selectedProvider = ae.getSelectedProvider().MVPD;
                $('#selectedProvider').text("Authenticated with " + selectedProvider + "   ");
 
                // If authenticated with TempPass
                // allow the user to login with
                // a real MVPD
                if (selectedProvider == "TempPass") {
                    $('#loginBtn').show();
                    $('#logoutBtn').hide();
                } else {
                    $('#loginBtn').hide();
                    $('#logoutBtn').show();
                }
 
                // Get authorization
                // Note: This is mandatory in order to "start" the temp pass countdown
                ae.checkAuthorization(RESOURCE);
            } else if(code != "Provider not Selected Error") {
                // Auto-authenticate with TempPass only if we infer
                // that TempPass has not expired, otherwise we
                // inform the user that TempPass has expired
                if ($.cookie('tempPassUsed') == 1) {
                   $('#selectedProvider').text("Your Temp Pass has expired, please log in with your cable provider!");
                   $('#logoutBtn').show();
                   showPicker();
                } else {
                    selectedProvider = 'TempPass';
                    ae.getAuthentication();
                }
            }
        }
 
        /**
         * Displays the picker as a result
         * of user action
         */
        function loginClicked() {
            $('#loginBtn').hide();
            showPicker();
        }
 
        /**
         * Callback triggered in case of authorization success
         */
        function setToken(token) {
            console.log(token);
            $('#video').html('<img src=">');
        }
 
        /**
         * Callback triggered in case of authz failure
         */
        function tokenRequestFailed(resource, status, message) {
            console.log(resource);
            $('#video').html('<p style="color: red">' + status + ': ' + message + '</p>');
        }
 
    </script>
</head>
<body>
    <button id="loginBtn" style="display: none" onclick="loginClicked()">Login</button>
    <label id="selectedProvider" for="logoutBtn"></label><button id="logoutBtn"
        style="display: none" onclick="logout()">Logout</button>
    <div id="ifrm"
         style="display: none; position: absolute; top: 50px; left:50px;
         width: 400px; height: 400px; border: 2px solid red;">
        <button onclick="window.location.reload()" style="float:right">Close this window</button>
        <br /><hr />
        <iframe src="about:blank" id="mvpdframe" name="mvpdframe" width="80%" height="80%" frameborder="0"></iframe>  
    </div>
    <br/>
 
    <div id="video"></div>
    <div id="ae" style="display: none"><p>Loading Access Enabler...</p></div>
</body>
</html>
```

## 使用多個臨時刀路 {#use-mult-tempass}

某些事件要求對內容進行分階段的免費訪問，如初始的免費訪問間隔（如4小時），然後是每日免費訪問（如，後續每天10分鐘）。  為了使程式設計師能夠實施此方案，他們必須與Adobe聯繫人一起安排該方案，以便為程式設計師配置兩個臨時MVPD。

對於此示例方案（初始4小時免費會話，然後是每天10分鐘免費會話）Adobe配置名為TempPass1的MVPD，其生存時間(TTL)為4小時，而TempPass2的TTL為10分鐘。  這兩者都與程式設計師的請求者ID關聯。

### 程式設計師實施 {#mult-tempass-prog-impl}

在Adobe配置兩個TempPass實例後，另外兩個MVPD（TempPass1和TempPass2）將出現在程式設計師的MVPD清單中。  程式設計師需要採取以下步驟來實施多個臨時通道：

1. 在用戶對站點的初始訪問時，使用TempPass1自動登錄這些站點。 您可以將上面的自動登錄示例用作此任務的起點。
1. 檢測到TempPass1已過期時，請將事實儲存（在cookie/本地儲存中），並向用戶提供標準MVPD選取器。 **確保從該清單中篩選出TempPass1和TempPass2**。
1. 在後續的每天，如果TempPass1已過期，則使用TempPass2自動登錄該用戶。
1. 當TempPass2過期時，將事實（儲存在cookie/本地儲存中）儲存當天，並向用戶顯示標準MVPD選取器。 同樣，請確保從該清單中篩選出TempPass1和TempPass2。
1. 在每個新日00:00小時，使用 [重置TempPass Web API](/help/authentication/temp-pass.md#reset-all-tempass)。

>[!NOTE]
>**寫程式說明：** 黃金時段身份驗證沒有在10分鐘過後停止免費流的內置機制。  一旦TempPass2過期，程式設計師將限制訪問。 為此，程式設計師可以在其站點/應用中每X分鐘實施一次「checkAuthorization」調用，其中X是程式設計師確定對其應用有意義的時間段。

## 重置所有臨時刀路 {#reset-all-tempass}

某些業務規則要求定期清除臨時通行，或對為特定請求者ID和MVPD ID頒發的所有臨時通行進行臨時重置。 此功能支援以下使用情形：

* 每天10分鐘的臨時通道（必須在一天的開始時重置臨時通道）
* 在突發新聞期間，所有用戶都可以使用臨時通過。 （一旦突發新聞開始，需要為所有設備重置臨時通道。）
* 提供初始查看時段的某個長度，然後是後續日時段的另一個長度的組合的多個「臨時通過」方案。

為了重置所有臨時傳遞，Mogine身份驗證為程式設計師提供 *公共* Web API:

```url
DELETE https://mgmt.auth.adobe.com/reset-tempass/v2/reset
```

>[!NOTE]
>上面的URL將取代以前的重置API。 不再支援舊的重置API(v1)。

* **協定：** HTTPS
* **主機：**
   * 版本 — mgmt.auth.adobe.com
   * Prequal - mgmt-prequal.auth.adobe.com
* **路徑：** /reset tempass/v2/reset
* **查詢參數：** `device_id=all&requestor_id=REQUESTOR_ID&mvpd_id=TEMPPASS_MVPD_ID`
* **標題：** ApiKey - 1232293681726481
* **響應：**
   * 成功 — HTTP 204
   * 失敗：
      * HTTP 400請求不正確
      * 如果未指定ApiKey，則HTTP 401
      * ApiKey無效時的HTTP 403

例如：

```curl
$ curl -H "Authorization: Bearer <access_token_here>" -X DELETE -v "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset?device_id=all&requestor_id=AdobeBEAST&mvpd_id=TempPass"
```

## 支援的客戶端 {#supp-clients}

按平台支援臨時通過和重置工具：

| Adobe Primetime身份驗證客戶端 | 臨時通過 | 重置工具 |
|:--------------------------------------:|:---------:|:----------:|
| JS AccessEnabler | 是 | 是 |
| 本地客戶端iOS | 是 | 是 |
| 本機客戶端tvOS | 是 | 是 |
| 本機客戶端Android | 是 | 是 |
| 本機客戶端fireTV | 是 | 是 |
| 無客戶端API | 是 | 是 |

## 限制和已知問題 {#limitations}

本節介紹適用於當前Temp Pass實現的限制。

**JavaScript SDK**:支援從版本重置臨時傳遞功能 **3.X及以上**。

<!--For Customers migrating from the 2.X JavaScript AccessEnabler to the 3.X JavaScript AccessEnabler, see [AccessEnabler JS 2.x to JS 3.x migration guide](https://tve.helpdocsonline.com/accessenabler-js-to-js-migration-guide).-->
