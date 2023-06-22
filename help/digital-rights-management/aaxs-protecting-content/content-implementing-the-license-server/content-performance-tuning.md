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

使用下列提示來協助提高效能：

* 使用網路HSM比使用直接連線的HSM要慢得多。
* 為改善效能，您可以部署位於SDK「thirdparty/cryptoj」資料夾中的平台特定程式庫，選擇性地啟用密碼編譯作業的原生支援。 若要啟用原生支援，請將您平台的程式庫（適用於Windows的jsafe.dll或適用於Linux的libjsafe.so）新增至路徑。

   >[!NOTE]
   >
   >如果您在同一Tomcat執行個體中執行多個Web應用程式並擁有 `jsafe.dll` 在路徑上，只有第一個載入的Web應用程式才能載入 `jsafe.dll` 資料庫。 因此，只有第一個Web應用程式才能享受原生支援的好處。 在這種情況下，若要改善所有網頁應用程式的效能，請放置 `cryptoj.jar`在WAR檔案外部。 例如，在 `<tomcat_installation_folder>/lib` 目錄。

* 64位元作業系統(例如64位元版本的Red Hat®或Windows)比32位元作業系統提供更優異的效能。
