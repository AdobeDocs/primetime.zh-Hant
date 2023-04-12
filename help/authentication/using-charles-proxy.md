---
title: 使用Charles Proxy
description: 使用Charles Proxy
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# 使用Charles Proxy {#using-charles-proxy}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。


**Charles:** <http://charlesproxy.com>

 
## 下載、安裝及開始使用Charles Proxy {#download-install-and-get-stared-with-charles-proxy}

- **下載** - <http://www.charlesproxy.com/download/>
- **安裝** - <http://www.charlesproxy.com/documentation/installation/>
- **快速入門** - <http://www.charlesproxy.com/documentation/getting-started/>

 
## 結構與序列標籤 {#structure-vs-sequence-tabs}

有兩種不同的方式可檢視流量：

1. **結構**  — 請求按主機分組
1. **序列**  — 請求會依呼叫順序列出


## SSL和憑證 {#ssl-and-certificates}

啟用SSL代理 `\[ *Proxy -\> Proxy Settings... -\> SSL* \]`

勾選「啟用SSL代理」核取方塊，並新增所有HTTPS位置。


![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/ProxySettings.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/SSLSettings.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AddHttpsLocations.PNG)



- SSL代理 —  <http://www.charlesproxy.com/documentation/proxying/ssl-proxying/>
- SSL憑證 —  <http://www.charlesproxy.com/documentation/using-charles/ssl-certificates/>
- 從行動裝置代理SSL — 請參閱下方。

 
## 忽略/排除主機 {#ignore-/-exclude-hosts}

如果輸出變得過於雜亂，您可以選擇忽略或排除位置。您可以執行下列任一操作來忽略或排除位置：

- 以滑鼠右鍵按一下您要忽略的請求，然後選取「忽略」
- 手動新增要排除的位置 `\[ *Proxy -\> Recording Settings... -\> Exclude* \]`

 
## DNS欺騙 {#dns-spoffing}

`\[ *Tools -\> DNS Spoofing...* \]`

 

嘗試將請求重新導向至不同IP時（尤其是使用行動裝置時）,DNS欺騙非常有用：

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/DNSSpoofing.PNG)

<http://www.charlesproxy.com/documentation/tools/dns-spoofing/>

 
## 映射遠程 {#map-remote}

`\[ *Tools -\> Map Remote...* \]`

 

使用映射遠程，您可以將「傳入」請求重定向到其他端點。 此功能最常見的使用案例是「對應」 `AccessEnabler.swf` to `AccessEnablerDebug.swf:`

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/MapRemote.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/MapRemoteAdd.PNG)

<http://www.charlesproxy.com/documentation/tools/map-remote/>

 

## 反向代理 {#reverse-proxy}

<http://www.charlesproxy.com/documentation/proxying/reverse-proxy/>

## 行動 {#mobile}

### 在iOS裝置上使用Charles(iPhone / iPad) {#use-charles-on-an-ios-device-(iphone-/-ipad)}

#### 從iPhone進行SSL連線 {#ssl-connection-from-iphone}

瀏覽至 <http://charlesproxy.com/charles.crt> 從iOS裝置。  這將啟動證書安裝對話框：

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate1\(1\)。PNG)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate2\(1\)。PNG)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate3.PNG)

 </br>

按一下 `\[ *Install*... *Install*... *Done* \]` 完成證書安裝。

<http://www.charlesproxy.com/documentation/faqs/ssl-connections-from-within-iphone-applications/>

 

#### 從iOS裝置使用Charles {#using-charles-from-an-ios-device}

在iOS裝置上選取 `\[ *Settings* -\> *Wi-FI* -\> (*YOUR\_WIFI\_NETWORK)* \]`. 按一下網路旁的藍色小箭頭，然後下到HTTP代理並選擇「手動」： 


 </br>

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy1.png)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy2.PNG)


 </br>
在此，您需要指定運行Charles的電腦的IP和埠。 <span style="line-height: 1.6em;">如果您現在在iOS裝置上開啟Safari，並嘗試開啟網頁，在執行Charles的電腦上應該會出現下列快顯視窗：
 
 </br>

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy3.PNG)

</br>
按一下「允許」，允許裝置使用Charles來代理其所有請求。

<http://www.charlesproxy.com/documentation/faqs/using-charles-from-an-iphone/>


#### iOS — 信任任何憑證 {#ios-trust-any-certificates}

<http://stackoverflow.com/questions/933331/how-to-use-nsurlconnection-to-connect-with-ssl-for-an-untrusted-cert>

#### iOS驗證錯誤 — 找不到adobepass.ios.app

<https://tve.zendesk.com/entries/22135907-ios-authentication-error-adobepass-ios-app-cannot-be-found>


## 使用Charles for Android

<http://jaanus.com/post/17476995356/debugging-http-on-an-android-phone-or-tablet-with>

<http://www.charlesproxy.com/documentation/configuration/browser-and-system-configuration>


瀏覽至 [Charles Proxy](http://charlesproxy.com/charles.crt) 從Android裝置。
