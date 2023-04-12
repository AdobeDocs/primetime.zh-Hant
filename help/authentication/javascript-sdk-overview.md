---
title: JavaScript SDK概述
description: JavaScript SDK概述
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---


# JavaScript SDK概述 {#javascript-sdk-overview}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 簡介

Adobe強烈建議您遷移至AccessEnabler庫的最新JS v4.x。

Adobe Primetime驗證JavaScript整合為程式設計師提供熟悉的JS網頁應用程式開發環境中的TV-Everywhere解決方案。 整合的主要元件是您的「高級」應用程式（用戶交互、視頻演示），以及Adobe提供的「低級」AccessEnabler庫，該庫提供您的權限流條目，並處理與Adobe Primetime驗證伺服器的通信。

一般Adobe Primetime驗證權限流程在 [程式設計師權利流程](/help/authentication/entitlement-flow.md)，以及JavaScript整合逐步指南會帶您了解實作。 以下各節提供JavaScript AccessEnabler整合的特定說明和示例。

>[!IMPORTANT]
>
>本文檔介紹案頭Web解決方案的實施。 行動平台不支援JavaScript資料庫(例如iOS上的Safari、Android上的Chrome)。 如果您想要鎖定行動平台(iOS、Android、Windows)，請使用我們的原生SDK。

## 建立MVPD選擇對話框 {#creating-the-mvpd-selection-dialog}

若要讓使用者登入其MVPD並通過驗證，您的頁面或播放器必須提供讓使用者識別其MVPD的方式。 為開發提供MVPD選擇對話框的預設版本。 為了生產用途，您必須實作自己的MVPD選取器。 

如果您已知道客戶的提供者是誰，您可以 [以寫程式方式設定MVPD](/help/authentication/home.md)，不需使用者互動。 技術相同，但會略過叫用「提供者選取器」對話方塊並要求客戶選取其MVPD的步驟。

## 顯示服務提供程式 {#displaying-the-service-provider}

下列程式碼範例示範如何探索及顯示目前客戶的服務提供者：

 **HTML**  — 此頁面會新增一個區段至顯示客戶選擇的提供者（如果他們已登入）的頁面：

```HTML
    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" 
            "http://www.w3.org/TR/html4/loose.dtd"> 
    <html>
    <head>
        <title>Get the distributor that is used for the authentication</title>
        <script type="text/javascript" src="libs/jquery-1.4.4.min.js"></script>
        <script type="text/javascript" src="libs/swfobject.js"></script>
        <script type="text/javascript" src="scripts/sample6.js"></script>
    </head>
    <body>
        <div id="alternative">
        <a href="http://www.adobe.com/go/getflashplayer"> 
            <img src="http://www.adobe.com/images/shared/download_buttons/get_flash_player.gif" 
                 alt="Get Adobe Flash player"/> </a>
        </div> 
        <div id="user_authenticated">Please wait while we verify your authentication status</div> 
        <div id="control">
        <button id="sign_in" style="display:none;">Sign in</button>
        <button id="sign_out" style="display:none;">Sign out</button>
        </div> 
        <div id="distributor"></div> 
        <div id="provider_selector" style="display:none;">
        <select id="provider_list"></select>
        <button id="login">Login</button>
        <button id="cancel">Cancel</button>
        </div> 
        <div id="video_player">This is a video player showing an image as a preview.  You are not yet authorized to see this content.  Make sure that you first sign in.
        </div> 
        <div id="get_authorization">
        <button id="request_access" style="display:none;">Request access</button>
        </div> 
    </body>
    </html>
```
 

**JavaScript** 如果用戶已登錄，此JavaScript檔案將查詢當前提供程式的Access Enabler，並在為其保留的頁面部分中顯示結果。 也會實作MVPD選取器對話方塊：

