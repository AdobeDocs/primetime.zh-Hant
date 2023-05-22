---
title: JavaScript SDK概述
description: JavaScript SDK概述
exl-id: 8756c804-a4c1-4ee3-b2b9-be45f38bdf94
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# JavaScript SDK概述 {#javascript-sdk-overview}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 導言

Adobe強烈建議您遷移到AccessEnabler庫的最新JS v4.x。

Adobe Primetime驗證JavaScript整合在熟悉的JS Web應用程式開發環境中為程式設計師提供了TV-Everywhere解決方案。 整合的主要元件是您的「高級」應用程式（用戶交互、視頻演示），以及Adobe提供的「低級」AccessEnabler庫，該庫提供您對權利流的輸入，並處理與Adobe Primetime身份驗證伺服器的通信。

一般的Adobe Primetime身份驗證權限流在 [程式設計師權利流](/help/authentication/entitlement-flow.md)以及JavaScript整合指南指導您完成實現。 以下各節提供了特定於JavaScript AccessEnabler整合的說明和示例。

>[!IMPORTANT]
>
>本文檔介紹案頭Web解決方案的實施。 移動平台不支援JavaScript庫(例如，iOS的Safari和Android的Chrome)。 如果您希望將目標鎖定在移動平台(iOS、Android、Windows)，請使用我們的本機SDK。

## 建立MVPD選擇對話框 {#creating-the-mvpd-selection-dialog}

用戶若要登錄到其MVPD並經過身份驗證，您的頁面或播放器必須為用戶提供標識其MVPD的方法。 提供了MVPD選擇對話框的預設版本供開發。 為了生產用途，必須實現自己的MVPD選擇器。 

如果您已經知道客戶的提供商是誰，您可以 [以寫程式方式設定MVPD](/help/authentication/home.md)，而無需用戶交互。 該技術相同，但會繞過調用「提供程式選擇器」對話框並要求客戶選擇其MVPD的步驟。

## 顯示服務提供程式 {#displaying-the-service-provider}

以下代碼示例演示了如何發現和顯示當前客戶的服務提供商：

 **HTML**  — 如果客戶已登錄，此頁會向顯示其所選提供商的頁面添加一個部分：

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
 

**JavaScript** 如果用戶已登錄，則此JavaScript檔案將查詢當前提供程式的Access Enabler，並在為其保留的頁面部分中顯示結果。 它還實現MVPD選擇器對話框：

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

## 註銷 {#logout}

呼叫 `logout()` 啟動註銷進程。 此方法不使用任何參數。 它註銷當前用戶，清除該用戶的所有身份驗證和授權資訊，並從本地系統刪除所有AuthN和AuthZ令牌。

在某些情況下，您的玩家不負責處理用戶註銷：

 

- **從未與Adobe Primetime身份驗證整合的站點啟動註銷時。** 在這種情況下，MVPD可以通過瀏覽器重定向調用Adobe Primetime驗證單次註銷服務。 （當前不支援通過回通道調用調用SLO。）

>[!NOTE]
>
>如果用戶使其電腦空閒足夠長，以致其令牌過期，則他們仍可以返回其會話並成功啟動註銷。 Adobe Primetime驗證確保刪除所有令牌，並通知MVPD刪除其會話。

以下JavaScript代碼演示註銷（取消驗證）當前已驗證的用戶：

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
