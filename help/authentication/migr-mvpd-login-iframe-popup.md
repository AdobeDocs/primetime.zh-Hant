---
title: 如何將MVPD登入頁面從iFrame移轉至快顯視窗
description: 如何將MVPD登入頁面從iFrame移轉至快顯視窗
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---


# 如何將MVPD登入頁面從iFrame移轉至快顯視窗 {#migr-mvpd-login-iframe-popup}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 快顯視窗與iFrame {#popup-vs-iframe}

有些使用者在MVPD登入頁面的iFrame實作中遇到第三方Cookie問題。
<!--These issues are described in the tech notes linked below:

* [Adobe Primetime authentication and Safari login issues](https://tve.helpdocsonline.com/adobe-pass)
* [MVPD iFrame login and 3rd party cookies](https://tve.helpdocsonline.com/mvpd)-->

Adobe Primetime驗證團隊 **建議實作快顯視窗/新視窗登入頁面** 而非Firefox和Safari上的iFrame版本。  不過，如果您正在實作Internet Explorer的登入頁面，則可能會遇到快顯視窗實作的問題。 IE問題是因為，當使用者在快顯視窗中以其MVPD進行驗證後，Adobe Primetime驗證會強制上層頁面重新導向，而Internet Explorer會將此重新導向視為快顯封鎖程式。 Adobe Primetime驗證團隊 **建議為Internet Explorer實作iFrame登入**.

此技術說明中顯示的范常式式碼會使用iFrame和快顯視窗的混合實作 — 在Internet Explorer上開啟iFrame，並在其他瀏覽器上開啟快顯視窗。

考慮到iFrame實作已存在，技術說明的第一部分會顯示iFrame實作的程式碼，而第二部分會顯示變更，以將快顯視窗實作視為預設。


## iFrame中具有登入頁面的MVPD選取器 {#mvpd-pickr-iframe}

上一個程式碼範例顯示的HTML頁面包含 &lt;div> 標籤，其中iFrame與close iFrame按鈕一起建立：

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

以下是相關 **JavaScript** 代碼：

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


## 彈出式視窗中具有登入頁面的MVPD選取器 {#mvpd-pickr-popup}

因為我們不會使用 **iFrame** 現在，HTML代碼將不包含iFrame或關閉iFrame的按鈕。 先前包含iFrame的div - **mvpddiv**  — 將保留並用於下列項目：

* 若遺失快顯視窗焦點，通知使用者MVPD登入頁面已開啟
* 提供連結，重新聚焦於快顯視窗

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

MVPD清單會顯示在名為的div中 **選擇器** 作為選取 **-mvpdList**.

將使用新API回呼 —  **setConfig(configXML)**. 呼叫setRequestor(requestorID)函式後會觸發回呼。 此回呼會傳回與先前設定之requestorID整合的MVPD清單。 在回呼方法中，會剖析傳入的XML，並快取MVPD清單。 也會建立MVPD選擇器，但不會顯示。

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

呼叫getAuthentication()或getAuthorization()函式後，就會觸發displayProviderDialog()回呼。 通常，在此回呼內，會建置並顯示MVPD清單。 由於已建置MVPD選擇器，所以只需向使用者顯示它即可。

```JavaScript
/*
 * The custom non-Flash MVPD selector dialog will be implemented in this function.
 */
function displayProviderDialog(providers) {
   $('#picker').show();
}
```

使用者從選擇器中選取MVPD後，需要建立快顯視窗。 如果彈出式功能表是使用about:blank或位於其他域的頁面建立，則某些瀏覽器可能會阻止該彈出式功能表 — 因此，建議使用載入AccessEnabler的主機名開啟它。

在iFrame實作中，重設驗證流程是由btnCloseIframe按鈕和JavaScript函式closeIframeAction()完成，但現在已無法再裝飾iFrame。 因此，觀看彈出畫面關閉時（由使用者或完成驗證流程），即可達到相同的行為。 已新增程式碼片段，以協助防止使用者失去快顯視窗的焦點：

```HTML
"<a href="javascript:mvpdWindow.focus();">Click here to open it.</a>".
```

在createIFrame()回呼上， **mvpddiv** div隨即顯示。

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
>* 該示例代碼包含用於所用請求者ID - &#39;REF&#39;的硬編碼變數，該變數應被真正的程式設計師請求者ID替換。
>* 范常式式碼只會從與所使用請求者ID相關聯的白名單網域正常執行。
>* 由於整個程式碼可供下載，因此此技術說明中顯示的程式碼已遭截斷。 如需完整範例，請參閱 **JS iFrame與快顯視窗範例**.
>* 外部JavaScript程式庫已從 [Google代管服務](https://developers.google.com/speed/libraries/).

