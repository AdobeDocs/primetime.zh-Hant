---
title: JavaScript SDK概觀
description: JavaScript SDK概觀
exl-id: 8756c804-a4c1-4ee3-b2b9-be45f38bdf94
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# JavaScript SDK概觀 {#javascript-sdk-overview}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 簡介

Adobe強烈建議您移轉至AccessEnabler程式庫的最新JS v4.x。

Adobe Primetime驗證JavaScript整合在熟悉的JS Web應用程式開發環境中，為程式設計師提供無所不在的TV解決方案。 整合的主要元件是您的「高階」應用程式（使用者互動、視訊簡報），以及Adobe提供的「低階」 AccessEnabler資料庫，此資料庫提供您許可權流程的入口，並處理與Adobe Primetime驗證伺服器的通訊。

一般Adobe Primetime驗證許可權流程涵蓋 [程式設計師權益流程](/help/authentication/entitlement-flow.md)和JavaScript整合逐步指南會逐步引導您完成實作。 以下小節提供JavaScript AccessEnabler整合專屬的說明和範例。

>[!IMPORTANT]
>
>本檔案說明案頭Web解決方案的實作。 行動平台不支援JavaScript程式庫(例如iOS上的Safari、Android上的Chrome)。 如果您想要鎖定行動平台(iOS、Android、Windows)，請使用我們的原生SDK。

## 建立MVPD選擇對話方塊 {#creating-the-mvpd-selection-dialog}

使用者若要登入其MVPD並獲得驗證，您的頁面或播放器必須提供使用者識別其MVPD的方式。 會提供MVPD選取對話方塊的預設版本以進行開發。 對於生產使用，您必須實作自己的MVPD選擇器。 

如果您已經知道客戶的提供者，您可以 [以程式設計方式設定MVPD](/help/authentication/home.md)，無需使用者互動。 技巧相同，但會略過叫用「提供者選擇器」對話方塊並要求客戶選取其MVPD的步驟。

## 顯示服務提供者 {#displaying-the-service-provider}

下列程式碼範例示範如何探索和顯示目前客戶的服務提供者：

 **HTML**  — 此頁面會將區段新增至顯示客戶所選提供者（如果已登入）的頁面：

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
 

**JavaScript** 如果使用者已登入，此JavaScript檔案會查詢目前提供者的Access Enabler，並在為其保留的頁面區段中顯示結果。 它也會實作MVPD選擇器對話方塊：

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

呼叫 `logout()` 以啟動登出程式。 此方法不使用引數。 它會登出目前的使用者，清除該使用者的所有驗證和授權資訊，並從本機系統刪除所有AuthN和AuthZ權杖。

在某些情況下，您的播放器不負責處理使用者登出：

 

- **從未與Adobe Primetime驗證整合的網站起始登出時。** 在這種情況下，MVPD可透過瀏覽器重新導向來叫用Adobe Primetime驗證單一登出服務。 （目前不支援透過後通道呼叫叫用SLO。）

>[!NOTE]
>
>如果使用者讓電腦閒置足夠長的時間令其代號過期，他們仍可返回工作階段並成功起始登出。 Adobe Primetime驗證可確保刪除所有Token，並通知MVPD刪除其工作階段。

以下JavaScript程式碼會示範登出（取消驗證）目前驗證的使用者：

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
