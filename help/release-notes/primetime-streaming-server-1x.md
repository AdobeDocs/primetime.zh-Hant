---
title: Primetime Streaming Server版本
description: Primetime Streaming Server 1.3和1.4版本的新增功能。
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---


# Primetime Streaming Server版本{#primetime-streaming-server-x-releases}

Primetime Streaming Server 1.3和1.4版本的新增功能。

## Primetime Streaming Server 1.4（12月發行）的新功能{#what-s-new-in-primetime-streaming-server-december-release}

**Offline Packager**

* 輸出HLS串流現在包含MPEG-2 TS中顯示的ID3中繼資料
* 僅限HLS音頻流現在可以具有關聯的靜態影像
* 支援為HLS AES加密工作流程提供IV作為用戶輸入
* 支援在離線封裝工具產生IV時，將IV輸出至檔案
* Playlist Creator現在支援將多語言音訊群組和多語言WebVTT子標題群組與媒體串流產生關聯

**原始伺服器**

* HLS AES加密適用於即時和VOD工作流程。 Primetime原始碼可以及時將HLS AES加密應用到傳入的HLS流或MP4檔案。
* 它還可以在用於將傳入的HDS流轉換到HLS流時應用JIT HLS AES加密。
* Primetime原點現在支援SWF允許PHLS串流的清單。 之前僅支援PHDS串流

**Primetime Live Packager**

* 支援為輸入的RTMP和MPEG-2 TS串流產生HLS AES-128串流

已重新整理PHDS/PHLS憑證。 相同之新到期日為2016年10月1日。

### **1.4版包含的錯誤修正** {#bug-fixes-included-in-release}

* PTPUB-282-由OfflinePackager 1.3.1建立的HLS設定層級資訊清單沒有編碼解碼器和解析度資訊。
* PTPUB-353 - PlayListCreator不支援在設定層級資訊清單中新增WebVTT資訊
* PTPUB-583 - PlaylistCreator工具意外地預先決定URI的群組。
* PTPUB-605播放清單製作程式未在每個變型串流中列出SUBTITLE群組
* PTPUB-634 - Offline Packager新增SpliceInsert至manifest。
* PTPUB-635-針對單一廣告提示插入多個SpliceOut標籤。

### 1.4版{#known-issue-in-release}中的已知問題

* 即使在離線封裝設定中同時提供命令列提示和串流內提示時指定DPIScte35模式，PTPUB- 645 DPISimple模式仍會強制執行

## Primetime Streaming Server 1.3.1（5月發行版）的新增功能{#what-s-new-in-primetime-streaming-server-may-release}

1.3.1版是指修補程式。 以下增強功能讓客戶建議升級，因為它包含JIT MP4使用案例的主要效能增強功能：

1. 使用DRM（包括密鑰輪替）在原點生成MP4 JIT m3u8的效能修正
1. 已新增「CopyQueryParamToJITFragmentURIs」組態，將查詢參數從JIT資訊清單請求複製至產生的片段URI，以進行MP4 JIT轉換。 請參閱HTTP原始伺服器檔案以取得範例使用
1. 透過新增至vod.xml的Config/MP4Only設定，允許MP4檔案不需副檔名，即可進行JIT轉換

### 1.3.1 {#bug-fixes-included-in-release-1}版中包含的錯誤修正

* 3759167 —— 並非所有SCTE35提示都會因為封裝時的時間戳記異常而進入輸出資訊清單。 在SCTE35消息中SpliceInfoSection的TimeSignal中對SpliceTime應用pts_adjustment。

### 1.3.1版{#known-issues-in-release}中的已知問題

* 3717039 —— 當封裝程式設定為產生DPI簡單模式提示時，它確實應該尋找特定的訊號類型，例如接合插入或放置機會，並僅將這些訊號轉換為簡單模式提示。 它應忽略其它類型的信號，如程式啟動、網路啟動等。

* 3718598 —— 將Origin Server配置為使用啟用HSM訪問的保護內容服務時，後端LunaSA客戶端會頻繁與HSM模組通信

## Primetime Streaming Server 1.3（4月發行）的新增功能{#what-s-new-in-primetime-streaming-server-april-release}

Primetime 1.3版為串流內容、更佳的可用性與安全性帶來多項新功能。

**Primetime Streaming Server是Live Packager和Origin Server的統一形式**

Primetime Live Packager和Primetime Origin可整合為單一元件。 此元件可用作Packager或Origin，或使用結合的功能來封裝和代管即時串流。

這為這些伺服器提供了統一的檔案介面，使它們易於在單台電腦上運行。 它繼續提供將配置為獨立Packager或Origin的靈活性。

**測試版MPEG- DASH支援**

Primetime Streaming Server支援即時和VOD工作流程的MPEG-DASH封裝。 Live Packager元件會將內嵌的RTMP或MPEG-2-TS串流轉換為DASH格式。 原始元件接受DASH流。

對於VOD工作流程，Offline Packager元件會將MP4和TS資產轉換為MPEG-DASH ISOBFF格式。

**即時到VOD轉換**

