---
title: Mogfire Streaming Server版本
description: 黃金時段流式伺服器1.3和1.4版的新增功能。
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: 80c4687e-b0ac-48f2-a1c3-8751552da9d1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---

# Mogfire Streaming Server版本 {#primetime-streaming-server-x-releases}

黃金時段流式伺服器1.3和1.4版的新增功能。

## 黃金時段流式伺服器1.4（12月版）新增 {#what-s-new-in-primetime-streaming-server-december-release}

**離線打包程式**

* 輸出HLS流現在包含MPEG-2 TS中存在的ID3元資料
* HLS僅音頻流現在可以具有關聯的靜態影像
* 支援將IV作為HLS AES加密工作流的用戶輸入
* 支援在離線打包器生成IV時將IV輸出到檔案
* Playlist Creator現在支援將多語言音頻組和多語言WebVTT字幕組與媒體流關聯

**源伺服器**

* HLS AES加密可用於Live和VOD工作流。 黃金時段原點可以及時將HLS AES加密應用於傳入的HLS流或MP4檔案。
* 當用於將傳入的HDS流轉換為HLS流時，它還可以應用JIT HLS AES加密。
* Mighine Origin現在支援PHLS流的SWF允許清單。 早些時候，僅支援PHDS流

**黃金時段現場打包器**

* 支援為輸入RTMP和MPEG-2 TS流生成HLS AES-128流

已刷新PHDS/PHLS證書。 該項的新到期日為10/01/2016。

### **1.4版中包含的錯誤修復** {#bug-fixes-included-in-release}

* 由OfflinePackager 1.3.1建立的PTPUB-282-HLS設定級清單沒有編解碼器和解析度資訊。
* PTPUB-353 - PlayListCreator不支援在設定級別清單中添加WebVTT資訊
* PTPUB-583 - PlaylistCreator工具意外地預先使用組URI。
* PTPUB-605播放清單建立器未在每個變型流中列出SUBTITLE組
* PTPUB-634 — 離線打包器將SpliceInsert添加到清單中。
* PTPUB-635 — 為單個廣告提示插入多個SpliceOut標籤。

### 1.4版中的已知問題 {#known-issue-in-release}

* 即使在離線打包器配置中同時提供命令行提示和流內提示時指定DPIScte35模式，也強制PTPUB-645 DPISimple模式

## Mogfise Streaming Server 1.3.1(MAY Release)中的新增功能 {#what-s-new-in-primetime-streaming-server-may-release}

1.3.1版指修補程式。 以下增強功能使它成為推薦的客戶升級，因為它包括針對JIT MP4使用情形的關鍵效能增強：

1. 基於DRM的MP4 JIT m3u8生成的效能修復
1. 已添加配置「CopyQueryParamToJITFragmentURIs」，以將查詢參數從JIT清單請求複製到生成的用於MP4 JIT轉換的片段URI。 有關示例用法，請參閱HTTP Origin Server文檔
1. 允許通過添加到vod.xml的Config/MP4Only配置，在不擴展的情況下進行JIT轉換的MP4檔案

### 1.3.1版中包含的錯誤修復 {#bug-fixes-included-in-release-1}

* 3759167 — 並非所有SCTE35提示都是由於打包時時間戳異常而導致輸出清單。 在SCTE35消息中SpliceInfoSection的TimeSignal中對SpliceTime應用pts_adjustment。

### 1.3.1版中的已知問題 {#known-issues-in-release}

* 3717039 — 當打包器配置為生成DPI簡單模式提示時，它確實應該尋找特定的信號類型，如剪接插入或放置機會，並僅將這些信號轉換為簡單模式提示。 它應忽略程式啟動、網路啟動等其它類型的信號。

* 3718598 — 當配置Origin Server以通過啟用HSM訪問來提供受保護內容時，後端LunaSA客戶端會頻繁與HSM模組通信

## 黃金時段流式伺服器1.3（4月版）的新增功能 {#what-s-new-in-primetime-streaming-server-april-release}

黃金時段1.3版為流內容、更好的可用性和安全性帶來了幾項新功能。

**Mighine Streaming Server作為Live Packager和Origin Server的統一形式**

黃金時段即時打包器和黃金時段原點作為單個元件一起工作。 此元件可以用作打包器或源，或使用組合功能來打包和承載即時流。

這為這些伺服器提供了統一的檔案介面，使它們易於在單台電腦上運行。 它繼續提供靈活性，可以配置為單獨的打包程式或源。

**Beta MPEG-DASH支援**

黃金時段流式伺服器支援MPEG-DASH打包，用於即時和視頻點播工作流。 Live打包器元件將接收的RTMP或MPEG-2-TS流轉換為DASH格式。 「原點」(Origin)元件接受DASH流。

對於VOD工作流，離線打包器元件將MP4和TS資產轉換為MPEG-DASH ISOBFF格式。

