---
title: 如何將MVPD登錄頁從iFrame遷移到彈出窗口
description: 如何將MVPD登錄頁從iFrame遷移到彈出窗口
exl-id: 389ea0ea-4e18-4c2e-a527-c84bffd808b4
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# 如何將MVPD登錄頁從iFrame遷移到彈出窗口 {#migr-mvpd-login-iframe-popup}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 彈出與iFrame {#popup-vs-iframe}

一些用戶在MVPD登錄頁的iFrame實現中遇到第三方cookie問題。
<!--These issues are described in the tech notes linked below:

* [Adobe Primetime authentication and Safari login issues](https://tve.helpdocsonline.com/adobe-pass)
* [MVPD iFrame login and 3rd party cookies](https://tve.helpdocsonline.com/mvpd)-->

Adobe Primetime認證小組 **建議實現彈出/新窗口登錄頁** 而不是Firefox和Safari上的iFrame版本。  但是，如果要為Internet Explorer實現登錄頁，則可能會遇到彈出式實現問題。 IE問題的原因是，當用戶在彈出窗口中使用其MVPD進行身份驗證後，Adobe Primetime身份驗證將強制父頁重定向，Internet Explorer將其視為彈出窗口阻止程式。 Adobe Primetime認證小組 **建議為Internet Explorer實現iFrame登錄**。

本技術說明中提供的示例代碼使用iFrame和彈出窗口的混合實現 — 在Internet Explorer上開啟iFrame，在其他瀏覽器上開啟彈出窗口。

考慮到iFrame實現已存在，技術說明的第一部分顯示iFrame實現的代碼，第二部分顯示修改，以將彈出式實現作為預設值。


## 在iFrame中具有登錄頁的MVPD選取器 {#mvpd-pickr-iframe}

前面的代碼示例顯示了一個HTML頁，其中包含 &lt;div> 將建立iFrame的標籤以及「關閉iFrame」按鈕：

```HTML
<body> 
    <div id="mvpddiv">
        <div style="background: red">
            <input type="button" id="btnCloseIframe" value="X" onclick="closeIframeAction();">
        </div>
        <br/>
        <!-- We use the "about:blank" value so that when the iFrame loads
             we do not see the the parent page. -->
        <iframe id="mvpdframe" name="mvpdframe" src="about:blank"></iframe>
    </div> 
</body>
```

這是關聯 **JavaScript** 代碼：

```JavaScript
/*
 * Callback indicating that the AccessEnabler swf has initialized
 */
function swfLoaded() {
    // AccessEnabler is loaded so we can use the API function it provides
    accessEnablerObject.setRequestor(requestorID); 
    accessEnablerObject.checkAuthentication();
} 
/*
* The code the correctly closes the opened IFrame and does not leave the
* AccessEnabler in an undefined state.
*/
function closeIframeAction () {
    accessEnablerObject.setSelectedProvider(null);
    /* We use the "about:blank" value so that when the iFrame loads
     * we do not see the the previous MVPD.
     */
    document.getElementById('mvpdframe').src="about:blank";
    document.getElementById('mvpddiv').style.visibility="hidden";
    document.getElementById('mvpddiv').style.display="none";
}
/*
* Some of the supported MVPDs require their login pages to be displayed within an iFrame.
* In your HTML page, you must include the following <div> tag: "<div id="mvpddiv"></div>".
* Called when the selected MVPD requires an iFrame in which to display its authentication UI.
*/
function createIFrame(inWidth, inHeight) {
     // Create the iFrame to the specified width and height for the auth page
    ifrm = document.createElement("IFRAME");
    ifrm.name = "mvpdframe";
    ...
    document.getElementById('mvpddiv').appendChild(ifrm);
    ...
    // Force the name into the DOM since it is still not refreshed, for IE
    window.frames["mvpdframe"].name = "mvpdframe";
}
/*
 * The custom non-Flash MVPD selector dialog will be implemented in this function.
 */
function displayProviderDialog(providers) {
    /* This is an example how previously the MVPD picker was build and will be replaced. */
}
/* 
* Sending the user selected MVPD of the custom dialog is achieved
* by calling the API function setSelectedProvider(providerID:String).
*/
function setSelectedProvider(providerID) {
    accessEnablerObject.setSelectedProvider(providerID);
}
```


## 在彈出窗口中具有登錄頁的MVPD選取器 {#mvpd-pickr-popup}

因為我們不會 **iFrame** 現在，HTML代碼將不包含iFrame或關閉iFrame的按鈕。 以前包含iFrame的div - **mvpdiv**  — 將保留並用於以下用途：

* 通知用戶，如果彈出焦點丟失，MVPD登錄頁已開啟
* 提供連結以重新關注彈出菜單

```HTML
<body onload="javascript:loadAccessEnabler();"> 
   <div id="aeHolder">
       <div name="contentAccessEnabler" id="contentAccessEnabler"></div>
   </div>
   <div id="mvpddiv">
      <p>
      <strong>No login window?</strong>
      <br/>
      <a href="javascript:mvpdWindow.focus();">Click here to open it.</a>
      <br/>
      Still not working? Check popup blockers!
      </p>
   </div> 
 
   <div id="picker" style="display:none">
      Choose MVPD: <br/>
      <select id="mvpdList" multiple></select>
      <br/>
         <a id="authenticateButton" onclick="javascript:authenticate();">Authenticate</a>
   </div>
</body>
```

MVPD清單將顯示在名為的div中 **拾取器** 作為選擇 **-mvpd清單**。

將使用新的API回調 —  **setConfig(configXML)**。 調用setRequestor(requestorID)函式後觸發回調。 此回調將返回與以前設定的requestorID整合的MVPD的清單。 在回調方法中，將分析傳入的XML，並快取MVPD清單。 MVPD選取器也已建立，但未顯示。

```JavaScript
var mvpdList;  // The list of cached MVPDs
var mvpdWindow;  // The reference to the popup with the MVPD login page
var cancelTimer = 0;
/* Callback indicating that the AccessEnabler swf has initialized */
function swfLoaded() {
   accessEnablerObject = $('#AccessEnabler').get(0);
   // Using a custom implementation of the MVPD picker
   accessEnablerObject.setProviderDialogURL('none');
   accessEnablerObject.setRequestor(requestorID); 
}

function setConfig(configXML) {
   mvpdList = [];
   $.each($($.parseXML(configXML)).find('mvpd'), function (idx, item) {
      var mvpdId = $(item).find('id').text();
      mvpdList[mvpdId] = {
         displayName: $(item).find('displayName').text(),
         logo: $(item).find('logoUrl').text(),
         popup: $(item).find('iFrameRequired').text() == "true",
         width: $(item).find('iFrameWidth').text(),
         height: $(item).find('iFrameHeight').text()
      };

      $('#mvpdList').append($('<option value="' + mvpdId + '" title="' + mvpdId + '">' + mvpdList[mvpdId].displayName + '</option>'));
   });
   accessEnablerObject.getAuthentication();
}
```

調用getAuthentication()或getAuthorization()函式後，將觸發displayProviderDialog()回調。 通常，在此回調中，MVPD清單會生成並顯示。 由於MVPD選取器已構建，所以只需向用戶顯示即可。

```JavaScript
/*
 * The custom non-Flash MVPD selector dialog will be implemented in this function.
 */
function displayProviderDialog(providers) {
   $('#picker').show();
}
```

用戶從選取器中選擇MVPD後，需要建立彈出窗口。 如果建立彈出窗口時使用about:blank或另一個域上的頁面，則某些瀏覽器可能會阻止該彈出窗口 — 因此建議使用載入AccessEnabler的主機名開啟它。

在iFrame實現中，重新設定驗證流是由btnCloseIframe按鈕和JavaScript函式closeIframeAction()完成的，但現在不再能對iFrame進行裝飾。 因此，通過監視彈出窗口何時關閉（由用戶或完成驗證流），可以實現相同的行為。 添加了代碼段，這也有助於用戶丟失彈出式菜單的焦點：

```HTML
"<a href="javascript:mvpdWindow.focus();">Click here to open it.</a>".
```

在createIFrame()回調 **mvpdiv** 將顯示div。

```JavaScript
function createIFrame(width, height) {
   $('#mvpddiv').show();
   if (useIframeLoginStyle) {
      ...
   }
}

/* Function called when user has selected the MVPD from the picker */
function authenticate() {
   var selectedMvpd = $('#mvpdList').val()[0];
   if (mvpdList[selectedMvpd].popup) {
      mvpdWindow = window.open("http://entitlement.auth-staging.adobe.com", "mvpdframe", "width=" + mvpdList[selectedMvpd].width + ",height=" + mvpdList[selectedMvpd].height, true);
      if (!mvpdWindow) {
         // Message to user that popup blocker is not allowing the authentication process to start
      }
      //watch the mvpd popup for close
      clearInterval(cancelTimer);
      cancelTimer = setInterval(checkClosed, 200);
   }
   accessEnablerObject.setSelectedProvider(selectedMvpd);
}

function checkClosed() {
   try {
      if (mvpdWindow && mvpdWindow["closed"]) {
         clearInterval(cancelTimer);
         accessEnablerObject.setSelectedProvider(null);
         accessEnablerObject.getAuthentication();
         $('#mvpddiv').hide();
      }
   } catch (error) {
      console.log(error);
   }
}
```

>[!IMPORTANT]
>
>* 示例代碼包含用於使用的請求者ID的硬編碼變數 — 「REF」，該變數應替換為真正的程式設計師請求者ID。
>* 示例代碼將僅從與使用的請求者ID關聯的白名單域正確運行。
>* 由於整個代碼可供下載，因此此技術說明中顯示的代碼已被截斷。 有關完整示例，請參見 **JS iFrame與彈出式示例**。
>* 外部JavaScript庫已從 [Google托管服務](https://developers.google.com/speed/libraries/)。

