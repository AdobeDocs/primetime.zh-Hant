---
title: 預轉碼API
description: 您可以使用即時重新封裝API來提前轉碼廣告創意素材，如此就可視需要提供內容相容版本，避免與即時(JIT)重新封裝相關的2-4分鐘延遲。
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---


# 預轉碼和重新封裝API {#pre-transcoding-api}

PrimetimeAd Insertion針對預先知道創意URL的情況（例如大型直銷事件）提供轉碼前API。  如此可免除與即時轉碼相關的2-4分鐘延遲。

## HTTP請求{#section_F616F5722F0B4AB7939EE2ECBEDDB297}

傳送HTTPPOST命令至指定的URL，以告知CRS您要轉碼的廣告創意素材，以及您想要使用哪些選項。 回應程式碼會報告成功或失敗以及其他資訊。

此請求需要使用者名稱和密碼。 您可向Adobe技術客戶經理取得這些資訊。 如果您需要驗證相關資訊，請連絡您的Adobe Primetime啟用代表。

若要將轉碼請求提交給CRS，請傳送HTTP訊息，如下所示：

* **URL -** [https://id3.auditude.com/repackage](https://id3.auditude.com/repackage)

* **方法-** `POST`

* **驗證-** `Digest`

* **頁首-** `Content-Type: text/xml`

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

Body中的`RepackageList`塊可以包含1到300個`Repackage`塊。 如果內文中的`Repackage`區塊數超過300，則HTTP請求將失敗，並出現下列錯誤：

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


`Repackage`塊中的必需和可選參數如下：

* **`AdSystem`** （必要）-來源廣告伺服器，例如 `Auditude`, `FreeWheel`、 `Apad.tv`。這是與VAST元素`AdSystem`對應的字串值。

* **`AdId`** （必要）-這是請求中指定之第三方廣告伺服器的識別碼。它對應於VAST響應中`Ad`元素的`id`屬性。

* **`CreativeURL`** （必要）-要轉碼的廣告創意素材的位置(URI)。這對應於VAST `MediaFile`元素。

* `CreativeID` （選用）-廣告創意的識別碼，將會納入廣告體驗。
* **`Zone`** （必要）-您帳戶的區域ID（請向技術客戶經理取得）。這是與Auditude平台`publisher_site_id`設定相對應的數值。

* **`Format`** （可選）-控制CRS如何轉碼廣告創意的參數：

   * `clientside` -產生與TVSDK用來與CDN通訊的URL相容的輸出。
   >[!IMPORTANT]
   >
   >如果您想要重新封裝的廣告與用戶端Ad Insertion相容，您必須提供此參數。 如果您未提供此功能，則重新封裝的廣告將僅與伺服器端Ad Insertion相容。

   * `hls` -產生HLS相容的轉碼廣告創意。
   * `dash` -產生與DASH相容的轉碼廣告創意。
   * `id3` -將ID3計時中繼資料標籤插入轉碼廣告創意素材。
   * `targetdur` -轉碼廣告創意素材的區段持續時間（以秒為單位）。預設值為`targetdur=4`。 此值應與目標持續時間標籤中資訊清單中指定的`<s>`值相對應：`#EXT-X-TARGETDURATION:<s>`。

   >[!NOTE]
   >
   >與DASH相容的資產與Adobe Primetime廣告插入不相容。

>[!IMPORTANT]
>
>為確保播放順暢，請設定`targetdur`以符合內容區塊持續時間。

## HTTP響應{#section_B30D27E4A6AC4AAD9E758162EFF7D963}

CRS以下列其中一個狀態代碼回應請求：

* **HTTP 202** -已接受（內文為空）。這表示成功。 CRS會上傳轉碼廣告至CDN伺服器。
* **HTTP 400** -請求錯誤。張貼的XML無效。
* **HTTP 500**  —— 內部伺服器錯誤。伺服器遇到內部問題（例如，伺服器無法連接到資料庫）。

## SSAI或CSAI {#section_098888BB74FD4DC1AD0BD507B2A48318}的預轉碼資產

使用重新封裝API，您可以預先轉碼未來的SSAI或CSAI事件。 如果資產日後要與SSAI搭配使用，請確定POST呼叫中的所有參數都是唯一的。 參數包括：AdSystem、AdId、CreativeURL、Zone、Format。 這組參數中的任何差異都會導致新的SSAI轉碼要求。

對於未來與CSAI搭配使用的資產，資產獨特性取決於Zone和CreativeURL。 AdSystem和AdId不會產生不同的轉碼資產，而且這些資產可供客戶使用。
