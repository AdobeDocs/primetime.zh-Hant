---
title: 臨時通道
description: 臨時通道
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2210'
ht-degree: 0%

---


# 臨時通道 {#temp-pass}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 功能摘要 {#tempass-featur-summary}

Temp Pass可讓程式設計人員為沒有MVPD帳戶憑證的使用者，提供對其受保護內容的暫時存取權。  Temp Pass包含下列功能：

* Temp Pass可配置為提供臨時訪問以涵蓋多種情況，包括：
   * 程式設計師可以每天提供其其中一個網站的簡短（例如10分鐘預覽）。
   * 程式設計師可以提供單一、長時間的演示（例如，四小時），以舉辦奧運會或NCAA 3月瘋狂運動等重大體育賽事。
   * 程式設計師可以提供前兩種情況的組合；例如，一天的初始、較長的檢視期間，接著一系列短期間，會每天重複某些後續天數。
* 程式設計人員指定其臨時通道的持續時間（存留時間或TTL）。
* Temp Pass會依請求者操作。  例如，NBC可為請求者「NBCOlympics」設定4小時的Temp Pass。
* 程式設計師可以重置授予特定請求者的所有令牌。  實施Temp Pass的「臨時MVPD」必須設定為「每個請求者驗證」。
* **特定裝置上的個別使用者有權存取臨時通行證**. 當使用者的臨時通道存取過期後，該使用者在該使用者過期之前，將無法在同一部裝置上取得暫時存取權 [授權令牌](/help/authentication/glossary.md#authz-token) 會從Adobe Primetime驗證伺服器中清除。


>[!NOTE]
>
>Temp Pass是Premium Workflow package的一部分。 如果您有興趣使用此功能，請連絡您的Primetime銷售代表。

## 功能詳細資訊 {#tempass-featur-details}

* **查看時間的計算方式**  — 臨時通行證的有效時間與用戶在程式設計師應用程式上查看內容所花的時間無關。  當通過臨時通道對初始用戶請求授權時，通過將初始當前請求時間加到由程式設計師指定的TTL來計算到期時間。 此過期時間與用戶的設備ID和程式設計師請求者ID相關聯，並儲存在Primetime驗證資料庫中。 每當用戶嘗試使用來自同一設備的臨時傳遞來訪問內容時，Primetime身份驗證將比較伺服器請求時間與與用戶設備ID和程式設計師請求者ID相關的到期時間。 如果伺服器請求時間小於到期時間，則授權；否則，將拒絕授權。
* **設定參數**  — 可由程式設計師指定以下Temp Pass參數以建立Temp Pass規則：
   * **代號TTL**  — 允許使用者觀看而不登入MVPD的時間長度。 此時間以時鐘為基礎，且無論使用者是否觀看內容，都會過期。
   >[!NOTE]
   >請求者ID不能有多個相關聯的Temp Pass規則。
* **驗證/授權**  — 在「臨時通道」流程中，您會將MVPD指定為「臨時通道」。  Primetime驗證不會與臨時通道流程中的實際MVPD通訊，因此「臨時通道」MVPD會授權任何資源。 程式設計師可以指定一個可使用Temp Pass訪問的資源，就像他們對其網站上的其餘資源一樣。 媒體驗證程式庫可照常使用，以驗證Temp Pass短媒體權杖，並在播放前強制進行資源檢查。
* **在Temp Pass流中追蹤資料**  — 在「臨時通過」權限流程期間，有關追蹤資料的兩點：
   * 從Primetime驗證傳遞至您 **sendTrackingData()** callback是裝置ID的雜湊。
   * 由於Temp Pass流程中使用的MVPD ID為「Temp Pass」，因此會將相同的MVPD ID傳回 **sendTrackingData()**. 大部分程式設計人員都可能想將Temp Pass量度與實際MVPD量度以不同方式處理。 這需要您的分析實施中進行一些額外工作。

下圖顯示Temp Pass流程：

![臨時通道流](assets/temp-pass-flow.png)

*圖：臨時通道流*

## 實作Temp Pass {#implement-tempass}

在Primetime驗證端，在參與的程式設計師伺服器配置中添加名為「TempPass」的偽MVPD來實現TempPass。  此偽MVPD就像臨時授予對程式設計師受保護內容的訪問權的實際MVPD。

在程式設計師端，MVPD用於驗證的兩種情況的Temp Pass實施如下：

* **程式設計師頁面上的iFrame**. 無論MVPD的驗證類型為何，Temp Pass都能運作，但對於iFrame案例，需要額外步驟來取消目前的驗證流程並使用Temp Pass進行驗證。 這些步驟如 [iFrame登入](/help/authentication/temp-pass.md) 下方。
* **重新導向至MVPD登入頁面**. 在較傳統的情況下，若在使用MVPD開始驗證之前顯示用於觸發Temp Pass的UI，則不需要執行特殊步驟。 Temp Pass的處理方式應如同一般MVPD。

以下幾點適用於兩種實作案例：

* 「Temp Pass」只會針對尚未請求Temp Pass授權的使用者，顯示在MVPD選擇器中。 在Cookie上保留標幟，即可封鎖後續請求的顯示。 只要使用者未清除瀏覽器快取，就能使用此功能。 如果使用者清除其瀏覽器快取，選擇器中會再次出現「臨時傳遞」，且使用者將可再次提出要求。 只有在「臨時通過」時間尚未過期時，才授予訪問權。
* 當使用者透過Temp Pass要求存取時，Primetime驗證伺服器在驗證程式期間將不會執行其通常的安全性斷言標籤語言(SAML)要求。 反之，只要Token對裝置有效，每次叫用時，驗證端點都會傳回成功。
* 當Temp Pass過期時，其使用者將不再接受驗證，因為在Temp Pass流程中，驗證Token和授權Token具有相同的到期日。 為了向用戶解釋其臨時傳遞已過期，程式設計師必須在調用後立即檢索所選MVPD `setRequestor()`，然後呼叫 `checkAuthentication()` 照常。 在 `setAuthenticationStatus()` 可進行回呼檢查，以判斷auth狀態是否為0，如果選取的MVPD是「TempPass」，則會向使用者顯示其Temp Pass工作階段已過期的訊息。
* 如果使用者在到期前刪除臨時通過權杖，後續的權限檢查將產生一個權杖，其TTL等於剩餘時間。
* 如果使用者在過期後刪除Temp Pass代號，後續的權限檢查會傳回「未授權使用者」。

請參閱 [程式碼範例](/help/authentication/temp-pass.md#tempass-sample-code) 如需如何編寫本節所述實作詳細資料的範例，請參閱下文。

## 程式碼範例 {#tempass-sample-code}

以下各節說明如何呼叫Primetime驗證API以實作臨時通過流程：

* [iFrame登入範例](/help/authentication/temp-pass.md#iframe-login-sample)
* [自動登入範例](/help/authentication/temp-pass.md#auto-login-sample)

### iFrame登入範例 {#iframe-login-sample}

此範例說明如何針對MVPD支援iFrame整合的情況實作Temp Pass:

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

#### iFrame登入使用案例 {#iframe-login-use-cases}

**若要首次要求Temp Pass:**

1. 用戶訪問程式設計師的頁面並點擊登錄連結。
1. MVPD選擇器隨即開啟，使用者會從清單中選擇MVPD。
1. 驗證iFrame隨即顯示。 此iFrame包含「Temp Pass」連結。
1. 用戶按一下「臨時通過」，這樣程式設計師就會向Cookie添加一個標誌，以防止用戶在後續訪問頁面時看到「臨時通過」連結。
1. 臨時通過驗證請求到達Primetime驗證伺服器，並產生驗證Token。 TTL等於程式設計師為臨時通道設定的時段。
1. 臨時通過授權請求到達Primetime驗證伺服器。
1. Primetime驗證伺服器會從請求中擷取裝置與請求者ID，並連同到期時間一起儲存在資料庫中。 到期時間的計算方式為：初始臨時通過請求時間加上TTL（由程式設計師指定）。
1. Primetime驗證伺服器產生授權Token。
1. 用戶訪問受保護的內容。

**若要在傳回的Temp Pass使用者刪除瀏覽器Cookie後再次請求Temp Pass:**

1. 用戶訪問程式設計師的頁面並點擊登錄連結。
1. MVPD選擇器隨即開啟，使用者會從清單中選擇MVPD。
1. 驗證iFrame隨即顯示。 此iFrame包含「Temp Pass」連結（用戶刪除了原始Cookie，因此程式設計師不知道用戶之前是否點擊了「Temp Pass」連結）。
1. 使用者再次點按「Temp Pass」，讓程式設計人員再次將標幟新增至Cookie，以防止使用者在後續造訪頁面時看見「Temp Pass」連結。
1. 臨時通過驗證請求到達產生驗證Token的Primetime驗證伺服器。 TTL現在是臨時通行的剩餘時間（目前時間與裝置ID相關聯的到期時間之差）。
1. 臨時通過授權請求到達Primetime驗證伺服器。
1. Primetime驗證伺服器會從請求中擷取裝置與請求者ID，並使用它們從Primetime驗證資料庫擷取到期時間。 會將目前時間與到期時間比較。
1. 如果使用者的臨時通行尚未過期，則Primetime驗證伺服器會產生授權Token。
1. 如果用戶的臨時傳遞尚未過期，則用戶將能夠訪問受保護的內容。

### 自動登入範例 {#auto-login-sample}

下列範例說明當使用者造訪網站時，會自動以TempPass登入的案例。 使用者隨時都可以選擇使用一般MVPD登入，若TempPass已過期，系統會發出警告：

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

某些事件需要分階段免費存取內容，例如初始免費存取間隔（例如4小時），接著是每日免費存取（例如，後一天10分鐘）。  為了讓程式設計師實施此方案，他們必須與Adobe聯繫人安排此方案，為程式設計師配置兩個臨時MVPD。

此範例案例（初始4小時免費工作階段，接著是每日10分鐘免費工作階段）Adobe會設定名為TempPass1的MVPD，其存留時間(TTL)為4小時，而TempPass2的TTL為10分鐘，供後續期間使用。  這兩者都與程式設計師請求者ID相關聯。

### 程式設計人員實施 {#mult-tempass-prog-impl}

在Adobe配置兩個TempPass實例後，另外兩個MVPD（TempPass1和TempPass2）將出現在程式設計師的MVPD清單中。  程式設計師需要執行以下步驟來實施多個臨時通道：

1. 在使用者初次造訪網站時，使用TempPass1自動將其登入。 您可以使用上述的自動登入範例作為此工作的起點。
1. 當您偵測到TempPass1已過期時，請將事實儲存（在Cookie/本機儲存體中），並向使用者顯示標準MVPD選擇器。 **請務必從該清單中過濾掉TempPass1和TempPass2**.
1. 在後續的每一天，如果TempPass1已過期，則使用TempPass2自動登入該使用者。
1. 當TempPass2過期時，請儲存當天的數值（在Cookie/本機儲存空間中），並向使用者顯示標準MVPD選擇器。 再次，請務必從該清單中篩選掉TempPass1和TempPass2。
1. 在每新天00:00時，使用 [重設TempPass Web API](/help/authentication/temp-pass.md#reset-all-tempass).

>[!NOTE]
>**程式設計說明：** Primetime驗證沒有內建機制可在10分鐘後停止免費串流。  一旦TempPass2過期，程式設計師就可以限制訪問。 要完成這一點，程式設計師可以每X分鐘在其網站/應用中實施一次「checkAuthorization」調用，其中X是程式設計師確定的對其應用有意義的時間段。

## 重置所有臨時通道 {#reset-all-tempass}

某些業務規則需要定期清除Temp Pass ，或針對特定請求者ID和MVPD ID發出的所有Temp Passes進行臨機重設。 此功能支援下列使用案例：

* 每日10分鐘的臨時通道（臨時通道必須在一天開始時重置）
* 在重大新聞期間，所有使用者都可使用臨時通道。 （當突發新聞開始時，需要為所有設備重置臨時通道。）
* 多個臨時通過方案，提供某些長度的初始查看時段，以及後續另一個長度的每日時段的組合。

為了重設所有臨時傳遞，Primetime驗證為程式設計師提供 *公共* 網頁API:

```url
DELETE https://mgmt.auth.adobe.com/reset-tempass/v2/reset
```

>[!NOTE]
>上述URL會取代先前的重設API。 不再支援舊的重設API(v1)。

* **協定：** HTTPS
* **主機：**
   * 版本 — mgmt.auth.adobe.com
   * Prequal - mgmt-prequal.auth.adobe.com
* **路徑：** /reset-tempass/v2/reset
* **查詢參數：** `device_id=all&requestor_id=REQUESTOR_ID&mvpd_id=TEMPPASS_MVPD_ID`
* **標題：** ApiKey - 1232293681726481
* **回應：**
   * 成功 — HTTP 204
   * 失敗：
      * HTTP 400，以取得錯誤的要求
      * 若未指定ApiKey，則HTTP 401
      * ApiKey無效時的HTTP 403

例如：

```curl
$ curl -H "Authorization: Bearer <access_token_here>" -X DELETE -v "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset?device_id=all&requestor_id=AdobeBEAST&mvpd_id=TempPass"
```

## 支援的用戶端 {#supp-clients}

各平台對Temp Pass和Reset Tool的支援：

| Adobe Primetime驗證用戶端 | 臨時通道 | 重設工具 |
|:--------------------------------------:|:---------:|:----------:|
| JS AccessEnabler | 是 | 是 |
| 本機用戶端iOS | 是 | 是 |
| 原生用戶端tvOS | 是 | 是 |
| 原生用戶端Android | 是 | 是 |
| 本機用戶端fireTV | 是 | 是 |
| 無用戶端API | 是 | 是 |

## 限制和已知問題 {#limitations}

本節說明適用於目前Temp Pass實作的限制。

**JavaScript SDK**:支援從版本重置臨時傳遞功能 **3.X及以上版本**.

<!--For Customers migrating from the 2.X JavaScript AccessEnabler to the 3.X JavaScript AccessEnabler, see [AccessEnabler JS 2.x to JS 3.x migration guide](https://tve.helpdocsonline.com/accessenabler-js-to-js-migration-guide).-->