**即時到VOD轉換**

現在，新的元件錄制伺服器可用，它支援捕獲即時流和存檔以進行VOD播放。 它支援建立完整事件重放以及部分事件的剪輯/突出顯示。 它可以配置為在Live內容中記錄僅音頻流、刪除廣告或平板。 錄制伺服器與Mighine Streaming Server以及第三方Origins一起工作。

**黃金時段即時打包機RTMP到HLS的轉換**

Mighine Live Packager元件支援從RTMP流建立HLS流。 它還允許向輸出HLS流添加黃金時段DRM和受保護流。

**將傳入RTMP流驗證到Mighile Live Packager**

現在，用戶mgmt.jar隨Mogfire Live Packager一起提供，用於在將RTMP流發送到Migfire Live Packager時使用可信憑據配置訪問

現在，可以將編碼器配置為在將流發送到Live Packager時使用用戶名/密碼。

**用於為HDS和HLS建立頂級清單的PlaylistCreator工具**

Gimphire Offline Packager現在提供了一個巧妙的實用程式PlaylistCreator.jar，可輕鬆建立HDS和HLS資產的頂級清單檔案。

**附加安全功能，以合併硬體安全模組**

Mogine Offline Packager現在支援從硬體安全模組訪問Packager憑據證書和公用密鑰。

硬體安全模組為這些機密資產提供額外保護。

**VOD打包的效能改進**

為縮短黃金時段離線打包器中夾層資產的打包時間，已採用若干效能增強功能

**JIT MP4封裝效能的提高**

黃金時段原點的JIT打包功能已經融入了若干效能增強功能，以處理用戶對大型視頻點播資產庫的請求。

## Adobe Primetime流伺服器1.4 {#adobe-primetime-streaming-server}

### 最低系統要求 {#minimum-system-requirements}

**網路要求**

* 網路應啟用多播，以便將MPEG-TS流從編碼器發送到Live Packager。 Live Packager還接受來自不需要多播網路的編碼器的RTMP流。

**支援的作業系統**

* Linux CentOS 6.3 64位

**硬體要求**

* 3.2 GHz英特爾®奔騰® 4處理器（建議雙英特爾至強®或更快）
* 64位作業系統：4GB的RAM（建議8GB）
* 建議使用1 Gb乙太網卡（還支援多個網卡和10 Gb）
* 磁碟：

   * （磁碟 — SAS）:7.5K RPM，最低10GB
   * （磁碟 — SSD）:400MBps讀/寫
   * (NAS):1 GB專用鏈路

**軟體要求**

* OracleJava JRE 1.7(建議：Sun/Oracle熱點JVM)。 JDK是JConsole訪問JMX API所必需的

### 安裝和配置Mogfire Streaming Server {#install-and-configure-primetime-streaming-server}

**安裝流式伺服器**

