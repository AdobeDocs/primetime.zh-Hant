---
description: 當整個播放清單遺失時，例如當頂層資訊清單檔案中指定的M3U8檔案未下載時，TVSDK會嘗試復原。 如果無法復原，您的應用程式會決定下一個步驟。
title: 缺少播放清單容錯移轉
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# 缺少播放清單容錯移轉{#missing-playlist-failover}

當整個播放清單遺失時，例如當頂層資訊清單檔案中指定的M3U8檔案未下載時，TVSDK會嘗試復原。 如果無法復原，您的應用程式會決定下一個步驟。

如果缺少與中等解析度位元速率關聯的播放清單，TVSDK會搜尋具有相同解析度的變體播放清單。 如果找到相同的解析度，會開始從相符位置下載變體播放清單和區段。 如果TVSDK找不到相同解析度的播放清單，則會嘗試循環播放其他位元速率播放清單及其變體。 立即較低的位元速率是第一個選擇，然後是它的變體，依此類推。 如果嘗試尋找有效播放清單時，所有較低位元速率的播放清單及其變體都已耗盡，TVSDK將會移至最高位元速率，並從此處開始計數。 如果找不到有效的播放清單，程式會失敗，播放器會變成ERROR狀態。

您的應用程式會決定如何處理這種情況。 例如，您可以關閉播放器活動，並將使用者導向目錄活動。 感興趣的事件是 `STATE_CHANGED` 事件，而對應的回呼為 `onStateChanged` 方法。 以下是監控播放器是否將其內部狀態變更為錯誤的程式碼：

```java
case ERROR: 
    getActivity().finish(); // this is where we close the current activity (the Player activity) 
    break;
```

如需詳細資訊，請參閱 [!DNL PlayerFragment.java] SDK中的檔案：

```
[…]/samples/PrimetimeReference/src/PrimetimeReference/src/com/adobe/primetime/reference/ui/player/
```

如果使用者端網路已關閉，您可以使用此代碼進行驗證。

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

API會提供用於驗證使用者端網路是否關閉的URL。 此URL應為有效的URL，會在http要求上傳回http回應代碼200。

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

如果未設定setNetworkDownVerificationUrl，TVSDK預設會使用MainManifest URL來判斷網路是否關閉。