現在提供新的元件錄制伺服器，可支援擷取即時串流並封存以供VOD播放。 它支援建立完整事件重播，以及部分活動的片段／反白顯示。 它可設定為錄制純音訊串流、移除即時內容中的廣告或儲存格。 Recording Server可與Primetime Streaming Server及協力廠商Origins搭配使用。

**Primetime Live Packager中的RTMP到HLS轉換**

Primetime Live Packager元件支援從RTMP串流建立HLS串流。 它還允許將Primetime DRM和受保護流添加到輸出HLS流。

**Primetime Live Packager傳入RTMP串流的驗證**

usermgmt.jar現在隨Primetime Live Packager提供，可在傳送RTMP串流至Primetime Live Packager時，使用受信任的憑證來設定存取權

現在，可將編碼器設定為在傳送串流至Live Packager時使用使用者名稱／密碼。

**PlaylistCreator工具，以建立HDS和HLS的頂層清單**

Primetime Offline Packager現在提供一個精巧的公用程式PlaylistCreator.jar，可輕鬆建立HDS和HLS資產的頂層資訊清單檔案。

**其他安全性功能，以整合硬體安全性模組**

Primetime Offline Packager現在支援從硬體安全模組存取Packager憑證和常用金鑰。

硬體安全模組為這些機密資產提供附加保護。

**改善VOD封裝的效能**

Primetime Offline Packager已整合數種效能增強功能，以縮短夾層資產的封裝時間

**JIT MP4包裝的效能提升**

Primetime Origin的JIT封裝功能已整合數種效能增強功能，以處理大量VOD資產的使用者要求。

## Adobe PrimetimeStreaming Server 1.4 {#adobe-primetime-streaming-server}

### 最低系統需求{#minimum-system-requirements}

**網路需求**

* 應啟用「網路多點傳播」，將MPEG-TS串流從編碼器傳送至Live Packager。 Live Packager也可接受來自不需要多點傳播網路的編碼器的RTMP串流。

**支援的作業系統**

* Linux CentOS 6.3 64位元

**硬體需求**

* 3.2GHz Intel® Pentium® 4處理器（建議使用雙Intel Xeon®或速度更快的處理器）
* 64位元作業系統：4GB的記憶體（建議使用8GB）
* 建議使用1Gb乙太網卡（也支援多張網路卡和10Gb）
* 磁碟：

   * （磁碟-SAS）:7.5K RPM，最低10GB
   * （磁碟——固態硬碟）:400MBps讀／寫
   * (NAS):1 GB專用鏈路

**軟體需求**

* OracleJava JRE 1.7(建議：Sun/Oracle熱點JVM)。 JConsole存取JMX API時需要JDK

### 安裝和配置Primetime Streaming Server {#install-and-configure-primetime-streaming-server}

**安裝串流伺服器**

