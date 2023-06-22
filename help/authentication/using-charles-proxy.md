---
title: 使用Charles Proxy
description: 使用Charles Proxy
exl-id: bb38543f-f6bc-4b5a-91b8-41bc51ee4c56
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 使用Charles Proxy {#using-charles-proxy}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。


**Charles：** <http://charlesproxy.com>

 
## 下載、安裝並開始使用Charles Proxy {#download-install-and-get-stared-with-charles-proxy}

- **下載** - <http://www.charlesproxy.com/download/>
- **安裝** - <http://www.charlesproxy.com/documentation/installation/>
- **快速入門** - <http://www.charlesproxy.com/documentation/getting-started/>

 
## 結構與序列標籤 {#structure-vs-sequence-tabs}

有兩種不同的方式檢視流量：

1. **結構**  — 依主機將請求分組
1. **序列**  — 要求會依呼叫的順序列出


## SSL和憑證 {#ssl-and-certificates}

啟用SSL代理 `\[ *Proxy -\> Proxy Settings... -\> SSL* \]`

勾選「啟用SSL代理」核取方塊，然後新增所有HTTPS位置。


![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/ProxySettings.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/SSLSettings.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AddHttpsLocations.PNG)



- SSL代理 —  <http://www.charlesproxy.com/documentation/proxying/ssl-proxying/>
- SSL憑證 —  <http://www.charlesproxy.com/documentation/using-charles/ssl-certificates/>
- 從行動裝置進行SSL代理 — 請參閱下文。

 
## 忽略/排除主機 {#ignore-/-exclude-hosts}

如果您的輸出變得過於雜亂，您可以選擇忽略或排除位置。您可以執行下列任一項作業來忽略或排除位置：

- 以滑鼠右鍵按一下您要忽略的請求，然後選取「忽略」
- 手動新增要從中排除的位置 `\[ *Proxy -\> Recording Settings... -\> Exclude* \]`

 
## DNS欺騙 {#dns-spoffing}

`\[ *Tools -\> DNS Spoofing...* \]`

 

嘗試將請求重新導向至不同的IP時，DNS詐騙會很有用，尤其是使用行動裝置時：

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/DNSSpoofing.PNG)

<http://www.charlesproxy.com/documentation/tools/dns-spoofing/>

 
## 對應遠端 {#map-remote}

`\[ *Tools -\> Map Remote...* \]`

 

透過對應遠端，您可以將「傳入」要求重新導向至不同的端點。 此功能最常見的使用案例是「對應」 `AccessEnabler.swf` 至 `AccessEnablerDebug.swf:`

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/MapRemote.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/MapRemoteAdd.PNG)

<http://www.charlesproxy.com/documentation/tools/map-remote/>

 

## 反向Proxy {#reverse-proxy}

<http://www.charlesproxy.com/documentation/proxying/reverse-proxy/>

## 行動 {#mobile}

### 在iOS裝置(iPhone / iPad)上使用Charles {#use-charles-on-an-ios-device-(iphone-/-ipad)}

#### iPhone的SSL連線 {#ssl-connection-from-iphone}

瀏覽至 <http://charlesproxy.com/charles.crt> 從您的iOS裝置。  這會啟動憑證安裝對話方塊：

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate1\(1\)。PNG)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate2\(1\)。PNG)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate3.PNG)

 </br>

按一下 `\[ *Install*... *Install*... *Done* \]` 以完成憑證的安裝。

<http://www.charlesproxy.com/documentation/faqs/ssl-connections-from-within-iphone-applications/>

 

#### 從iOS裝置使用Charles {#using-charles-from-an-ios-device}

在您的iOS裝置上選取 `\[ *Settings* -\> *Wi-FI* -\> (*YOUR\_WIFI\_NETWORK)* \]`. 按一下網路旁的藍色小箭頭，然後向下移至HTTP Proxy並選取「手動」： 


 </br>

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy1.png)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy2.PNG)


 </br>
您必須在此指定執行Charles的電腦的IP和連線埠。 <span style="line-height: 1.6em;">如果您現在在iOS裝置上開啟Safari，並嘗試開啟網頁，則執行Charles的電腦上應該會出現下列快顯視窗：
 
 </br>

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy3.PNG)

</br>
按一下「允許」以允許裝置使用Charles代理其所有請求。

<http://www.charlesproxy.com/documentation/faqs/using-charles-from-an-iphone/>


#### iOS — 信任任何憑證 {#ios-trust-any-certificates}

<http://stackoverflow.com/questions/933331/how-to-use-nsurlconnection-to-connect-with-ssl-for-an-untrusted-cert>

#### iOS驗證錯誤 — 找不到adobepass.ios.app

<https://tve.zendesk.com/entries/22135907-ios-authentication-error-adobepass-ios-app-cannot-be-found>


## 使用Charles for Android

<http://jaanus.com/post/17476995356/debugging-http-on-an-android-phone-or-tablet-with>

<http://www.charlesproxy.com/documentation/configuration/browser-and-system-configuration>


瀏覽至 [Charles Proxy](http://charlesproxy.com/charles.crt) （從您的Android裝置）。
