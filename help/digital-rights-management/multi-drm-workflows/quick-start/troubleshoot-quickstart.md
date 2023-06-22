---
description: 測試中的常見問題通常與您的ExpressPlay驗證者、傳輸通訊協定和必要的服務要求引數有關。
title: 疑難排解您的快速入門
exl-id: d8908f9c-98f4-4100-a003-d3b990105dee
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# 疑難排解您的快速入門{#troubleshooting-your-quick-start}

測試中的常見問題通常與您的ExpressPlay驗證者、傳輸通訊協定和必要的服務要求引數有關。

若您的 [!DNL curl] 對ExpressPlay產生Token的請求失敗，回應內文將包含說明失敗原因的錯誤訊息。

如果權杖產生成功，但內容仍然沒有播放，請檢查ExpressPlay權杖贖回記錄檔中是否有錯誤，例如「已到期的權杖」。

如果代號產生成功，而且贖回沒有錯誤，但視訊仍然沒有播放，請檢查CEK是否符合內容，以及內容格式是否符合目標裝置的功能。

此外：

* 檢查您是否在服務請求中使用正確的客戶驗證器。 當您想要使用測試驗證器時，很容易意外使用生產驗證器。 此外，請務必使用 *您的* 驗證者。 例如，在測試期間，您可能會借用他人的 `curl` 命令，而忘記在驗證器中交換他們的內容。

* 檢查您在請求或資訊清單中是否使用正確的傳輸通訊協定( `https://` 與 `https://`、或是在FairPlay的案例中， `skd://` 與 `https://` 與 `https://`.

* 請確定您已包含您所使用DRM解決方案的所有必要查詢引數。 例如，PlayReady和Widevine很容易混淆，因為它們都使用DASH，但所需的請求引數和封裝設定不同。
* 確認您的ExpressPlay帳戶有足夠的代號積分，而且尚未用完。
* 確認傳送至TVSDK的三重DRM資料正確：ExpressPlay權杖、授權伺服器URL及DRM型別。
* 確認您所有的元件對於使用哪個ExpressPlay環境的假設與有兩個環境（測試和生產）的假設相同。
* 請注意，不同的瀏覽器通常只支援一個DRM作為DASH內容。
* 自TVSDK 2.4起，僅支援DASH-LIVE封裝設定檔。 （DASH-OnDemand支援正在規劃中。）
* 由於裝置製造商的限制，AndroidTV PlayReady支援會斷斷續續。 舉例來說，

   * Razer Forge裝置的PlayReady內容有問題
   * Amazon FireTV無法使用已加密音訊曲目的破折號內容

* 自TVSDK 2.4起，只有AndroidTV裝置通常同時支援PlayReady和Widevine DRM。 其他所有Android裝置通常僅支援Widevine。
* 截至TVSDK 2.4，Android TVSDK目前要求PSSH方塊位於.mpd資訊清單中。 這與DASH標準相反，後者規定PSSH方塊可位於任何位置，例如內容本身，而不僅僅是.mpd。
