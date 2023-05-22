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
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。


**查爾斯：** <http://charlesproxy.com>

 
## 下載、安裝和開始使用Charles代理 {#download-install-and-get-stared-with-charles-proxy}

- **下載** - <http://www.charlesproxy.com/download/>
- **安裝** - <http://www.charlesproxy.com/documentation/installation/>
- **入門** - <http://www.charlesproxy.com/documentation/getting-started/>

 
## 結構與序列頁籤 {#structure-vs-sequence-tabs}

查看流量有兩種不同的方法：

1. **結構**  — 請求按主機分組
1. **序列**  — 請求按調用順序列出


## SSL和證書 {#ssl-and-certificates}

啟用SSL代理 `\[ *Proxy -\> Proxy Settings... -\> SSL* \]`

選中「啟用SSL代理」複選框，並添加所有HTTPS位置。


![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/ProxySettings.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/SSLSettings.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AddHttpsLocations.PNG)



- SSL代理 —  <http://www.charlesproxy.com/documentation/proxying/ssl-proxying/>
- SSL證書 —  <http://www.charlesproxy.com/documentation/using-charles/ssl-certificates/>
- SSL從移動設備代理 — 請參閱下面。

 
## 忽略/排除主機 {#ignore-/-exclude-hosts}

如果輸出變得過於混亂，您可以選擇忽略或排除位置。您可以通過執行以下任一操作來忽略或排除位置：

- 按一下右鍵要忽略的請求，然後選擇「忽略」
- 手動添加要從中排除的位置 `\[ *Proxy -\> Recording Settings... -\> Exclude* \]`

 
## DNS欺騙 {#dns-spoffing}

`\[ *Tools -\> DNS Spoofing...* \]`

 

當嘗試將請求重定向到其他IP時，DNS欺騙非常有用，特別是當使用移動設備時：

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/DNSSpoofing.PNG)

<http://www.charlesproxy.com/documentation/tools/dns-spoofing/>

 
## 映射遠程 {#map-remote}

`\[ *Tools -\> Map Remote...* \]`

 

使用map remote ，您可以將「傳入」請求重定向到其他端點。 此功能最常用的用例是「映射」 `AccessEnabler.swf` 至 `AccessEnablerDebug.swf:`

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/MapRemote.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/MapRemoteAdd.PNG)

<http://www.charlesproxy.com/documentation/tools/map-remote/>

 

## 反向代理 {#reverse-proxy}

<http://www.charlesproxy.com/documentation/proxying/reverse-proxy/>

## 移動 {#mobile}

### 在iOS設備上使用Charles(iPhone/iPad) {#use-charles-on-an-ios-device-(iphone-/-ipad)}

#### 來自iPhone的SSL連接 {#ssl-connection-from-iphone}

瀏覽到 <http://charlesproxy.com/charles.crt> 從你的iOS裝置里。  這將啟動證書安裝對話框：

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate1\(1\)。PNG)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate2\(1\)。PNG)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate3.PNG)

 </br>

按一下 `\[ *Install*... *Install*... *Done* \]` 完成證書安裝。

<http://www.charlesproxy.com/documentation/faqs/ssl-connections-from-within-iphone-applications/>

 

#### 用iOS裝置的查爾斯 {#using-charles-from-an-ios-device}

在您的iOS設備上選擇 `\[ *Settings* -\> *Wi-FI* -\> (*YOUR\_WIFI\_NETWORK)* \]`。 按一下網路旁的藍色小箭頭，然後下到HTTP代理並選擇「手動」： 


 </br>

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy1.png)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy2.PNG)


 </br>
在此，您需要指定運行Charles的電腦的IP和埠。 <span style="line-height: 1.6em;">如果您現在在iOS設備上開啟Safari並嘗試開啟網頁，則應在運行Charles的電腦上獲得以下彈出窗口：
 
 </br>

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy3.PNG)

</br>
按一下「允許」允許設備使用Charles代理其所有請求。

<http://www.charlesproxy.com/documentation/faqs/using-charles-from-an-iphone/>


#### iOS — 信任任何證書 {#ios-trust-any-certificates}

<http://stackoverflow.com/questions/933331/how-to-use-nsurlconnection-to-connect-with-ssl-for-an-untrusted-cert>

#### iOS驗證錯誤 — 找不到adobepass.ios.app

<https://tve.zendesk.com/entries/22135907-ios-authentication-error-adobepass-ios-app-cannot-be-found>


## 使用Charles for Android

<http://jaanus.com/post/17476995356/debugging-http-on-an-android-phone-or-tablet-with>

<http://www.charlesproxy.com/documentation/configuration/browser-and-system-configuration>


瀏覽到 [查爾斯代理](http://charlesproxy.com/charles.crt) 你的安卓設備。
