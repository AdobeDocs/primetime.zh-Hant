---
title: 封裝程式屬性檔案
description: 封裝程式屬性檔案
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# 封裝程式屬性檔案 {#packager-properties-file}

使用 [!DNL flashaccess-refimpl-packager.properties] 檔案來設定參考實作的Watched資料夾封裝程式元件。 至少請務必設定授權伺服器URL、授權伺服器憑證、封裝者認證和金鑰保護選項。 此檔案也包含每個watched資料夾(packager.watchfolder.source)的位置。 `n`). 此屬性檔案中值的任何變更將在下次執行watched資料夾封裝程式時生效（不需要重新啟動伺服器）。 但是，如果封裝程式發生設定錯誤，watched資料夾封裝程式執行緒將會結束，而且伺服器必須重新啟動才能重新啟動封裝程式執行緒。