1. 從[Oracle站點](https://www.oracle.com/technetwork/java/javase/downloads/index.html)下載Java SE和JDK軟體，然後按照安裝說明操作。
2. 將`Primetime- StreamingServer-1-4-0-b206-12042014.zip`的Adobe Primetime-Streaming Server 1.4存檔檔案解壓到磁碟。

**啟動Primetime串流伺服器**

要啟動Streaming Server，請從Streaming Server根目錄中的命令行執行以下命令：\
`$./pss_start.sh`

**將Primetime串流伺服器設定為Live Packager或HTTP Origin Server**

若要將串流伺服器設定為Live Packager或Origin Server，請更新位於串流伺服器根目錄conf目錄的pss.xml設定檔案：

```
<Config> 
<!-- Set this false to disable the Origin Component. --> 
<OriginEnabled&gt;true&lt;/OriginEnabled>  
<!-- Set this false to disable the Packager Component. -->  
<PackagerEnabled&gt;true&lt;/PackagerEnabled>
</Config>
```

**停止Primetime串流伺服器**

要停止Streaming Server，請在Streaming Server的根目錄中執行以下命令：\
`$./pss_stop.sh`

**重新啟動Primetime串流伺服器**

要重新啟動Streaming Server，請停止並啟動Streaming Server。

<!-- 

Comment Type: draft

**Configuring Primetime Streaming Server**

Refer the Primetime Streaming Server Getting Started document for the configuration details available at [https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf](https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf).

-->

**解除安裝Primetime串流伺服器**

若要解除安裝Streaming Server，請停止Streaming Server，並移除Primetime目錄中Streaming Server的pss目錄

## 使用Live Packager和Origin Server 1.4 {#working-with-live-packager-and-origin-server}

本節適用於未使用Primetime Streaming Server，而部署Primetime Live Packager AND/OR Primetime Origin Server的情況

### 最低系統需求{#minimum-system-requirements-1}

**網路需求**

* 應啟用「網路多點傳播」，將MPEG-TS串流從編碼器傳送至Live Packager。 Live Packager也可接受來自不需要多點傳播網路的編碼器的RTMP串流。

**支援的作業系統**

* Linux CentOS 6.3 64位元

**硬體需求**

* 3.2GHz Intel® Pentium® 4處理器（建議使用雙Intel Xeon®或速度更快的處理器）
* 64位元作業系統：4GB的記憶體（建議使用8GB）
* 建議使用1Gb乙太網卡（也支援多張網路卡和10Gb）
* 磁碟：

   * （磁碟-SAS）:7.5K RPM，最低10GB
   * （磁碟——固態硬碟）:400MBps讀／寫
   * (NAS):1 GB專用鏈路

**軟體需求**

* OracleJava JRE 1.7(建議：Sun/Oracle熱點JVM)。 JConsole存取JMX API時需要JDK

上述最低系統需求適用於Origin Server和Live Packager。

### 安裝並配置Live Packager {#install-and-configure-the-live-packager}

**安裝Live Packager**

1. 從[Oracle站點](https://www.oracle.com/technetwork/java/javase/downloads/index.html)下載Java SE和JDK軟體，然後按照安裝說明操作。
1. 將Adobe Primetime- Live Packager 1.4存檔檔案`Primetime-LivePackager-1-4-0-b206-12042014.zip`解壓到磁碟。

**安裝HTTP原始伺服器**

1. 從[Oracle站點](https://www.oracle.com/technetwork/java/javase/downloads/index.html)下載Java JRE和JDK軟體，然後按照安裝說明操作。
1. 將Adobe Primetime- HTTP Origin Server 1.4存檔檔案`Primetime-HttpOrigin-1-4-0-b206-12042014.zip`解壓到磁碟。

**要啟動Live** Packager要啟動Packager，請從Packager的根目錄執行以下命令：\
`$packager_start.sh`

**啟動HTTP源伺服器**

要啟動HTTP源伺服器，請從源伺服器根目錄中的命令行執行以下命令：\
`$./origin_start.sh`

**停止Live Packager**

要停止Packager，請從Packager的根目錄中執行以下命令：\
`$packager_stop.sh`

**停止HTTP原始伺服器**

要停止HTTP源伺服器，請在源伺服器的根目錄中執行以下命令：\
`$./origin_stop.sh`

**重新啟動Live Packager**

要重新啟動打包器，請停止並啟動打包器。

**注意**:當軟體包啟動時，它嘗試從臨時目錄中的片段目標初始化引導資訊。如果在片段目標處找到引導資訊，則表示已重新啟動包裝程式。 在重新啟動時，封裝程式會等到下一個片段邊界，然後開始封裝。 封裝程式會在引導程式中插入間隙項目，以指出有遺失片段。

**重新啟動HTTP原始伺服器**

要重新啟動HTTP源伺服器，請停止並啟動HTTP源伺服器。

**設定Live Packager**

分發檔案包含可用於測試軟體包的示例配置。

解壓縮Adobe Primetime- Live Packager 1.4檔案後，將目錄變更為packager目錄，然後執行packager_start.sh指令碼。 示例配置偵聽多點傳播地址239.235.0.3:14000，並在埠8080上運行本地源伺服器。 輸出被配置為寫入到`packager/webroot/_default_/_default_/ directory`。

<!-- 

Comment Type: draft

For more details about the configuration refer [the Primetime Live Packager document](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

-->

**配置HTTP源伺服器**

請參閱Primetime HTTP Origin Server快速入門檔案，以取得這裡的設定詳細資訊。

**解除安裝Live Packager**

若要解除安裝封裝程式，請停止封裝程式並從Primetime目錄移除封裝程式目錄。

**卸載HTTP源伺服器**

若要解除安裝HTTP原始伺服器，請停止HTTP原始伺服器，並移除Primetime目錄中HTTP原始伺服器的httporigin目錄。

## Adobe PrimetimeOffline Packager 1.4 {#adobe-primetime-offline-packager}

### 最低系統需求{#minimum-system-requirements-2}

**支援的作業系統**

* Linux CentOS 6.3 64位元

**硬體需求**

* 3.2GHz Intel® Pentium® 4處理器（建議使用雙Intel Xeon®或速度更快的處理器）
* 64位元作業系統：4GB的記憶體（建議使用8GB）
* 建議使用1Gb乙太網卡（也支援多張網路卡和10Gb）
* 磁碟：

   * （磁碟-SAS）:7.5K RPM，最低10GB
   * （磁碟——固態硬碟）:400MBps讀／寫
   * (NAS):1 GB專用鏈路

**軟體需求**

* OracleJava JRE 1.7或更新版本。

### 安裝並配置Offline Packager {#install-and-configure-offline-packager}

要安裝Offline Packager，請執行以下步驟：

1. 從[Oracle站點](https://www.oracle.com/technetwork/java/javase/downloads/index.html)下載Java SE軟體，然後按照安裝說明操作。
1. 將Adobe Primetime- Offline Packager 1.4存檔檔案`Primetime- OfflinePackager-1-4-0-b206-12042014.zip`解壓到磁碟。

請參閱Primetime Offline Packager快速入門檔案，以取得[這裡](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)的設定詳細資訊。

## 實用資源{#helpful-resources}

* 請參閱[Adobe Primetime學習與支援](https://helpx.adobe.com/support/primetime.html)頁面的完整說明檔案。