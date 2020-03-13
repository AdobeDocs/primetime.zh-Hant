---
description: 例如，當整個播放清單遺失時，當頂層資訊清單檔案中指定的M3U8檔案未下載時，TVSDK會嘗試復原。 如果無法恢復，則您的應用程式將決定下一步。
seo-description: 例如，當整個播放清單遺失時，當頂層資訊清單檔案中指定的M3U8檔案未下載時，TVSDK會嘗試復原。 如果無法恢復，則您的應用程式將決定下一步。
seo-title: 遺失播放清單容錯功能
title: 遺失播放清單容錯功能
uuid: 91a537f3-3e69-4669-8f84-0292c19ac209
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 遺失播放清單容錯功能{#missing-playlist-failover}

例如，當整個播放清單遺失時，當頂層資訊清單檔案中指定的M3U8檔案未下載時，TVSDK會嘗試復原。 如果無法恢復，則您的應用程式將決定下一步。

如果遺失與中解析度位元速率相關聯的播放清單，TVSDK會以相同解析度搜尋變型播放清單。 如果找到相同的解析度，就會開始從相符位置下載變型播放清單和區段。 如果TVSDK找不到相同的解析度播放清單，它會嘗試循環檢視其他位元速率播放清單及其變數。 位元速率立即降低是首選，然後是其變體，依此類推。 如果所有較低位元速率的播放清單及其變數在嘗試尋找有效播放清單時已用盡，TVSDK會移至最高位元速率，並從此計算。 如果找不到有效的播放清單，程式會失敗，而播放器會移至ERROR狀態。

您的應用程式可判斷如何處理此情況。 例如，您可能想要關閉播放器活動，並將使用者導向目錄活動。 感興趣的事件是事 `STATE_CHANGED` 件，對應的回呼是方 `onStateChanged` 法。 以下程式碼會監視播放器是否將內部狀態變更為ERROR:

```java
case ERROR: 
    getActivity().finish(); // this is where we close the current activity (the Player activity) 
    break;
```

如需詳細資訊，請參 [!DNL PlayerFragment.java] 閱SDK中的檔案：

```
[…]/samples/PrimetimeReference/src/PrimetimeReference/src/com/adobe/primetime/reference/ui/player/
```

如果客戶端網路關閉，您可以使用此代碼進行驗證。

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

API將提供用於驗證客戶端網路是否關閉的URL。 此URL應為有效的URL，會在http請求上傳回http回應代碼200。

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

如果未設定setNetworkDownVerificationUrl,TVSDK會依預設使用MainManifest URL來判斷網路是否關閉。
