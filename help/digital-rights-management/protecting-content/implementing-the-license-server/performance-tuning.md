---
title: 效能調整
description: 效能調整
copied-description: true
exl-id: 1b54b7c2-da32-47db-b57f-b2afbaf386c4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 效能調整{#performance-tuning}

使用以下提示幫助提高效能：

* 使用網路HSM比使用直接連接的HSM要慢得多。
* 為了提高效能，您可以選擇通過部署位於 [!DNL thirdparty/cryptoj] 資料夾。 要啟用本機支援，請將平台的庫（用於Windows的jsafe.dll或用於Linux的libjsafe.so）添加到路徑中。

   >[!NOTE]
   >
   >如果在同一Tomcat實例中運行多個Web應用程式，並且 `jsafe.dll` 在路徑上，只有載入的第一個Web應用程式能夠載入 `jsafe.dll` 的下界。 因此，只有第一個Web應用程式才能獲得本機支援的好處。 在這種情況下，要提高所有Web應用程式的效能，請 `cryptoj.jar`在戰爭檔案之外。 例如，在 `<tomcat_installation_folder>/lib` 的子菜單。

* 64位作業系統（如64位版本的Red Hat®或Windows）比32位作業系統提供了更好的效能。

## 生成隨機數(Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

在某些情況下，Linux環境在執行黃金時段DRM相關操作時可能會暫停，這些操作需要隨機數生成，包括：

* 啟動Adobe PrimetimeDRM許可證伺服器
* 使用 [!DNL AdobePolicyManager] 實用
* 將受DRM保護的內容與Adobe Medium伺服器或Mogine OfflinePackager打包

這些操作中的延遲通常是Linux伺服器上低熵池的結果。

在Linux上，隨機數從伺服器環境的熵池中產生。 熵池通常通過Linux內核接收硬體中斷來維護。 如果伺服器被隔離並且沒有從硬體資源（例如滑鼠或鍵盤）接收常規輸入，則可以擴展等待重新填充熵池。 在此方案中，等待資料的操作 [!DNL /dev/random] 可以暫停。

您可以在Linux伺服器上使用硬體隨機數生成器來確保生成足夠的熵。 但是，如果在給定的部署方案中沒有硬體隨機數生成器，則可以使用基於軟體的解決方案來增加熵池刷新率。 在Linux上，這樣的軟體解決方案之一是 [!DNL haveged] （HArdware Volatile Entropy Gathering and Expansion守護程式）。

## 確定可用熵 {#section_686B311FE6144566B6939E9F20915ADC}

要在意外延遲期間驗證給定伺服器的熵池中可用的位數，請執行以下命令：

```
cat /proc/sys/kernel/random/entropy_avail 
```

一個健康的Linux系統，有大量的熵值，將回到接近4096位的熵值。 如果返回的值小於200，則系統運行的熵非常低。
