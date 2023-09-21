---
title: 如何將MVPD登入頁面從iFrame移轉至快顯視窗
description: 如何將MVPD登入頁面從iFrame移轉至快顯視窗
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# 如何將MVPD登入頁面從iFrame移轉至Popup {#migr-mvpd-login-iframe-popup}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要Adobe的目前授權。 不允許未經授權的使用。

## 快顯視窗與iFrame {#popup-vs-iframe}

有些使用者在MVPD登入頁面的iFrame實作中遇到第三方Cookie問題。
<!--These issues are described in the tech notes linked below:

* [Adobe Primetime authentication and Safari login issues](https://tve.helpdocsonline.com/adobe-pass)
* [MVPD iFrame login and 3rd party cookies](https://tve.helpdocsonline.com/mvpd)-->

Adobe Primetime驗證團隊 **建議實作快顯/新視窗登入頁面** 而非Firefox和Safari上的iFrame版本。  不過，如果您要實作Internet Explorer的登入頁面，您可能會遇到快顯視窗實作的問題。 IE問題是因為以下事實所造成：當使用者在快顯視窗中使用他們的MVPD進行驗證後，Adobe Primetime驗證會強制上層頁面重新導向，而這會被Internet Explorer視為快顯封鎖程式。 Adobe Primetime驗證團隊 **建議實作Internet Explorer的iFrame登入**.

此技術備註中顯示的範常式式碼使用iFrame和快顯視窗的混合實作 — 在Internet Explorer上開啟iFrame，並在其他瀏覽器上開啟快顯視窗。

鑑於iFrame實作已經存在，技術備註的第一部分會顯示iFrame實作的程式碼，第二部分則會顯示變更，以將快顯視窗實作設為預設值。


## iFrame中具有登入頁面的MVPD選擇器 {#mvpd-pickr-iframe}

HTML先前的程式碼範例顯示包含 &lt;div> 標籤會與關閉iFrame按鈕一起建立iFrame：

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

以下是相關聯的 **JavaScript** 程式碼：

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


## 在快顯視窗中具有登入頁面的MVPD選擇器 {#mvpd-pickr-popup}

因為我們不會使用 **iFrame** HTML程式碼將不再包含iFrame或關閉iFrame的按鈕。 先前包含iFrame的div - **mvpddiv**  — 將保留，並用於下列專案：

* 通知使用者MVPD登入頁面已在快顯視窗焦點遺失時開啟
* 提供連結，以重新取得快顯視窗的焦點

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

MVPD清單將顯示在名為的div中 **選取器** 作為選擇 **-mvpdList**.

將使用新的API回呼 —  **setConfig(configXML)**. 呼叫setRequestor(requestorID)函式之後會觸發回呼。 此回呼會傳回與先前設定的requestorID整合的MVPD清單。 在回呼方法中，會剖析傳入的XML，並快取MVPD清單。 也會建立MVPD選擇器，但不會顯示。

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

呼叫getAuthentication()或getAuthorization()函式之後，就會觸發displayProviderDialog()回呼。 一般而言，在此回呼內，會建置並顯示MVPD清單。 由於MVPD選擇器已經建置，因此唯一要做的就是向使用者顯示它。

```JavaScript
/*
 * The custom non-Flash MVPD selector dialog will be implemented in this function.
 */
function displayProviderDialog(providers) {
   $('#picker').show();
}
```

使用者從選擇器選取MVPD後，需要建立快顯視窗。 如果使用about：blank或其他網域上的頁面建立快顯視窗，有些瀏覽器可能會封鎖快顯視窗，因此建議使用載入AccessEnabler的主機名稱來開啟快顯視窗。

在iFrame實作中，重設驗證流程已由btnCloseIframe按鈕和JavaScript函式closeIframeAction()完成，但現在已無法再裝飾iFrame。 因此，觀看快顯視窗關閉的時間（由使用者或完成驗證流程）也會獲得相同的行為。 已新增程式碼片段，萬一使用者失去快顯視窗的焦點時也有幫助：

```HTML
"<a href="javascript:mvpdWindow.focus();">Click here to open it.</a>".
```

在createIFrame()回呼上 **mvpddiv** 將會顯示div。

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
>* 程式碼範例包含所用要求者ID - &#39;REF&#39;的硬式編碼變數，該變數應被真正的程式設計人員要求者ID取代。
>* 程式碼範例只會從與所使用要求者ID關聯的白名單網域中正確執行。
>* 由於整個程式碼都可供下載，此技術備註中顯示的程式碼已遭截斷。 如需完整範例，請參閱 **JS iFrame與快顯視窗範例**.
>* 外部JavaScript程式庫是從 [Google託管服務](https://developers.google.com/speed/libraries/).
