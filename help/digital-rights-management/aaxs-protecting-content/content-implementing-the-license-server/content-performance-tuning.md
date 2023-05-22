---
title: 效能調整
description: 效能調整
copied-description: true
exl-id: f6b2338e-a209-4881-a599-ded5f1498daf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# 效能調整{#performance-tuning}

使用以下提示幫助提高效能：

* 使用網路HSM比使用直接連接的HSM要慢得多。
* 為了提高效能，您可以選擇通過部署位於SDK「第三方/密碼」資料夾中的平台特定庫來啟用對加密操作的本機支援。 要啟用本機支援，請將平台的庫（用於Windows的jsafe.dll或用於Linux的libjsafe.so）添加到路徑中。

   >[!NOTE]
   >
   >如果在同一Tomcat實例中運行多個Web應用程式，並且 `jsafe.dll` 在路徑上，只有載入的第一個Web應用程式能夠載入 `jsafe.dll` 的下界。 因此，只有第一個Web應用程式才能獲得本機支援的好處。 在這種情況下，要提高所有Web應用程式的效能，請 `cryptoj.jar`在戰爭檔案之外。 例如，在 `<tomcat_installation_folder>/lib` 的子菜單。

* 64位作業系統（如64位版本的Red Hat®或Windows）比32位作業系統提供了更好的效能。
