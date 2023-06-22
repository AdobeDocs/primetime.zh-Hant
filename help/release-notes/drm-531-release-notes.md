---
title: DRM 5.3.1發行說明
description: DRM 5.3.1發行說明說明DRM 5.3.1的新功能和已知問題。
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: e4e0a933-cfc6-4713-ae13-5df11cfc1aad
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# DRM 5.3.1發行說明 {#drm-release-notes}

DRM 5.3.1發行說明說明DRM 5.3.1的新功能和已知問題。

## 5.3版中的新功能 {#new-features}

* **安全停止 —** 您可以指定在播放視窗結束時是否停止或繼續播放。
* **以解析度為基礎的輸出保護(RBOP) -** 您可以根據畫素解析度來指定輸出限制。
* **CDM閘道 —** 為了支援HTML5，Adobe更新了Adobe Primetime DRM (原稱Adobe Access DRM) Java SDK隨附的參考實作授權伺服器，以便能夠在單一URL端點使用所有DRM通訊協定訊息。 為了遵循CDM （內容解密模組） DRM廠商實作的HTML5 EME （加密媒體擴充功能）規格，必須合併HTTP URL方法。 之前，這些是Reference Implementation授權伺服器公開的唯一一個URL端點：

   * /flashaccess/i15n/v3 （個人化）
   * /flashaccess/license/v5 （授權要求）
   * /flashaccess/licenseRet/v5 （授權退回）
   * /flashaccess/getServerVersion/v5 （取得伺服器版本）

現在，所有請求(源自HTML5 CDM)都可以被導向到單一端點：/req

此變更可回溯相容於非CDM平台，例如Flash Player、Android、iOS。

* **RBOP縮減比例 —** 特定於HTML5空間，RBOP包含自動縮減縮放功能，其中如果位元速率超過DRM原則中指定的允許位元速率，內容將會縮減到允許的最大解析度。 例如，如果將1080p資料流傳輸至在非HDCP相容監視器上顯示內容的使用者端，DRM原則可能會指出最大解析度應為720p。 Primetime DRM會解碼1080p資料流，然後在熒幕上呈現之前將其縮小至720p。 如果播放視訊的瀏覽器接著被拖曳到支援HDCP的監視器上，Primetime DRM就會停止縮減內容縮放並允許1080重播。

## 5.3版中的已知問題 {#known-issues}

* `Hasher.bat (flashaccess-hasher.jar)` 將記錄訊息輸出至 `flashaccess-global.log.`您必須確保 `flashaccess-global.log` 檔案與Hasher.bat位於相同目錄中。

* 部分「 」的 `toJSON()`呼叫傳回 `Strings` 非完全符合JSON規範或以獨立方式完全符合（即沒有JSON結構組成）的檔案。

* Xbox金鑰伺服器接受版本值不等於1的金鑰要求。

Xbox金鑰伺服器應僅支援版本等於1的關鍵要求，但目前，伺服器接受版本不是1的關鍵要求。

* Xbox金鑰伺服器無法正確驗證原則。

Xbox金鑰伺服器不應該接受超過有效日期的原則，但是目前，伺服器無論如何都會接受這些原則。

* Xbox金鑰伺服器應拒絕金鑰要求，該金鑰要求包含使用錯誤的封裝程式憑證建立的中繼資料。
* 部分JSON結構的傳回值格式不正確，無法用於以解析度為基礎的輸出保護相關類別。

有幾個類別實作toJSON()方法，該方法應該會將該物件的JSON相容表示傳回為String，但目前傳回的值不完全符合JSON。

## 實用資源 {#helpful-resources}

* 如需完整說明檔案，請前往 [Adobe Primetime學習與支援](https://helpx.adobe.com/support/primetime.html) 頁面。
