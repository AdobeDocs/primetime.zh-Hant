---
title: 封裝程式屬性檔案
description: 封裝程式屬性檔案
copied-description: true
exl-id: 7d78576b-fd77-460d-92d9-c2e69e37006e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# 封裝程式屬性檔案 {#packager-properties-file}

使用 [!DNL flashaccess-refimpl-packager.properties] 檔案來設定參考實作的Watched Folder Packager元件。 至少請務必設定授權伺服器URL、授權伺服器憑證、封裝者認證和金鑰保護選項。 此檔案也包含每個監看資料夾(packager.watchfolder.source)的位置。 `n`). 此屬性檔案中值的任何變更將在下次執行watched資料夾封裝程式時生效（不需要重新啟動伺服器）。 不過，如果封裝程式發生設定錯誤，就會結束watched資料夾封裝程式執行緒，而且伺服器必須重新啟動才能重新啟動封裝程式執行緒。
