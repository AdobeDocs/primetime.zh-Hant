---
title: Primetime Offline Packager 2.x版
description: Primetime Offline Packager 2.1和2.3.1版的新增功能
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: 911549b4-45b3-400a-b903-fa1479ee862b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# Primetime Offline Packager版本 {#primetime-offline-packager-x-releases}

Primetime Offline Packager 2.1和2.3.1版的新增功能

## Primetime Offline Packager 2.3.1的新增功能（2016年10月）  {#what-s-new-in-primetime-offline-packager-oct}

此發行版本啟用MPEG-DASH的隨選設定檔，新增對 `validate` 選項適用於PlaylistCreator工具，並且針對下列多DRM案例有幾項關鍵修正。

| **問題編號** | **說明** |
|---|---|
| PTPUB-985 | HLS AAXS和Sample-AES不適用於封裝程式產生的金鑰 |
| PTPUB-973 | 修正某些特定Widevine內容的加密演演算法錯誤 |
| PTPUB-964 | 某些播放器上特定媒體型別的CENC加密中斷 — Android TVSDK。 |
| PTPUB-954 | 範例AES加密預設會略過AAXS DRM /在啟用遠端金鑰傳遞時擲回錯誤。 |
| PTPUB-951 | 未使用Widevine指定key_file_path時，Offline Packager不會擲回例外狀況。 而是會擲回NPE。 |

Primetime封裝程式的最新檔案可在以下網址取得： [https://help.adobe.com/en_US/primetime/api/packagers/index.html](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

### 2.3.1版中的已知問題 {#known-issue-in-version}

此版本中存在下列問題。

| **問題編號** | **說明** |
|---|---|
| PTPUB-1005 | PlaylistCreator沒有為針對AAXS DRM產生的最終設定層級.mpd檔案中的.pssh檔案提供正確的URL。 |
| PTPUB-1001 | 透過in_path引數提供空白路徑時，PlaylistCreator應擲回錯誤 |
| PTPUB-990 | 對於DASH，當引數為時，Offline Packager不會將封裝程式產生的IV寫入磁碟 `log_vi` 和 `iv_out_path` 已指定。 |
| PTPUB-980 | 使用組態檔進行封裝時，請使用引數 `key_url` 不會從提供的輸入中移除引號。 |

## Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager}

### 最低系統需求 {#minimum-system-requirements}

支援的作業系統

* Linux CentOS 6.3 64位元

硬體需求

* 3.2GHz Intel® Pentium® 4處理器(建議使用雙Intel Xeon®或更快處理器)

* 64位元作業系統：4GB的RAM （建議使用8GB）

* 硬碟

（磁碟 — SAS）：最少10GB (7,500RPM)

（磁碟 — SSD）：400MBps讀取/寫入速度

(NAS)：1 GB專用連結

軟體需求

* oracleJava SE 1.8或更高版本

### Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager-1}

1. 從下載Java SE軟體 [oracle網站](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 並依照安裝指示操作。
1. 解壓縮Adobe Primetime Offline Packager 2.3.1封存檔案（已命名） `PrimetimeOfflinePackager-2-3-1-b47-10142016.zip` 到磁碟。

### 設定Offline Packager 2.3.1 {#configuring-the-offline-packager}

您可以在Primetime Offline Packager快速入門手冊中找到設定指示 [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Primetime Offline Packager 2.1的新增功能（2015年7月） {#what-s-new-in-primetime-offline-packager-july}

支援PlayReady BuyDRM (DASH)。 如需詳細資訊，請參閱說明檔案 [此處提供](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

對離線封裝程式也進行了下列增強功能。

PTPUB-780新增對EXT-X-START標籤的支援

## Primetime Offline Packager 2.0 （2015年6月）的新增功能 {#what-s-new-in-primetime-offline-packager-june}

新增了「清除DASH輸出」支援。 請參閱產品檔案 [此處](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html) 以取得詳細資訊。

此版本也修正了下列問題。

* PTPUB-783 Offline Packager現在可以處理空的WebVTT檔案。
* PTPUB- Chrome上HLS輸出中的781成品（當某些轉碼的MP4資產與離線封裝程式封裝在一起以產生MBR輸出時）。

## Adobe Primetime Offline Packager 2.1 {#adobe-primetime-offline-packager-2}

### 最低系統需求 {#minimum-system-requirements-1}

**支援的作業系統**

* Linux CentOS 6.3 64位元

**硬體需求**

* 3.2GHz Intel® Pentium® 4處理器(建議使用雙Intel Xeon®或更快處理器)

* 64位元作業系統：4GB的RAM （建議使用8GB）

* 建議使用1Gb乙太網路卡（也支援多張網路卡和10Gb）

* 硬碟

   * （磁碟 — SAS）：最少10GB (7,500RPM)
   * （磁碟 — SSD）：400MBps讀取/寫入速度
   * (NAS)：1 GB專用連結

**軟體需求**

* oracleJava SE 1.8或更高版本

### 安裝離線封裝程式2.1 {#installing-offline-packager}

1. 從下載Java SE軟體 [oracle網站](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 並依照安裝指示操作。
1. 擷取 `Adobe Primetime - Offline Packager 2.1.0 archive file, PrimetimeOfflinePackager-2-1-0-b15-07082015.zip`，移至您的磁碟。

### 設定離線封裝程式2.1 {#configuring-the-offline-packager-1}

如需此處可用的設定詳細資訊，請參閱Primetime Offline Packager快速入門檔案 [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## 實用資源 {#helpful-resources}

* 如需完整說明檔案，請前往 [Adobe Primetime學習與支援](https://helpx.adobe.com/support/primetime.html) 頁面。
