---
description: 您可以使用CRS重新封裝API來預先轉碼非HLS廣告創意，因此當您需要執行時，可以使用HLS版本，消除與即時(JIT)重新封裝相關的2至4分鐘延遲。
title: 重新封裝API
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---


# 重新封裝API {#repackaging-api}

您可以使用CRS重新封裝API來預先轉碼非HLS廣告創意，因此當您需要執行時，可以使用HLS版本，消除與即時(JIT)重新封裝相關的2至4分鐘延遲。

## HTTP要求 {#section_F616F5722F0B4AB7939EE2ECBEDDB297}

傳送HTTPPOST命令至指定的URL，告訴CRS您要轉碼哪些廣告創意，以及您想使用哪些選項。 回應代碼會報告成功或失敗以及其他資訊。

此請求需要使用者名稱和密碼。 您可以向Adobe技術客戶經理索取。 如果您需要有關驗證的資訊，請聯絡您的Adobe Primetime啟用代表。

若要提交轉碼請求給CRS，請傳送HTTP訊息，如下所示：

* **URL -** [https://id3.auditude.com/repackage](https://id3.auditude.com/repackage)

* **方法 —** `POST`

* **驗證 —** `Digest`

* **頁首 —** `Content-Type: text/xml`

* **內文 —** XML，如下列範例所示：

   ```xml
   <RepackageList>
       <Repackage>
           <AdSystem>Auditude</AdSystem>
           <AdID>AUD1</AdID>
           <CreativeID>AUD-CR1</CreativeID>
           <CreativeURL>https://cdn.auditude.com/assets/ip/starbucks2.mp4</CreativeURL>
           <Zone>3</Zone>
       </Repackage>
       <Repackage>
           <AdSystem>Auditude</AdSystem>
           <AdID>AUD2</AdID>
           <CreativeID>AUD-CR1</CreativeID>
           <CreativeURL>https://cdn.auditude.com/assets/ip/starbucks2.mp4</CreativeURL>
           <Format>id3 targetdur=5</Format>
           <Zone>3</Zone>
       </Repackage>
   </RepackageList>
   ```

此 `RepackageList` 內文中的區塊可包含1到300 `Repackage` 個區塊。 如果數量 `Repackage` 內文中的區塊超過300個，則HTTP請求將失敗，並出現以下錯誤：

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


中的必要和選用引數 `Repackage` 區塊如下所示：

* **`AdSystem`** （必要） — 來源廣告伺服器，例如， `Auditude`， `FreeWheel`， `Apad.tv`. 這是對應至VAST元素的字串值 `AdSystem`.

* **`AdId`** （必要） — 這是要求中指定的第三方廣告伺服器的識別碼。 它對應至 `id` 的屬性 `Ad` VAST回應中的元素。

* **`CreativeURL`** （必要） — 要轉碼的廣告創意位置(URI)。 此專案對應至VAST `MediaFile` 元素。

* `CreativeID` （選用） — 要包含在廣告體驗中的廣告創意識別碼。
* **`Zone`** （必要） — 您帳戶的區域ID （請向您的技術客戶經理取得）。 這是對應至Auditude平台的數值 `publisher_site_id` 設定。

* **`Format`** （選用） — 控制CRS如何轉碼廣告創意的引數：

   * `clientside`  — 產生與TVSDK用來與CDN通訊的URL相容的輸出。
   >[!IMPORTANT]
   >
   >如果您希望重新封裝的廣告和使用者端Ad Insertion相容，則必須提供此引數。 如果您不提供此功能，重新封裝的廣告只會與伺服器端Ad Insertion相容。

   * `hls`  — 產生與HLS相容的轉碼廣告創意。
   * `dash`  — 產生與DASH相容的轉碼廣告創意。
   * `id3`  — 將ID3計時中繼資料標籤插入轉碼廣告創意中。
   * `targetdur`  — 轉碼廣告創意的區段持續時間（秒）。 預設為 `targetdur=4`. 此值應該對應至資訊清單中指定的值 `<s>` 在目標持續時間標籤中： `#EXT-X-TARGETDURATION:<s>`.

   >[!NOTE]
   >
   >DASH相容資產與Adobe Primetime廣告插入不相容。

>[!IMPORTANT]
>
>若要確保最流暢的播放，請設定 `targetdur` 以符合內容區塊持續時間。

## HTTP回應 {#section_B30D27E4A6AC4AAD9E758162EFF7D963}

CRS會使用下列其中一個狀態代碼來回應要求：

* **HTTP 202**  — 已接受（內文空白）。 這表示成功。 CRS會將轉碼廣告上傳至CDN伺服器。
* **HTTP 400**  — 錯誤請求。 張貼的XML無效。
* **HTTP 500**  — 內部伺服器錯誤。 伺服器發生內部問題（例如，伺服器無法連線到資料庫）。

## 為SSAI或CSAI預先轉碼資產 {#section_098888BB74FD4DC1AD0BD507B2A48318}

使用重新封裝API，您可以預先轉碼未來的SSAI或CSAI事件。 如果資產預計在未來與SSAI搭配使用，請確定POST呼叫中的所有引數都是唯一的。 引數為：AdSystem、AdId、CreativeURL、Zone、Format。 這組引數中的任何差異，都會導致SSAI有新的轉碼要求。

對於日後與CSAI一起使用的資產，資產的唯一性取決於Zone和CreativeURL。 AdSystem和AdId不會產生不同的轉碼資產，這些資產可供使用者端使用。
