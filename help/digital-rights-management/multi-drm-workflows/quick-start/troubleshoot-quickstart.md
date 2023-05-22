---
description: 測試過程中的常見問題通常涉及您的ExpressPlay身份驗證器、傳輸協定和所需的服務請求參數。
title: 快速啟動故障排除
exl-id: d8908f9c-98f4-4100-a003-d3b990105dee
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# 快速啟動故障排除{#troubleshooting-your-quick-start}

測試過程中的常見問題通常涉及您的ExpressPlay身份驗證器、傳輸協定和所需的服務請求參數。

如果 [!DNL curl] 請求ExpressPlay生成令牌失敗，響應正文將包含一條錯誤消息，說明失敗的原因。

如果令牌生成成功，但內容仍不播放，請檢查ExpressPlay令牌兌現日誌中是否有「過期令牌」等錯誤。

如果令牌生成成功且兌現沒有錯誤，但視頻仍未播放，請檢查CEK是否與內容匹配，以及內容格式是否與目標設備的功能匹配。

此外：

* 檢查您在服務請求中是否使用了正確的客戶驗證器。 當您想要使用test驗證器時，很容易意外地使用生產驗證器。 另外，確保您正在使用 *你* 驗證器。 例如，在測試期間，你可能會借別人的 `curl` 命令，忘記替鑑定器換。

* 檢查您的請求或清單中是否使用了正確的傳輸協定( `https://` 與 `https://`或者在FairPlay的例子中， `skd://` 與 `https://` 與 `https://`。

* 確保包含所使用的DRM解決方案的所有所需查詢參數。 例如，很容易混淆PlayReady和Widevine，因為它們都使用DASH，但所需的請求參數和打包配置不同。
* 確認您的ExpressPlay帳戶具有足夠的令牌信用額且尚未用完。
* 確認要發送到TVSDK的DRM資料的三份正確：ExpressPlay令牌、許可證伺服器URL和DRM類型。
* 確認您的所有元件都對使用的ExpressPlay環境做了相同的假設，因為有兩個環境：Test和生產。
* 請注意，不同的瀏覽器通常只支援DRM內容。
* 從TVSDK 2.4開始，僅支援DASH-LIVE打包配置檔案。 （DASH-OnDemand支援在路線圖中。）
* 由於設備製造商的限制，AndroidTV PlayReady支援間歇性。 為了舉例，

   * Razer Forge設備與PlayReady內容有問題
   * AmazonFireTV無法使用已加密音頻軌道的DASH內容

* 從TVSDK 2.4開始，只有AndroidTV設備通常同時支援PlayReady和Widevine DRM。 所有其他Android設備通常只支援Widevine。
* 從TVSDK 2.4開始，Android TVSDK當前要求PSSH框位於.mpd清單中。 這與DASH標準相反，後者指定PSSH框可以位於任何位置，如內容本身，而不僅是.mpd。
