---
title: 效能調整
description: 效能調整
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# 效能調整{#performance-tuning}

使用下列提示協助提高效能：

* 使用網路HSM比使用直接連接的HSM要慢得多。
* 為提升效能，您可選擇部署位於SDK「協力廠商／密碼」資料夾中的平台特定程式庫，以啟用加密作業的原生支援。 若要啟用原生支援，請將平台的程式庫（Windows專用的jsafe.dll,Linux專用的libjsafe.so）新增至路徑。

   >[!NOTE]
   >
   >如果在同一個Tomcat實例中運行多個Web應用程式並且路徑上具有`jsafe.dll` ，則只有載入的第一個Web應用程式能夠載入`jsafe.dll`庫。 因此，只有第一個Web應用程式才能享有原生支援的優點。 在這種情況下，要提高所有Web應用程式的效能，請將`cryptoj.jar`置於WAR檔案之外。 例如，在`<tomcat_installation_folder>/lib`目錄中。

* 64位元作業系統（例如64位元版本的Red Hat®或Windows）可提供比32位元作業系統更佳的效能。

