---
description: 您可以使用CRS重新封裝API來提前轉碼非HLS廣告創作元素，因此當您需要執行HLS版本時，就可使用HLS版本，避免與即時(JIT)重新封裝相關的2-4分鐘延遲。
seo-description: 您可以使用CRS重新封裝API來提前轉碼非HLS廣告創作元素，因此當您需要執行HLS版本時，就可使用HLS版本，避免與即時(JIT)重新封裝相關的2-4分鐘延遲。
seo-title: 重新封裝API
title: 重新封裝API
uuid: 03cd2428-510a-4b99-8496-059a48d5abba
translation-type: tm+mt
source-git-commit: 5c026bfc678bafc08f93ad056823e36fd77a8a25

---


# 重新封裝API {#repackaging-api}

您可以使用CRS重新封裝API來提前轉碼非HLS廣告創作元素，因此當您需要執行HLS版本時，就可使用HLS版本，避免與即時(JIT)重新封裝相關的2-4分鐘延遲。

## HTTP請求 {#section_F616F5722F0B4AB7939EE2ECBEDDB297}

傳送HTTP POST命令至指定的URL，以告知CRS您要轉碼的廣告創意素材，以及您想要使用哪些選項。 回應程式碼會報告成功或失敗以及其他資訊。

此請求需要使用者名稱和密碼。 您可向Adobe技術客戶經理取得這些資訊。 如果您需要驗證的相關資訊，請連絡您的Adobe Primetime啟用代表。

若要將轉碼請求提交給CRS，請傳送HTTP訊息，如下所示：

* **URL -**[https://id3.auditude.com/repackage](https://id3.auditude.com/repackage)

* **方法-**`POST`

* **驗證-**`Digest`

* **標題-**`Content-Type: text/xml`

* **Body -** XML，如下例所示：

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

主體 `RepackageList` 中的塊可以包含1到300個 `Repackage` 塊。 如果內文中 `Repackage` 的區塊數超過300，則HTTP請求將失敗，並出現下列錯誤：

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


塊中的必需和可選參 `Repackage` 數如下：

* **`AdSystem`** （必要）-來源廣告伺服器，例如 `Auditude`, `FreeWheel`、 `Apad.tv`。 這是與VAST元素對應的字串值 `AdSystem`。

* **`AdId`** （必要）-這是請求中指定之第三方廣告伺服器的識別碼。 它對應於VAST `id` 響應中 `Ad` 的元素屬性。

* **`CreativeURL`** （必要）-要轉碼的廣告創意素材的位置(URI)。 這與VAST元素相 `MediaFile` 對應。

* `CreativeID` （選用）-廣告創意的識別碼，將會納入廣告體驗。
* **`Zone`** （必要）-您帳戶的區域ID（請向技術客戶經理取得）。 這是與Auditude平台設定相對應的數 `publisher_site_id` 值。

* **`Format`** （可選）-控制CRS如何轉碼廣告創意的參數：

   * `clientside` -產生與TVSDK用來與CDN通訊的URL相容的輸出。
   >[!IMPORTANT]
   >
   >如果您希望重新封裝的廣告與「用戶端廣告插入」相容，您必須提供此參數。 如果您未提供此功能，重新封裝的廣告將只與「伺服器端廣告插入」相容。

   * `hls` -產生HLS相容的轉碼廣告創意。
   * `dash` -產生與DASH相容的轉碼廣告創意。
   * `id3` -將ID3計時中繼資料標籤插入轉碼廣告創意素材。
   * `targetdur` -轉碼廣告創意素材的區段持續時間（以秒為單位）。 預設為 `targetdur=4`。 此值應與資訊清單中指定的目標持續時 `<s>` 間標籤的值相對應： `#EXT-X-TARGETDURATION:<s>`。
   >[!NOTE]
   >
   >與DASH相容的資產與Adobe Primetime廣告插入不相容。

>[!IMPORTANT]
>
>為確保播放順暢，請設 `targetdur` 定為符合內容區塊持續時間。

## HTTP回應 {#section_B30D27E4A6AC4AAD9E758162EFF7D963}

CRS以下列其中一個狀態代碼回應請求：

* **HTTP 202** —— 已接受（內文為空）。 這表示成功。 CRS會上傳轉碼廣告至CDN伺服器。
* **HTTP 400** —— 請求錯誤。 張貼的XML無效。
* **HTTP 500** —— 內部伺服器錯誤。 伺服器遇到內部問題（例如，伺服器無法連接到資料庫）。

## SSAI或CSAI的預轉碼資產 {#section_098888BB74FD4DC1AD0BD507B2A48318}

使用重新封裝API，您可以預先轉碼未來的SSAI或CSAI事件。 如果資產日後要與SSAI搭配使用，請確定POST呼叫中的所有參數都是唯一的。 參數包括：AdSystem、AdId、CreativeURL、Zone、Format。 這組參數中的任何差異都會導致新的SSAI轉碼要求。

對於未來與CSAI搭配使用的資產，資產獨特性取決於Zone和CreativeURL。 AdSystem和AdId不會產生不同的轉碼資產，而且這些資產可供客戶使用。
