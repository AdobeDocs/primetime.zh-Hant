---
title: 效能調整
description: 效能調整
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 效能調整{#performance-tuning}

使用下列提示來協助提高效能：

* 使用網路HSM會比使用直接連線的HSM慢很多。
* 為改善效能，您可以部署位於以下位置的平台特定程式庫，選擇性地啟用密碼編譯作業的原生支援： [!DNL thirdparty/cryptoj] SDK的資料夾。 若要啟用原生支援，請將您平台的程式庫（適用於Windows的jsafe.dll或適用於Linux的libjsafe.so）新增至路徑。

  >[!NOTE]
  >
  >如果您在同一Tomcat執行個體中執行多個Web應用程式，而且具有 `jsafe.dll` 在路徑上，只有第一個載入的Web應用程式才能載入 `jsafe.dll` 資料庫。 因此，只有第一個網頁應用程式才能享有原生支援的好處。 在這種情況下，若要改善所有Web應用程式的效能，請將 `cryptoj.jar`在WAR檔案外部。 例如，在 `<tomcat_installation_folder>/lib` 目錄。

* 64位元作業系統(例如Red Hat®或Windows的64位元版本)比32位元作業系統提供更好的效能。

## 產生隨機數字(Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

在某些情況下，Linux環境在進行需要隨機數字產生的Primetime DRM相關作業時可能會暫停，包括：

* 啟動Adobe Primetime DRM授權伺服器
* 使用產生原則 [!DNL AdobePolicyManager] 公用程式
* 使用Adobe Media Server或Primetime OfflinePackager封裝受DRM保護的內容

這些作業期間的延遲通常是因為Linux伺服器上的低平均資訊量集區所造成。

在Linux上，隨機數字會從伺服器環境的平均資訊量集區產生。 平均資訊量集區通常是透過接收Linux核心的硬體中斷來維護。 如果伺服器被隔離且未收到硬體資源（例如滑鼠或鍵盤）的定期輸入，則重新填滿平均資訊量集區的等待時間可能會延長。 在此案例中，等待資料來自的作業 [!DNL /dev/random] 可能會暫停。

您可以在Linux伺服器上使用硬體隨機數字產生器，以確保產生足夠的平均資訊量。 不過，如果指定的部署案例中沒有硬體隨機數字產生器，您可以使用軟體解決方案來增加平均資訊量集區重新整理率。 在Linux上的這類軟體解決方案之一是 [!DNL haveged] (HArdware Volatile Entropy Gathering and Expansion daemon)。

## 決定可用的平均資訊量 {#section_686B311FE6144566B6939E9F20915ADC}

若要確認在意外的延遲期間，特定伺服器的Entropy集區中可用的位元數，請執行下列命令：

```
cat /proc/sys/kernel/random/entropy_avail 
```

健全的Linux系統，若有大量的可用平均資訊量，將可傳回接近完整的4,096位元平均資訊量。 如果傳回的值小於200，則系統的平均資訊量會很低。