```JS
    $(function() {
        embedAE();
    }); 
    function embedAE() {
        var flashvars = {};
        var params = {
            bgcolor: "#869ca7",
            quality: "high",
            allowscriptaccess: "always"
        };
        var attributes = {
            id: "ae_swf",
            align: "middle",
            name: "ae_swf"
        };
        swfobject.embedSWF(
                "https://entitlement.auth-staging.adobe.com/entitlement/AccessEnabler.swf",      
                "alternative", "1", "1", "10.1.53", "", flashvars, params, attributes);
    } 
    function getAE() {
        return document.getElementById("ae_swf");
    } 
    function swfLoaded() {
        var swf = getAE();
        initBindings();
        // don't load the default provider-selection dialog 
        swf.setProviderDialogURL("none");
        // identify yourself 
        swf.setRequestor("sample_requestor_Id");
        swf.checkAuthentication();
    } 
    // Define the button actions for the provider dialog
    function initBindings() {
        var provider_selector = $('#provider_selector');
        var sign_in = $('#sign_in');
        var sign_out = $('#sign_out');
        var login = $('#login');
        var cancel = $('#cancel');
        var request_access = $('#request_access'); 
        sign_out.click(function() {
            getAE().logout();
        });
        sign_in.click(function() {
            getAE().getAuthentication();
        }); 
        login.click(function() {
            var selected_mvpd_id = $("#provider_list option:selected").val();
            getAE().setSelectedProvider(selected_mvpd_id);
        }); 
        cancel.click(function() {
            getAE().setSelectedProvider(null);
            provider_selector.hide();
        }); 
        request_access.click(function(){
            getAE().getAuthorization("sample_requestor_Id");
        });
    }
    // Called if user is already authenticated; queries AE to find the current user's MVPD, 
    // Adds the result to the UI 
    function setDistributor() {
        var distributor = $("#distributor");
        var selectedProvider = getAE().getSelectedProvider();
        distributor.replaceWith('<div id="distributor">' +
                                'Courtesy of ' +
                                selectedProvider.MVPD +
                                '</div>');
    } 
    // Adjust the contents of the provider dialog, based on authentication status 
    // Adds the call to check and display the current distributor, if the user is already
    // logged in. 
    function setAuthenticationStatus(isAuthenticated, errorCode) {
        var user_authenticated = $("#user_authenticated");
        var video_player = $("#video_player");
        var sign_in = $('#sign_in');
        var sign_out = $('#sign_out');
        var request_access = $('#request_access'); 
        if (isAuthenticated == 1) {
            setDistributor();
            user_authenticated.replaceWith('<div id="user_authenticated">
                                           You are authenticated - if you wish you can sign out
                                           </div>');
            sign_out.show();
            sign_in.hide();
            video_player.replaceWith('<div id="video_player">Now you can ask for access.</div>');
            request_access.show();
        } else {
            user_authenticated.replaceWith('<div id="user_authenticated">
                                           You are not authenticated please sign in
                                           </div>');
            sign_in.show();
            sign_out.hide();
        }
    } 
    // Allow user to choose a provider 
    function displayProviderDialog(providers) {
        var provider_list = $("#provider_list");
        var options = provider_list.attr('options');
        for (var index in providers) {
            options[index] = new Option(providers[index].displayName,
                                        providers[index].ID);
        }
        //select the first one by default 
        if (!$("#provider_list option:selected").length)
            $("#provider_list option[0]").attr('selected', 'selected'); 
        $('#provider_selector').show();
    } 
    // Handle the authorization response by sending token to video player 
    function setToken(requested_resource_id, token) {
        var video_player = $("#video_player");
        var request_access = $("#request_access");
        video_player.replaceWith('<div id="video_player">Now you are authorized to ' +
                                 requested_resource_id +
                                 ' content with ' + token + ' . </div>');
    }
```

## 登出 {#logout}

呼叫 `logout()` 啟動註銷過程。 此方法不使用引數。 它會登出目前的使用者，清除該使用者的所有驗證和授權資訊，並從本機系統刪除所有AuthN和AuthZ代號。

在某些情況下，您的播放器不負責處理使用者登出：

 

- **從未與Adobe Primetime驗證整合的網站啟動登出時。** 在此情況下，MVPD可透過瀏覽器重新導向來叫用Adobe Primetime驗證單一登出服務。 （目前不支援透過後通道呼叫叫用SLO。）

>[!NOTE]
>
>如果使用者讓電腦閒置夠久，使其代號過期，他們仍可以返回工作階段並成功起始登出。 Adobe Primetime驗證可確保刪除所有代號，並通知MVPD刪除其工作階段。

下列JavaScript程式碼會示範登出（取消驗證）目前已驗證的使用者：

```JS
    [...]
    /*
     * @param isAuthenticated authentication status: 1 - Authenticated, 0 - not authenticated 
     * @param errorCode Any error that occurred when determining the authentication status.
     * An empty string if no error occurred.
     */
    function setAuthenticationStatus(isAuthenticated, errorCode) {
        if (isAuthenticated == 1 ) {
            /* User is authenticated – we can logout / deauthenticate */
            accessEnablerObject.logout();
            /* Logs out the current user, clearing all authentication
             * and authorization information for that user. Deletes
             * all authN and authZ tokens from the user's system.
             */
        } else {
            /*
             * User is NOT authenticated – we do not need to logout;
             * Show the log-in image/button/message
             */
        }
    }
```

<!--
**Related Information**

- [JavaScript SDK Cookbook](/help/authentication/javascript-sdk-cookbook.md)
- [JavaScript SDK API Reference](/help/authentication/javascript-sdk-api-reference.md)
- [JavaScript Code Samples](#javascript-code-samples)
- [Understanding Tokens](#understanding_tokens)
-->