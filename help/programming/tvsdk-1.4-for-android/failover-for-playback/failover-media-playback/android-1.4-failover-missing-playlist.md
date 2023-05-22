---
description: 當缺少整個播放清單時，例如，當在頂級清單檔案中指定的M3U8檔案未下載時，TVSDK會嘗試恢復。 如果無法恢復，則應用程式將確定下一步。
title: 缺少播放清單故障轉移
exl-id: aab2dde3-aee2-4ade-b8f9-91c72df0c747
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# 缺少播放清單故障轉移{#missing-playlist-failover}

當缺少整個播放清單時，例如，當在頂級清單檔案中指定的M3U8檔案未下載時，TVSDK會嘗試恢復。 如果無法恢復，則應用程式將確定下一步。

如果缺少與中解析度位速率關聯的播放清單，TVSDK將搜索相同解析度的變型播放清單。 如果找到相同的解析度，則開始從匹配位置下載變型播放清單和段。 如果TVSDK找不到相同的解析度播放清單，它將嘗試循環播放其他比特率播放清單及其變體。 立即降低比特率是首選，然後是其變數，等等。 如果在嘗試查找有效播放清單時已用盡所有低比特率播放清單及其變體，則TVSDK將轉到最高比特率並從那裡計算下來。 如果找不到有效的播放清單，則進程將失敗，並且播放器將移到ERROR狀態。

您的應用程式可以確定如何處理此情況。 例如，您可能希望關閉播放器活動並將用戶引導到目錄活動。 感興趣的事件是 `STATE_CHANGED` 事件，相應的回調是 `onStateChanged` 的雙曲餘切值。 下面是代碼，用於監視播放器是否將其內部狀態更改為ERROR:

```java
case ERROR: 
    getActivity().finish(); // this is where we close the current activity (the Player activity) 
    break;
```

有關詳細資訊，請參見 [!DNL PlayerFragment.java] SDK中的檔案：

```
[…]/samples/PrimetimeReference/src/PrimetimeReference/src/com/adobe/primetime/reference/ui/player/
```

如果客戶端網路已關閉，則可以使用此代碼進行驗證。

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

API將提供用於驗證客戶端網路是否關閉的url。 這應該是有效的url，它在http請求上返回http響應代碼200。

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

如果未設定setNetworkDownVerificationUrl，則TVSDK預設使用MainManifest URL來確定網路是否關閉。
