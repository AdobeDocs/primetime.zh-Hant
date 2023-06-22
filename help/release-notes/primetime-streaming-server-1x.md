---
title: Primetime串流伺服器發行版本
description: Primetime Streaming Server 1.3和1.4版的新增功能。
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: 80c4687e-b0ac-48f2-a1c3-8751552da9d1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---

# Primetime串流伺服器發行版本 {#primetime-streaming-server-x-releases}

Primetime Streaming Server 1.3和1.4版的新增功能。

## Primetime Streaming Server 1.4的新增功能（12月發行） {#what-s-new-in-primetime-streaming-server-december-release}

**離線封裝程式**

* 輸出HLS資料流現在包含MPEG-2 TS中顯示的ID3中繼資料
* 僅限HLS音訊的串流現在可以有關聯的靜態影像
* 支援提供IV作為HLS AES加密工作流程的使用者輸入
* 當離線封裝程式產生IV時，支援將IV輸出至檔案
* 播放清單建立器現在支援將多語言音訊群組和多語言WebVTT字幕群組與媒體串流建立關聯

**原始伺服器**

* HLS AES加密可用於Live和VOD工作流程。 Primetime Origin可以及時將HLS AES加密套用至傳入的HLS資料流或MP4檔案。
* 當它用來將傳入的HDS資料流轉換為HLS資料流時，也可以套用JIT HLS AES加密。
* Primetime Origin現在支援SWF允許列出PHLS資料流。 之前僅支援PHDS串流

**Primetime Live Packager**

* 支援為輸入RTMP和MPEG-2 TS資料流產生HLS AES-128資料流

PHDS/PHLS憑證已更新。 新的到期日將為2016年10月1日。

### **版本1.4中包括的錯誤修正** {#bug-fixes-included-in-release}

* PTPUB-282- OfflinePackager 1.3.1建立的HLS設定層級資訊清單沒有轉碼器和解析度資訊。
* PTPUB-353 - PlayListCreator不支援在設定層級資訊清單中新增WebVTT資訊
* PTPUB-583 - PlaylistCreator工具意外地在群組URI的前面加上。
* PTPUB-605播放清單產生器未在每個變體資料流中列出SUBTITLE群組
* PTPUB-634 -Offline Packager將SpliceInsert新增至資訊清單。
* PTPUB-635 — 插入多個SpliceOut標籤以取得單一廣告提示。

### 版本1.4中的已知問題 {#known-issue-in-release}

* PTPUB- 645 DPISimple Mode即使在離線封裝程式設定中同時提供命令列提示和串流提示時，指定DPIScte35模式時也會強制執行

## Primetime Streaming Server 1.3.1的新增功能（5月版本） {#what-s-new-in-primetime-streaming-server-may-release}

1.3.1版是指Hotfix。 下列增強功能使其成為客戶的建議升級，包含JIT MP4使用案例的關鍵效能增強功能：

1. 透過DRM在原點上產生MP4 JIT m3u8的效能修正，包括金鑰輪換
1. 新增設定「CopyQueryParamToJITFragmentURIs」，以將查詢引數從JIT資訊清單請求複製到產生的片段URI以進行MP4 JIT轉換。 如需使用範例，請參閱HTTP原始伺服器檔案
1. 透過新增至vod.xml的Config/MP4Only設定，允許無副檔名的MP4檔案進行JIT轉換

### 版本1.3.1中包含的錯誤修正 {#bug-fixes-included-in-release-1}

* 3759167 — 並非所有SCTE35提示都會因為封裝時的時間戳記異常而出現在輸出資訊清單中。 對SCTE35訊息中SpliceInfoSection的TimeSignal中的SpliceTime套用pts_adjustment。

### 版本1.3.1中的已知問題 {#known-issues-in-release}

