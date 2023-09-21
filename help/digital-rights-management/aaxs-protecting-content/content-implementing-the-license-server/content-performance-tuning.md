---
title: 效能調整
description: 效能調整
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# 效能調整{#performance-tuning}

使用下列提示來協助提高效能：

* 使用網路HSM會比使用直接連線的HSM慢很多。
* 為改善效能，您可以部署位於SDK「第三方/cryptoj」資料夾中的平台特定程式庫，選擇啟用密碼編譯作業的原生支援。 若要啟用原生支援，請將您平台的程式庫（適用於Windows的jsafe.dll或適用於Linux的libjsafe.so）新增至路徑。

  >[!NOTE]
  >
  >如果您在同一Tomcat執行個體中執行多個Web應用程式，而且具有 `jsafe.dll` 在路徑上，只有第一個載入的Web應用程式才能載入 `jsafe.dll` 資料庫。 因此，只有第一個網頁應用程式才能享有原生支援的好處。 在這種情況下，若要改善所有Web應用程式的效能，請將 `cryptoj.jar`在WAR檔案外部。 例如，在 `<tomcat_installation_folder>/lib` 目錄。

* 64位元作業系統(例如Red Hat®或Windows的64位元版本)比32位元作業系統提供更好的效能。
