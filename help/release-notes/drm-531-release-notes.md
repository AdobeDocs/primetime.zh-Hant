---
title: DRM 5.3.1發行說明
seo-title: DRM 5.3.1發行說明
description: DRM 5.3.1發行說明介紹DRM 5.3.1中的新功能和已知問題。
seo-description: DRM 5.3.1發行說明介紹DRM 5.3.1中的新功能和已知問題。
uuid: bb61b79f-a5b3-42ed-8016-495b1ac99ea6
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# DRM 5.3.1發行說明 {#drm-release-notes}

DRM 5.3.1發行說明介紹DRM 5.3.1中的新功能和已知問題。

## 5.3版中的新功能 {#new-features}

* **安全停止** -您可以指定在播放窗口的末尾停止或繼續播放。
* **基於解析度的輸出保護(RBOP)** -您可以根據像素解析度指定輸出約束。
* **CDM門控** -為了支援HTML5,Adobe已更新Adobe Primetime DRM（舊稱Adobe Access DRM）Java SDK隨附的「參考實作」授權伺服器，以便能夠在單一URL端點使用所有DRM通訊協定訊息。 為了符合HTML5 EME（加密媒體擴展）規範，HTTP URL方法的這種整合是必要的，而CDM（內容解密模組）DRM供應商又需要該規範。 以前，這些是「參考實作」授權伺服器公開的唯一URL端點：

   * /flashaccess/i15n/v3（個人化）
   * /flashaccess/license/v5（授權要求）
   * /flashaccess/licenseRet/v5（授權退貨）
   * /flashaccess/getServerVersion/v5（Get Server版本）

現在，所有請求（源自HTML5 CDM）都可以導向至單一端點：/req

這項變更可向後相容於非CDM平台，例如Flash Player、Android、iOS。

* **RBOP縮減縮放** - RBOP針對HTML5空間包含自動縮放功能，其中，如果位元速率超過DRM原則中指定的允許位元速率，內容將縮放至允許的最大解析度。 例如，如果1080p流被流式傳輸到在非HDCP相容監視器上顯示內容的客戶端，DRM策略可能表示最大解析度應為720p。 Primetime DRM將解碼1080p串流，然後縮放至720p，再在螢幕上呈現。 如果播放視訊的瀏覽器接著拖曳至支援HDCP的螢幕，Primetime DRM會停止縮放內容，並於10時80分讓它播放。

## 5.3版中的已知問題 {#known-issues}

* `Hasher.bat (flashaccess-hasher.jar)` 將日誌消息輸 `flashaccess-global.log.`出到You must `flashaccess-global.log` ensurt the file is in the same directory with Hasher.bat.

* 有些呼叫的輸 `toJSON()`出會傳 `Strings` 回未完全符合JSON或完全符合的獨立方式（例如，未合成JSON結構）。

* Xbox金鑰伺服器接受版本值不等於1的金鑰要求。

Xbox金鑰伺服器僅支援版本等於1的金鑰要求，但目前伺服器接受版本不為1的金鑰要求。

* Xbox金鑰伺服器無法正確驗證原則。

Xbox金鑰伺服器不應接受有效日期以外的原則，但目前伺服器不受任何限制接受這些原則。

* Xbox金鑰伺服器應拒絕包含使用錯誤封裝憑證所建立之中繼資料的金鑰要求。
* 某些JSON結構的傳回值無法正確格式化，無法用於「解析度型輸出保護」相關類別。

數個類別會實作toJSON()方法，該方法應傳回該物件的JSON相容表示為「字串」，但目前傳回的值並不完全相容。

## 有用的資源 {#helpful-resources}

* 請參閱 [Adobe Primetime學習與支援頁面的完整說明檔案](https://helpx.adobe.com/support/primetime.html) 。