* 3717039 — 當封裝程式設定為產生DPI簡單模式提示時，它實際上應該尋找特定的訊號型別，例如插接插入或放置機會，並且只將這些轉換成簡單模式提示。 它應該忽略其他型別的訊號，例如程式啟動、網路啟動等。

* 3718598 — 當原始伺服器設定為在啟用HSM存取的情況下提供受保護的內容時，後端LunaSA使用者端會經常與HSM模組通訊

## Primetime Streaming Server 1.3的新增功能（4月版本） {#what-s-new-in-primetime-streaming-server-april-release}

Primetime 1.3版提供數項串流內容的新功能，以及更出色的可用性與安全性。

**Primetime Streaming Server為Live Packager和Origin Server的統一形式**

Primetime Live Packager和Primetime Origin會一起作為單一元件運作。 此元件可用作封裝器或作為來源，或使用合併的功能來封裝和託管即時資料流。

這可提供這些伺服器的統一檔案介面，讓它們在單一電腦上輕鬆執行。 它繼續提供彈性以設定為個別封裝程式或來源。

**Beta MPEG — 短劃線支援**

Primetime串流伺服器支援MPEG-DASH封裝以供即時和VOD工作流程使用。 Live Packager元件會將內嵌RTMP或MPEG-2-TS資料流轉換為虛線格式。 原始元件接受DASH資料流。

對於VOD工作流程， Offline Packager元件會將MP4和TS資產轉換為MPEG — 破折號ISOBFF格式。

**即時到VOD轉換**

現在有新的元件錄製伺服器可用，可支援擷取即時資料流並封存以供VOD播放。 它支援建立完整事件重播，以及部分事件的剪輯/醒目提示。 您可以將其設定為錄製純音訊串流、移除廣告或即時內容中的標籤。 Recording Server可與Primetime Streaming Server及協力廠商原始檔搭配使用。

**Primetime Live Packager中的RTMP至HLS轉換**

Primetime Live Packager元件支援從RTMP資料流建立HLS資料流。 它也可以將Primetime DRM和Protected Streaming新增至輸出HLS資料流。

**對Primetime Live Packager的傳入RTMP資料流的驗證**

usermgmt.jar現在隨Primetime Live Packager提供，可在傳送RTMP資料流至Primetime Live Packager時，使用信任的認證來設定存取權

現在，編碼器可設定為在傳送資料流至Live Packager時使用使用者名稱/密碼。

**PlaylistCreator工具可建立HDS和HLS的頂層資訊清單**

Primetime Offline Packager現在提供聰明的公用程式PlaylistCreator.jar，可輕鬆建立HDS和HLS資產的頂層資訊清單檔案。

**整合硬體安全性模組的額外安全性功能**

Primetime Offline Packager現在支援從Hardware Security Module存取Packager認證憑證和通用金鑰。

Hardware Security模組為這些機密資產提供額外的保護。

**改善VOD封裝的效能**

已納入數個效能增強功能，以改善Primetime Offline Packager中Mezzanine資產的封裝時間

**改善JIT MP4封裝的效能**

Primetime Origin的JIT封裝功能已納入數個效能增強功能，以處理使用者對大型VOD資產資料庫的請求。

## Adobe Primetime Streaming Server 1.4 {#adobe-primetime-streaming-server}

### 最低系統需求 {#minimum-system-requirements}

**網路需求**

* 網路應啟用多點傳送，以便從編碼器傳送MPEG-TS資料流至Live Packager。 Live Packager也接受來自不需要多點傳送網路之編碼器的RTMP資料流。

**支援的作業系統**

* Linux CentOS 6.3 64位元

**硬體需求**

* 3.2GHz Intel® Pentium® 4處理器(建議使用雙Intel Xeon®或更快處理器)
* 64位元作業系統：4GB的RAM （建議使用8GB）
* 建議使用1Gb乙太網路卡（也支援多張網路卡和10Gb）
* 磁碟：

   * （磁碟 — SAS）：最少10GB (7,500RPM)
   * （磁碟 — SSD）：400MBps讀取/寫入
   * (NAS) ：1 GB專用連結

