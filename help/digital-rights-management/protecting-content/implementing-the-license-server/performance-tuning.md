---
title: 效能調整
description: 效能調整
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# 效能調整{#performance-tuning}

使用下列提示協助提高效能：

* 使用網路HSM比使用直接連接的HSM要慢得多。
* 為提升效能，您可選擇部署位於SDK [!DNL thirdparty/cryptoj]資料夾中的平台特定程式庫，以啟用加密作業的原生支援。 若要啟用原生支援，請將平台的程式庫（Windows專用的jsafe.dll,Linux專用的libjsafe.so）新增至路徑。

   >[!NOTE]
   >
   >如果在同一個Tomcat實例中運行多個Web應用程式並且路徑上具有`jsafe.dll` ，則只有載入的第一個Web應用程式能夠載入`jsafe.dll`庫。 因此，只有第一個Web應用程式才能享有原生支援的優點。 在這種情況下，要提高所有Web應用程式的效能，請將`cryptoj.jar`置於WAR檔案之外。 例如，在`<tomcat_installation_folder>/lib`目錄中。

* 64位元作業系統（例如64位元版本的Red Hat®或Windows）可提供比32位元作業系統更佳的效能。

## 生成隨機數(Linux){#section_3E2E936A538F40B7BF8892C65E117907}

在某些情況下，Linux環境在執行需要隨機數字產生的與Primetime DRM相關的操作時可能會暫停，包括：

* 啟動Adobe PrimetimeDRM許可證伺服器
* 使用[!DNL AdobePolicyManager]實用程式生成策略
* 將受DRM保護的內容與Adobe Medium伺服器或Primetime OfflinePackager封裝

這些操作中的延遲通常是由於Linux伺服器上的低熵池造成的。

在Linux上，隨機數是從伺服器環境的熵池中產生的。 熵池通常通過Linux內核接收硬體中斷來維護。 如果伺服器被隔離並且沒有從硬體資源（例如滑鼠或鍵盤）接收常規輸入，則可以延長等待重新填充熵池。 在此情況下，等待[!DNL /dev/random]資料的操作可能會暫停。

您可以在Linux伺服器上使用硬體隨機數生成器，以確保生成足夠的熵。 但是，如果在給定的部署方案中沒有硬體隨機數生成器，則可以使用基於軟體的解決方案來增加熵池刷新率。 在Linux上，此類軟體解決方案之一是[!DNL haveged]（HArdware Volatile Entropy Gathering and Expansion守護程式）。

## 確定可用熵{#section_686B311FE6144566B6939E9F20915ADC}

要在意外延遲期間驗證給定伺服器的熵池中可用的位數，請執行以下命令：

```
cat /proc/sys/kernel/random/entropy_avail 
```

一個具有大量可用熵的健康Linux系統將會回到接近4,096位熵的狀態。 如果傳回的值小於200，系統的熵值會非常低。