1. 從 [Oracle站點](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 並按照安裝說明進行操作。
2. 解壓縮Adobe Primetime流伺服器1.4存檔檔案， `Primetime- StreamingServer-1-4-0-b206-12042014.zip` 光碟。

**啟動Mogfire Streaming Server**

要啟動流伺服器，請從流伺服器根目錄的命令行執行以下命令：\
`$./pss_start.sh`

**將黃金時段流伺服器配置為即時打包器或HTTP源伺服器**

要將流伺服器配置為Live Packager或Origin Server，請更新位於流伺服器根目錄中conf目錄的pss.xml配置檔案：

```
<Config> 
<!-- Set this false to disable the Origin Component. --> 
<OriginEnabled&gt;true&lt;/OriginEnabled>  
<!-- Set this false to disable the Packager Component. -->  
<PackagerEnabled&gt;true&lt;/PackagerEnabled>
</Config>
```

**停止黃金時段流伺服器**

要停止流式伺服器，請在流伺服器的根目錄中執行以下命令：\
`$./pss_stop.sh`

**重新啟動Mogfise Streaming Server**

要重新啟動流式伺服器，請停止並啟動流式伺服器。

<!-- 

Comment Type: draft

**Configuring Primetime Streaming Server**

Refer the Primetime Streaming Server Getting Started document for the configuration details available at [https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf](https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf).

-->

**卸載Mogfire Streaming Server**

要卸載流伺服器，請停止流伺服器，並刪除Mighine目錄中Streaming Server的pss目錄

## 使用Live Packager和Origin Server 1.4 {#working-with-live-packager-and-origin-server}

本節適用於未使用Mogfire Streaming Server，而是部署Mogfire Live Packager AND/OR Migfire Origin Server

### 最低系統要求 {#minimum-system-requirements-1}

**網路要求**

* 網路應啟用多播，以便將MPEG-TS流從編碼器發送到Live Packager。 Live Packager還接受來自不需要多播網路的編碼器的RTMP流。

**支援的作業系統**

* Linux CentOS 6.3 64位

**硬體要求**

* 3.2 GHz英特爾®奔騰® 4處理器（建議雙英特爾至強®或更快）
* 64位作業系統：4GB的RAM（建議8GB）
* 建議使用1 Gb乙太網卡（還支援多個網卡和10 Gb）
* 磁碟：

   * （磁碟 — SAS）:7.5K RPM，最低10GB
   * （磁碟 — SSD）:400MBps讀/寫
   * (NAS):1 GB專用鏈路

**軟體要求**

* OracleJava JRE 1.7(建議：Sun/Oracle熱點JVM)。 JDK是JConsole訪問JMX API所必需的

上述最低系統要求適用於Origin Server和Live Packager。

### 安裝和配置Live Packager {#install-and-configure-the-live-packager}

**安裝Live Packager**

1. 從 [Oracle站點](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 並按照安裝說明進行操作。
1. 解壓Adobe Primetime- Live Packager 1.4存檔檔案 `Primetime-LivePackager-1-4-0-b206-12042014.zip` 光碟。

**安裝HTTP源伺服器**

1. 從 [Oracle站點](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 並按照安裝說明進行操作。
1. 解壓Adobe Primetime- HTTP Origin Server 1.4存檔檔案， `Primetime-HttpOrigin-1-4-0-b206-12042014.zip`，到光碟。

**啟動即時打包程式** 要啟動打包程式，請從打包程式的根目錄中執行以下命令：\
`$packager_start.sh`

**啟動HTTP源伺服器**

要啟動HTTP源伺服器，請從源伺服器根目錄的命令行執行以下命令：\
`$./origin_start.sh`

**停止即時打包程式**

要停止打包程式，請從打包程式的根目錄中執行以下命令：\
`$packager_stop.sh`

**停止HTTP源伺服器**

要停止HTTP源伺服器，請在源伺服器的根目錄中執行以下命令：\
`$./origin_stop.sh`

**重新啟動Live Packager**

要重新啟動打包器，請停止並啟動打包器。

**注釋**:打包器啟動時，會嘗試從臨時目錄中的片段目標初始化引導資訊。 如果在片段目標上找到引導資訊，則表明已重新啟動打包程式。 在重新啟動時，打包器會等待到下一個片段邊界，然後開始打包。 打包器在引導程式中插入一個間隙條目，以指示缺少片段。

**重新啟動HTTP源伺服器**

要重新啟動HTTP源伺服器，請停止並啟動HTTP源伺服器。

**配置即時打包器**

分發檔案包含可用於測試打包器的示例配置。

在解壓Adobe Primetime- Live Packager 1.4存檔檔案後，將目錄更改到打包器目錄，並運行packager_start.sh指令碼。 示例配置偵聽多播地址239.235.0.3:14000，並在埠8080上運行本地源伺服器。 將輸出配置為寫入 `packager/webroot/_default_/_default_/ directory`。

<!-- 

Comment Type: draft

For more details about the configuration refer [the Primetime Live Packager document](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

-->

**配置HTTP源伺服器**

有關此處提供的配置詳細資訊，請參閱黃金時段HTTP源伺服器入門文檔。

**卸載Live Packager**

要卸載打包程式，請停止打包程式並從Mighide目錄中刪除打包程式目錄。

**卸載HTTP源伺服器**

要卸載HTTP源伺服器，請停止HTTP源伺服器，並刪除Mighine目錄中HTTP源伺服器的httpporigin目錄。

## Adobe Primetime離線打包器1.4 {#adobe-primetime-offline-packager}

### 最低系統要求 {#minimum-system-requirements-2}

**支援的作業系統**

* Linux CentOS 6.3 64位

**硬體要求**

* 3.2 GHz英特爾®奔騰® 4處理器（建議雙英特爾至強®或更快）
* 64位作業系統：4GB的RAM（建議8GB）
* 建議使用1 Gb乙太網卡（還支援多個網卡和10 Gb）
* 磁碟：

   * （磁碟 — SAS）:7.5K RPM，最低10GB
   * （磁碟 — SSD）:400MBps讀/寫
   * (NAS):1 GB專用鏈路

**軟體要求**

* OracleJava JRE 1.7或更高版本。

### 安裝和配置離線打包程式 {#install-and-configure-offline-packager}

要安裝離線打包程式，請執行以下步驟：

1. 從 [Oracle站點](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 並按照安裝說明進行操作。
1. 解壓Adobe Primetime — 離線打包程式1.4存檔檔案， `Primetime- OfflinePackager-1-4-0-b206-12042014.zip`，到光碟。

有關可用的配置詳細資訊，請參閱Mogine Offline Packager入門文檔 [這裡](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)。

## 有用的資源 {#helpful-resources}

* 請參閱以下網址的完整幫助文檔 [Adobe Primetime學習和支援](https://helpx.adobe.com/support/primetime.html) 的子菜單。