**軟體需求**

* oracleJava JRE 1.7 (建議： Sun/Oracle熱點JVM)。 Jconsole存取JMX API需要JDK

### 安裝及設定Primetime串流伺服器 {#install-and-configure-primetime-streaming-server}

**安裝串流伺服器**

1. 從下載Java SE和JDK軟體 [oracle網站](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 並依照安裝指示操作。
2. 解壓縮Adobe Primetime-Streaming Server 1.4封存檔案， `Primetime- StreamingServer-1-4-0-b206-12042014.zip` 至您的磁碟。

**啟動Primetime串流伺服器**

若要啟動串流伺服器，請從串流伺服器的根目錄中的命令列執行下列命令：\
`$./pss_start.sh`

**將Primetime串流伺服器設定為Live Packager或HTTP原始伺服器**

若要將串流伺服器設定為Live Packager或Origin Server，請更新位於串流伺服器根目錄之conf目錄的pss.xml設定檔：

```
<Config> 
<!-- Set this false to disable the Origin Component. --> 
<OriginEnabled&gt;true&lt;/OriginEnabled>  
<!-- Set this false to disable the Packager Component. -->  
<PackagerEnabled&gt;true&lt;/PackagerEnabled>
</Config>
```

**停止Primetime串流伺服器**

若要停止串流伺服器，請在串流伺服器的根目錄中執行以下命令：\
`$./pss_stop.sh`

**重新啟動Primetime串流伺服器**

若要重新啟動串流伺服器，請停止並啟動串流伺服器。

<!-- 

Comment Type: draft

**Configuring Primetime Streaming Server**

Refer the Primetime Streaming Server Getting Started document for the configuration details available at [https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf](https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf).

-->

**解除安裝Primetime串流伺服器**

若要解除安裝串流伺服器，請停止串流伺服器，並移除Primetime目錄中的串流伺服器的pss目錄

## 使用Live Packager和Origin Server 1.4 {#working-with-live-packager-and-origin-server}

此區段適用於未使用Primetime串流伺服器，而是部署Primetime Live Packager和/或Primetime Origin Server的情況

### 最低系統需求 {#minimum-system-requirements-1}

**網路需求**

* 網路應啟用多點傳送，以便從編碼器傳送MPEG-TS資料流至Live Packager。 Live Packager也接受來自不需要多點傳送網路之編碼器的RTMP資料流。

**支援的作業系統**

* Linux CentOS 6.3 64位元

**硬體需求**

* 3.2GHz Intel® Pentium® 4處理器(建議使用雙Intel Xeon®或更快處理器)
* 64位元作業系統：4GB的RAM （建議使用8GB）
* 建議使用1Gb乙太網路卡（也支援多張網路卡和10Gb）
* 磁碟：

   * （磁碟 — SAS）：最少10GB (7,500RPM)
   * （磁碟 — SSD）：400MBps讀取/寫入
   * (NAS) ：1 GB專用連結

**軟體需求**

* oracleJava JRE 1.7 (建議： Sun/Oracle熱點JVM)。 Jconsole存取JMX API需要JDK

上述最低系統需求對於Origin Server和Live Packager都成立。

### 安裝及設定即時封裝程式 {#install-and-configure-the-live-packager}

**安裝即時封裝程式**

1. 從下載Java SE和JDK軟體 [oracle網站](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 並依照安裝指示操作。
1. 解壓縮Adobe Primetime - Live Packager 1.4封存檔案 `Primetime-LivePackager-1-4-0-b206-12042014.zip` 至您的磁碟。

**安裝HTTP原始伺服器**

1. 從下載Java JRE和JDK軟體 [oracle網站](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 並依照安裝指示操作。
1. 解壓縮Adobe Primetime - HTTP Origin Server 1.4封存檔案， `Primetime-HttpOrigin-1-4-0-b206-12042014.zip`，移至您的磁碟。

**啟動即時封裝程式** 若要啟動封裝程式，請從封裝程式的根目錄執行下列命令：\
`$packager_start.sh`

**啟動HTTP原始伺服器的方式**

若要啟動HTTP原始伺服器，請從原始伺服器根目錄的命令列執行下列命令：\
`$./origin_start.sh`

**停止即時封裝程式**

若要停止封裝程式，請從封裝程式的根目錄執行下列命令：\
`$packager_stop.sh`

**停止HTTP原始伺服器**

若要停止HTTP原始伺服器，請在原始伺服器的根目錄中執行下列命令：\
`$./origin_stop.sh`

**重新啟動即時封裝程式**

若要重新啟動封裝程式，請停止並啟動封裝程式。

**注意**：當封裝程式啟動時，會嘗試從臨時目錄中的片段目標初始化啟動載入資訊。 如果在片段目標找到啟動程式資訊，則表示封裝程式已重新啟動。 如果重新啟動，封裝程式會等待下一個片段邊界，然後開始封裝。 封裝程式會在啟動程式中插入間隙專案，指出遺漏片段。

**重新啟動HTTP原始伺服器**

若要重新啟動HTTP原始伺服器，請停止並啟動HTTP原始伺服器。

**設定即時封裝程式**

散發檔案包含可用於測試封裝器的設定範例。

解壓縮Adobe Primetime - Live Packager 1.4封存後，將目錄變更為packager目錄，並執行packager_start.sh指令碼。 範例設定監聽多點傳送位址239.235.0.3：14000，並在連線埠8080上執行本機原始伺服器。 輸出已設定為寫入 `packager/webroot/_default_/_default_/ directory`.

<!-- 

Comment Type: draft

For more details about the configuration refer [the Primetime Live Packager document](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

-->

**設定HTTP原始伺服器**

如需此處可用的設定詳細資訊，請參閱Primetime HTTP Origin Server快速入門檔案。

**解除安裝Live Packager**

若要解除安裝封裝程式，請停止封裝程式並從Primetime目錄移除封裝程式目錄。

**解除安裝HTTP原始伺服器**

若要解除安裝HTTP原始伺服器，請停止HTTP原始伺服器，並移除Primetime目錄中的HTTP原始伺服器的httporigin目錄。

## Adobe Primetime Offline Packager 1.4 {#adobe-primetime-offline-packager}

### 最低系統需求 {#minimum-system-requirements-2}

**支援的作業系統**

* Linux CentOS 6.3 64位元

**硬體需求**

* 3.2GHz Intel® Pentium® 4處理器(建議使用雙Intel Xeon®或更快處理器)
* 64位元作業系統：4GB的RAM （建議使用8GB）
* 建議使用1Gb乙太網路卡（也支援多張網路卡和10Gb）
* 磁碟：

   * （磁碟 — SAS）：最少10GB (7,500RPM)
   * （磁碟 — SSD）：400MBps讀取/寫入
   * (NAS) ：1 GB專用連結

**軟體需求**

* oracleJava JRE 1.7或更新版本。

### 安裝及設定Offline Packager {#install-and-configure-offline-packager}

若要安裝Offline Packager，請執行下列步驟：

1. 從下載Java SE軟體 [oracle網站](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 並依照安裝指示操作。
1. 解壓縮Adobe Primetime - Offline Packager 1.4封存檔案， `Primetime- OfflinePackager-1-4-0-b206-12042014.zip`，移至您的磁碟。

如需可用的設定詳細資訊，請參閱Primetime Offline Packager快速入門檔案 [此處](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

## 實用資源 {#helpful-resources}

* 如需完整說明檔案，請前往 [Adobe Primetime學習與支援](https://helpx.adobe.com/support/primetime.html) 頁面。
