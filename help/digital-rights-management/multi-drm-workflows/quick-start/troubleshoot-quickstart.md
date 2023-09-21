---
description: 測試中的常見問題通常與您的ExpressPlay驗證者、傳輸通訊協定及必要的服務要求引數有關。
title: 疑難排解您的快速入門
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# 疑難排解您的快速入門{#troubleshooting-your-quick-start}

測試中的常見問題通常與您的ExpressPlay驗證者、傳輸通訊協定及必要的服務要求引數有關。

若您的 [!DNL curl] 對ExpressPlay產生Token的請求失敗，回應本文會包含錯誤訊息，說明失敗的原因。

如果權杖產生成功，但內容仍然沒有播放，請檢查ExpressPlay權杖贖回記錄檔是否有錯誤，例如「已到期的權杖」。

如果代號產生成功且兌換沒有錯誤，但視訊仍然沒有播放，請檢查CEK是否符合內容，以及內容格式是否符合目標裝置的功能。

此外：

* 檢查您是否在服務請求中使用正確的客戶驗證器。 使用測試驗證器時，很容易意外使用生產驗證器。 此外，請務必使用 *您的* 驗證者。 例如，在測試期間，您可能會借用他人的 `curl` 命令並忘記在驗證器中交換他們的驗證器。

* 檢查您在請求或資訊清單中是否使用正確的傳輸通訊協定( `https://` 與 `https://`、或在FairPlay的情況下， `skd://` 與 `https://` 與 `https://`.

* 請確定您包含正在使用的DRM解決方案的所有必要查詢引數。 例如，PlayReady和Widevine很容易混淆，因為它們都使用DASH，但所需的要求引數和封裝組態不同。
* 確認您的ExpressPlay帳戶有足夠的權杖積分，而且尚未用完。
* 確認傳送至TVSDK的三重DRM資料是否正確： ExpressPlay權杖、授權伺服器URL以及DRM型別。
* 確認您所有的元件對於使用中的ExpressPlay環境有相同的假設，因為有兩個環境：測試和生產。
* 請注意，不同的瀏覽器通常只支援一個DASH內容的DRM。
* 自TVSDK 2.4起，僅支援DASH-LIVE封裝設定檔。 （DASH-OnDemand支援正在規劃中。）
* 由於裝置製造商的限制，AndroidTV PlayReady支援會斷斷續續。 舉例來說，

   * Razer Forge裝置的PlayReady內容有問題
   * Amazon FireTV無法使用已加密音訊曲目的DASH內容

* 截至TVSDK 2.4，只有AndroidTV裝置通常同時支援PlayReady和Widevine DRM。 其他所有Android裝置通常僅支援Widevine。
* 截至TVSDK 2.4，Android TVSDK目前要求PSSH方塊位於.mpd資訊清單中。 這與DASH標準相悖，後者規定PSSH方塊可位於任何位置，例如內容本身，而不只是.mpd。
