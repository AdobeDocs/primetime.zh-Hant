---
description: 您可以使用CRS重新打包API提前對非HLS廣告創意進行代碼轉換，因此在需要運行HLS版本時，HLS版本可用，從而消除了與即時(JIT)重新打包相關的2-4分鐘延遲。
title: 重新打包API
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---


# 重新打包API {#repackaging-api}

您可以使用CRS重新打包API提前對非HLS廣告創意進行代碼轉換，因此在需要運行HLS版本時，HLS版本可用，從而消除了與即時(JIT)重新打包相關的2-4分鐘延遲。

## HTTP請求 {#section_F616F5722F0B4AB7939EE2ECBEDDB297}

將HTTPPOST命令發送到指定的URL，以告訴CRS您要轉換哪些廣告和希望使用哪些選項。 響應代碼報告成功或失敗以及其他資訊。

此請求需要用戶名和密碼。 您可以從Adobe技術客戶經理處獲取這些資訊。 如果您需要有關驗證的資訊，請與Adobe Primetime支援代表聯繫。

要向CRS提交轉碼請求，請發送HTTP消息，如下所示：

* **URL -** [https://id3.auditude.com/repackage](https://id3.auditude.com/repackage)

* **方法 —** `POST`

* **身份驗證 —** `Digest`

* **標題 —** `Content-Type: text/xml`

* **正文 —** XML，如下例所示：

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

的 `RepackageList` 正文中的塊可以包含1到300 `Repackage` 塊。 如果 `Repackage` Body中的塊超過300，則HTTP請求將失敗，並出現以下錯誤：

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


中的必需和可選參數 `Repackage` 塊如下所示：

* **`AdSystem`** （必需） — 源和伺服器，例如， `Auditude`。 `FreeWheel`。 `Apad.tv`。 這是與VAST元素對應的字串值 `AdSystem`。

* **`AdId`** （必需） — 這是請求中指定的第三方和伺服器的標識符。 它與 `id` 屬性 `Ad` VAST響應中的元素。

* **`CreativeURL`** （必需） — 要轉碼的廣告創意的位置(URI)。 這對應於 `MediaFile` 的子菜單。

* `CreativeID` （可選） — 作為廣告體驗一部分要包括的廣告創意的標識符。
* **`Zone`** （必需） — 帳戶的區域ID（從技術客戶經理處獲取）。 這是一個與Auditude平台相對應的數值 `publisher_site_id` 的子菜單。

* **`Format`** （可選） — 控制CRS如何轉換廣告創意的參數：

   * `clientside`  — 生成與TVSDK用於與CDN通信的URL相容的輸出。
   >[!IMPORTANT]
   >
   >如果希望重新打包的廣告與客戶端Ad Insertion相容，則必須提供此參數。 如果不提供此功能，則重新打包的廣告將僅與伺服器端Ad Insertion相容。

   * `hls`  — 生成與HLS相容的轉碼廣告創意。
   * `dash`  — 生成與DASH相容的轉碼廣告創意。
   * `id3`  — 將ID3定時元資料標籤插入已轉碼和創意。
   * `targetdur`  — 轉碼廣告創意的段持續時間（秒）。 預設值為 `targetdur=4`。 此值應與清單中指定的值相對應 `<s>` 在目標持續時間標籤中： `#EXT-X-TARGETDURATION:<s>`。

   >[!NOTE]
   >
   >與DASH相容的資產與Adobe Primetime廣告插入不相容。

>[!IMPORTANT]
>
>要確保最平穩的回放，請設定 `targetdur` 匹配內容塊持續時間。

## HTTP響應 {#section_B30D27E4A6AC4AAD9E758162EFF7D963}

CRS使用以下狀態代碼之一響應請求：

* **HTTP 202**  — 已接受（正文為空）。 這表示成功。 CRS將轉碼廣告上載到CDN伺服器。
* **HTTP 400**  — 錯誤請求。 已發佈的XML無效。
* **HTTP 500**  — 內部伺服器錯誤。 伺服器遇到內部問題（例如，伺服器無法連接到資料庫）。

## SSAI或CSAI的預轉碼資產 {#section_098888BB74FD4DC1AD0BD507B2A48318}

使用重新打包API，可以預轉碼將來的SSAI或CSAI事件。 如果資產將來要與SSAI一起使用，請確保POST調用中的所有參數都是唯一的。 參數包括：AdSystem、AdId、CreativeURL、區域、格式。 這組參數中的任何差異都會導致對SSAI的新轉碼請求。

對於將來與CSAI一起使用的資產，資產唯一性取決於Zone和CreativeURL。 AdSystem和AdId不會導致不同的轉碼資產，這些資產可供客戶端使用。
