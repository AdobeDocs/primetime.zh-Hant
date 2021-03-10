---
description: 測試過程中常見的問題通常涉及您的ExpressPlay驗證器、傳輸協定和所需的服務請求參數。
title: 疑難排解快速入門
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# 疑難排解快速入門{#troubleshooting-your-quick-start}

測試過程中常見的問題通常涉及您的ExpressPlay驗證器、傳輸協定和所需的服務請求參數。

如果您的[!DNL curl]要求ExpressPlay產生代號失敗，回應內文將包含錯誤訊息，說明失敗的原因。

如果代號產生成功，但內容仍無法播放，請檢查ExpressPlay代號兌換記錄是否有錯誤，例如「過期代號」。

如果代號產生成功且兌換沒有錯誤，但視訊仍然無法播放，請檢查CEK是否符合內容，以及內容格式是否符合目標裝置的功能。

此外：

* 檢查您在服務請求中是否使用正確的客戶驗證器。 當您想要使用測試驗證器時，很容易意外使用生產驗證器。 此外，請確定您使用&#x200B;*您的*&#x200B;驗證器。 例如，在測試期間，您可能會借用別人的`curl`命令，而忘記在驗證器中交換對方的命令。

* 檢查您的請求或清單中是否使用正確的傳輸通訊協定(`https://`與`https://`，或在FairPlay中，`skd://`與`https://`與`https://`。

* 請確定您已包含所使用DRM解決方案的所有必要查詢參數。 例如，PlayReady和Widevine之間很容易混淆，因為兩者都使用DASH，但所需的請求參數和封裝組態不同。
* 確認您的ExpressPlay帳戶有足夠的代號點數，且尚未用盡。
* 確認傳送至TVSDK的DRM資料三重體正確：ExpressPlay Token、授權伺服器URL和DRM類型。
* 確認您的所有元件都假定使用了與測試和生產兩種環境相同的ExpressPlay環境。
* 請注意，不同的瀏覽器通常只支援DASH內容的一個DRM。
* 自TVSDK 2.4起，僅支援DASH-LIVE封裝設定檔。 （DASH-OnDemand支援已列在規劃藍圖中。）
* 由於裝置製造商的限制，AndroidTV PlayReady支援不時出現。 為了提供範例，

   * razer Forge裝置在PlayReady內容上有問題
   * AmazonFireTV無法使用已加密音軌的DASH內容

* 自TVSDK 2.4起，只有AndroidTV裝置通常同時支援PlayReady和Widevine DRM。 所有其他Android裝置通常僅支援Widevine。
* 自TVSDK 2.4起，Android TVSDK目前要求PSSH方塊位於。mpd資訊清單中。 這與DASH標準相左，該標準指定PSSH方塊可以位於任何位置，例如內容本身，而不只是。mpd中。

