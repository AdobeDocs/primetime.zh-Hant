---
title: 黃金時段離線打包器2.x版
description: 黃金時段離線打包器2.1和2.3.1版的新增功能
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: 911549b4-45b3-400a-b903-fa1479ee862b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# 黃金時段離線打包器版本 {#primetime-offline-packager-x-releases}

黃金時段離線打包器2.1和2.3.1版的新增功能

## 黃金時段離線打包器2.3.1（2016年10月）的新增功能  {#what-s-new-in-primetime-offline-packager-oct}

該版本為MPEG-DASH啟用按需配置檔案，為 `validate` 選項，並且對下面列出的多DRM方案沒有關鍵修復。

| **發行編號** | **說明** |
|---|---|
| PTPUB-985 | HLS AAXS和Sample-AES不適用於打包程式生成的密鑰 |
| PTPUB-973 | 某些特定Widevine內容加密算法中的固定錯誤 |
| PTPUB-964 | 某些播放器上某些媒體類型的CENC加密已中斷 — Android TVSDK。 |
| PTPUB-954 | 預設情況下，Sample-AES加密會繞過AAXS DRM/啟用遠程密鑰傳遞時引發的錯誤。 |
| PTPUB-951 | 當未使用Widevine指定key_file_path時，離線打包程式不會引發異常。 它拋棄了NPE。 |

黃金時段打包器的最新文檔可在以下網址獲得： [https://help.adobe.com/en_US/primetime/api/packagers/index.html](https://help.adobe.com/en_US/primetime/api/packagers/index.html)。

### 2.3.1版中的已知問題 {#known-issue-in-version}

此版本中存在以下問題。

| **發行編號** | **說明** |
|---|---|
| PTPUB-1005 | PlaylistCreator在為AAXS DRM生成的最終設定級別.mpd檔案中未提供.pssh檔案的正確URL。 |
| PTPUB-1001 | 當通過in_path參數提供空路徑時，PlaylistCreator應拋出錯誤 |
| PTPUB-990 | 對於DASH，當參數為VI時，離線打包器不會將生成的IV寫入磁碟 `log_vi` &amp; `iv_out_path` 。 |
| PTPUB-980 | 當配置檔案用於打包時，使用參數 `key_url` 不會從提供的輸入中刪除引號。 |

## Adobe Primetime離線打包器2.3.1 {#adobe-primetime-offline-packager}

### 最低系統要求 {#minimum-system-requirements}

支援的作業系統

* Linux CentOS 6.3 64位

硬體要求

* 3.2 GHz英特爾®奔騰® 4處理器（建議雙英特爾至強®或更快）

* 64位作業系統：4GB的RAM（建議8GB）

* 硬碟

（磁碟 — SAS）:7.5K RPM，最低10GB

（磁碟 — SSD）:400MBps讀/寫速度

(NAS):1 GB專用鏈路

軟體要求

* OracleJava SE 1.8或更高版本

### Adobe Primetime離線打包器2.3.1 {#adobe-primetime-offline-packager-1}

1. 從 [Oracle站點](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 並按照安裝說明進行操作。
1. 解壓名為的Adobe Primetime離線包2.3.1存檔檔案 `PrimetimeOfflinePackager-2-3-1-b47-10142016.zip` 到磁碟。

### 配置離線打包程式2.3.1 {#configuring-the-offline-packager}

有關配置說明，請參閱《Mogine Offline Packager入門指南》，網址為 [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## 黃金時段線下打包器2.1（2015年7月）的新增內容 {#what-s-new-in-primetime-offline-packager-july}

支援PlayReady BuyDRM（用於DASH）。 有關詳細資訊，請參閱幫助文檔 [此處](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)。

還對離線打包器進行了以下增強。

PTPUB-780添加了對EXT-X-START標籤的支援

## 黃金時段線下打包器2.0（2015年6月）的新增內容 {#what-s-new-in-primetime-offline-packager-june}

已添加明確的DASH輸出支援。 請參閱產品文檔 [這裡](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html) 的雙曲餘切值。

本版本中還解決了以下問題。

* PTPUB-783離線打包程式現在可以處理空的WebVTT檔案。
* PTPUB- 781當某些經過轉碼的MP4資產與離線打包器打包以生成MBR輸出時，Chrome上的HLS輸出中的偽物。

## Adobe Primetime離線打包器2.1 {#adobe-primetime-offline-packager-2}

### 最低系統要求 {#minimum-system-requirements-1}

**支援的作業系統**

* Linux CentOS 6.3 64位

**硬體要求**

* 3.2 GHz英特爾®奔騰® 4處理器（建議雙英特爾至強®或更快）

* 64位作業系統：4GB的RAM（建議8GB）

* 建議使用1 Gb乙太網卡（還支援多個網卡和10 Gb）

* 硬碟

   * （磁碟 — SAS）:7.5K RPM，最低10GB
   * （磁碟 — SSD）:400MBps讀/寫速度
   * (NAS):1 GB專用鏈路

**軟體要求**

* OracleJava SE 1.8或更高版本

### 安裝離線打包程式2.1 {#installing-offline-packager}

1. 從 [Oracle站點](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 並按照安裝說明進行操作。
1. 提取 `Adobe Primetime - Offline Packager 2.1.0 archive file, PrimetimeOfflinePackager-2-1-0-b15-07082015.zip`，到光碟。

### 配置離線打包程式2.1 {#configuring-the-offline-packager-1}

有關此處提供的配置詳細資訊，請參閱黃金時段離線打包程式入門文檔 [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## 有用的資源 {#helpful-resources}

* 請參閱以下網址的完整幫助文檔 [Adobe Primetime學習和支援](https://helpx.adobe.com/support/primetime.html) 的子菜單。
