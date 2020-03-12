---
title: Primetime Offline Packager 2.x版本
seo-title: Primetime Offline Packager 2.x版本
description: Primetime Offline Packager 2.1和2.3.1版本的新增功能
seo-description: Primetime Offline Packager 2.1和2.3.1版本的新增功能
uuid: 01926a10-890d-477d-b832-e22847d957e0
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: 933a0711-846a-4bb7-bf51-b300822a93d4
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# Primetime Offline Packager版本 {#primetime-offline-packager-x-releases}

Primetime Offline Packager 2.1和2.3.1版本的新增功能

## Primetime Offline Packager 2.3.1的新增功能（2016年10月） {#what-s-new-in-primetime-offline-packager-oct}

此發行可啟用MPEG-DASH的隨選設定檔、新增對PlaylistCreator工具選項的支援，而下列的多DRM藍本的重要修正則很少。 `validate`

| **期刊編號** | **說明** |
|---|---|
| PTPUB-985 | HLS AAXS和Sample-AES不適用於封裝工具產生的金鑰 |
| PTPUB-973 | 修正某些特定Widevine內容的加密算法錯誤 |
| PTPUB-964 | CENC加密已針對特定播放器上的特定媒體類型中斷- Android TVSDK。 |
| PTPUB-954 | Sample-AES加密預設會略過AAXS DRM / Error thrown with remote key delivery enabled. |
| PTPUB-951 | 當未在Widevine中指定key_file_path時，離線套件不會拋出異常。 而是拋出NPE。 |

Primetime Packagers的最新檔案可在https://help.adobe.com/en_US/primetime/api/packagers/index.html上 [找到](https://help.adobe.com/en_US/primetime/api/packagers/index.html)。

### 2.3.1版中的已知問題 {#known-issue-in-version}

此發行中存在下列問題。

| **期刊編號** | **說明** |
|---|---|
| PTPUB-1005 | PlaylistCreator未在為AAXS DRM產生的最終設定層級。mpd檔案中，為。pssh檔案提供正確的URL。 |
| PTPUB-1001 | 透過in_path參數提供空路徑時，PlaylistCreator應擲回錯誤 |
| PTPUB-990 | 對於DASH，指定參數和時，Offline Packager不會將生成的IV寫入 `log_vi` 磁 `iv_out_path` 盤中。 |
| PTPUB-980 | 當使用配置檔案進行封裝時，使用參 `key_url` 數不會從提供的輸入中刪除引號。 |

## Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager}

### 最低系統需求 {#minimum-system-requirements}

支援的作業系統

* Linux CentOS 6.3 64位元

硬體需求

* 3.2GHz Intel® Pentium® 4處理器（建議使用雙Intel Xeon®或速度更快的處理器）

* 64位元作業系統：4GB的記憶體（建議使用8GB）

* 硬碟

（磁碟-SAS）:7.5K RPM，最低10GB

（磁碟——固態硬碟）:400MBps的讀／寫速度

(NAS):1 GB專用鏈路

軟體需求

* Oracle Java SE 1.8或更高版本

### Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager-1}

1. 從 [Oracle站點下載Java SE軟體](https://www.oracle.com/technetwork/java/javase/downloads/index.html) ，然後按照安裝說明操作。
1. 將名為的Adobe Primetime Offline Packager 2.3.1封存檔解壓縮 `PrimetimeOfflinePackager-2-3-1-b47-10142016.zip` 至磁碟。

### 設定Offline Packager 2.3.1 {#configuring-the-offline-packager}

如需設定指示，請參閱Primetime Offline Packager快速入門手冊，網址為 [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Primetime Offline Packager 2.1的新增功能（2015年7月） {#what-s-new-in-primetime-offline-packager-july}

支援PlayReady BuyDRM（適用於DASH）。 如需詳細資訊，請參閱此處提供的 [說明檔案](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)。

對離線封裝程式也進行了下列增強功能。

PTPUB-780新增對EXT-X-START標籤的支援

## Primetime Offline Packager 2.0的新增功能（2015年6月） {#what-s-new-in-primetime-offline-packager-june}

已新增明確的DASH輸出支援。 如需詳細資訊，請參 [閱此處](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html) 的產品檔案。

此版本中也修正了下列問題。

* PTPUB-783 Offline Packager現在可處理空的WebVTT檔案。
* PTPUB —— 當某些經過轉碼的MP4資產與離線封裝器封裝以產生MBR輸出時，Chrome上的HLS輸出中的781偽影。

## Adobe Primetime Offline Packager 2.1 {#adobe-primetime-offline-packager-2}

### 最低系統需求 {#minimum-system-requirements-1}

**支援的作業系統**

* Linux CentOS 6.3 64位元

**硬體需求**

* 3.2GHz Intel® Pentium® 4處理器（建議使用雙Intel Xeon®或速度更快的處理器）

* 64位元作業系統：4GB的記憶體（建議使用8GB）

* 建議使用1Gb乙太網卡（也支援多張網路卡和10Gb）

* 硬碟

   * （磁碟-SAS）:7.5K RPM，最低10GB
   * （磁碟——固態硬碟）:400MBps的讀／寫速度
   * (NAS):1 GB專用鏈路

**軟體需求**

* Oracle Java SE 1.8或更高版本

### 安裝Offline Packager 2.1 {#installing-offline-packager}

1. 從 [Oracle站點下載Java SE軟體](https://www.oracle.com/technetwork/java/javase/downloads/index.html) ，然後按照安裝說明操作。
1. 將光 `Adobe Primetime - Offline Packager 2.1.0 archive file, PrimetimeOfflinePackager-2-1-0-b15-07082015.zip`盤解壓。

### 設定Offline Packager 2.1 {#configuring-the-offline-packager-1}

請參閱Primetime Offline Packager快速入門檔案，以取得此處https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html的設定詳細資 [訊](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## 有用的資源 {#helpful-resources}

* 請參閱 [Adobe Primetime學習與支援頁面的完整說明檔案](https://helpx.adobe.com/support/primetime.html) 。