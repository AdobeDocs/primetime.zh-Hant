---
title: DRM 5.3.1發行說明
description: 《DRM 5.3.1發行說明》介紹了DRM中的新功能和已知問5.3.1。
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

《DRM 5.3.1發行說明》介紹了DRM中的新功能和已知問5.3.1。

## 5.3版中的新功能 {#new-features}

* **安全停止 —** 可以指定回放是在回放窗口結束時停止還是繼續。
* **基於解析度的輸出保護(RBOP)-** 可以根據像素解析度指定輸出約束。
* **CDM門控 —** 為了支援HTML5,Adobe已經更新了Adobe PrimetimeDRM(以前稱為Adobe訪問DRM)Java SDK附帶的參考實現許可伺服器，以便能夠在單個URL端點處使用所有DRM協定消息。 為了符合CDM（內容解密模組）DRM供應商需要實現的HTML5 EME（加密媒體擴展）規範，HTTP URL方法的這種合併是必要的。 以前，這些是引用實施許可證伺服器公開的唯一URL終結點：

   * /flashaccess/i15n/v3（個性化）
   * /flashaccess/license/v5（許可證請求）
   * /flashaccess/licenseRet/v5（許可證返回）
   * /flashaccess/getServerVersion/v5（獲取伺服器版本）

現在，所有請求(源於HTML5 CDM)都可以定向到單個端點：/req

這種變化與Flash Player、安卓、iOS等非CDM平台向後相容。

* **RBOP縮放 —** 對於HTML5空間，RBOP包含自動縮放功能，其中，如果比特率超過DRM策略中指定的允許比特率，則內容將縮放到最大允許解析度。 例如，如果1080p流被流式傳輸到在非HDCP相容監視器上顯示內容的客戶端，則DRM策略可指示最大解析度應為720p。 黃金時段DRM將解碼1080p流，然後縮放到720p，然後再在螢幕上呈現。 如果播放視頻的瀏覽器隨後被拖到支援HDCP的監視器，則黃金時段DRM將停止縮放內容，並允許其在10時80回放。

## 5.3版中的已知問題 {#known-issues}

* `Hasher.bat (flashaccess-hasher.jar)` 將日誌消息輸出到 `flashaccess-global.log.`您必須確保 `flashaccess-global.log` 檔案與Hasher.bat位於同一目錄中。

* 某些 `toJSON()`呼叫回復 `Strings` 不完全符合JSON或完全符合（即不合成JSON結構）。

* Xbox密鑰伺服器接受版本值不等於1的密鑰請求。

Xbox密鑰伺服器只應支援版本等於1的密鑰請求，但當前，伺服器接受版本不為1的密鑰請求。

* Xbox密鑰伺服器無法正確驗證策略。

Xbox密鑰伺服器不應接受有效日期之外的策略，但目前伺服器無論如何都接受這些策略。

* Xbox密鑰伺服器應拒絕包含使用錯誤打包證書建立的元資料的密鑰請求。
* 某些JSON結構的返回值的格式不正確，無法用於與基於解析度的輸出保護相關的類。

若干類實現toJSON()方法，該方法應將該對象的JSON相容表示形式返回為String，但當前返回的值不完全符合JSON。

## 有用的資源 {#helpful-resources}

* 請參閱以下網址的完整幫助文檔 [Adobe Primetime學習和支援](https://helpx.adobe.com/support/primetime.html) 的子菜單。
