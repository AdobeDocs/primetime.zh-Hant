---
seo-title: 效能調整
title: 效能調整
uuid: db8889c7-ecf5-4551-a6fc-1d3ab992b9ff
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# 效能調整{#performance-tuning}

使用下列提示協助提高效能：

* 使用網路HSM比使用直接連接的HSM要慢得多。
* 為提升效能，您可選擇部署位於SDK資料夾中的平台特定程式庫，以啟用加密 [!DNL thirdparty/cryptoj] 作業的原生支援。 若要啟用原生支援，請將平台的程式庫（Windows專用的jsafe.dll,Linux專用的libjsafe.so）新增至路徑。

   >[!NOTE]
   >
   >如果在同一Tomcat實例中運行多個Web應用 `jsafe.dll` 程式並且路徑上有，則只有載入的第一個Web應用程式能夠載入庫 `jsafe.dll` 。 因此，只有第一個Web應用程式才能享有原生支援的優點。 在這種情況下，為了改善所有Web應用程式的效能，請 `cryptoj.jar`置於WAR檔案之外。 例如，在目錄 `<tomcat_installation_folder>/lib` 中。

* 64位元作業系統（例如64位元版本的Red Hat®或Windows）可提供比32位元作業系統更佳的效能。

## 產生隨機數(Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

在某些情況下，Linux環境在執行需要隨機數字產生的與Primetime DRM相關的操作時可能會暫停，包括：

* 啟動Adobe Primetime DRM授權伺服器
* 使用實用程式生成策 [!DNL AdobePolicyManager] 略
* 將DRM保護的內容與Adobe Media Server或Primetime OfflinePackager封裝

這些操作中的延遲通常是由於Linux伺服器上的低熵池造成的。

在Linux上，隨機數是從伺服器環境的熵池中產生的。 熵池通常通過Linux內核接收硬體中斷來維護。 如果伺服器被隔離並且沒有從硬體資源（例如滑鼠或鍵盤）接收常規輸入，則可以延長等待重新填充熵池。 在此情況下，等待資料的操作可 [!DNL /dev/random] 能會暫停。

您可以在Linux伺服器上使用硬體隨機數生成器，以確保生成足夠的熵。 但是，如果在給定的部署方案中沒有硬體隨機數生成器，則可以使用基於軟體的解決方案來增加熵池刷新率。 在Linux上，此類軟體解決方 [!DNL haveged] 案之一是（HArdware Volatile Entropy Gathering and Expansion守護程式）。

## 確定可用熵 {#section_686B311FE6144566B6939E9F20915ADC}

要在意外延遲期間驗證給定伺服器的熵池中可用的位數，請執行以下命令：

```
cat /proc/sys/kernel/random/entropy_avail 
```

一個具有大量可用熵的健康Linux系統將會回到接近4,096位熵的狀態。 如果傳回的值小於200，系統的熵值會非常低。
