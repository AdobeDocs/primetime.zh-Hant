---
seo-title: 效能調整
title: 效能調整
uuid: bb5321a0-48ef-49cb-aaf0-00d7ab9562fe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 效能調整{#performance-tuning}

使用下列提示協助提高效能：

* 使用網路HSM比使用直接連接的HSM要慢得多。
* 為提升效能，您可選擇部署位於SDK「協力廠商／密碼」資料夾中的平台特定程式庫，以啟用加密作業的原生支援。 若要啟用原生支援，請將平台的程式庫（Windows專用的jsafe.dll,Linux專用的libjsafe.so）新增至路徑。

   >[!NOTE] {class=&quot;- topic/note &quot;}
   >
   >如果在同一Tomcat實例中運行多個Web應用 `jsafe.dll` 程式並且路徑上有，則只有載入的第一個Web應用程式能夠載入庫 `jsafe.dll` 。 因此，只有第一個Web應用程式才能享有原生支援的優點。 在這種情況下，為了改善所有Web應用程式的效能，請 `cryptoj.jar`置於WAR檔案之外。 例如，在目錄 `<tomcat_installation_folder>/lib` 中。

* 64位元作業系統（例如64位元版本的Red Hat®或Windows）可提供比32位元作業系統更佳的效能。

