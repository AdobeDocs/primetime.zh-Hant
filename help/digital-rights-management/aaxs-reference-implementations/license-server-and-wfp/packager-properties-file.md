---
title: Packager屬性檔案
description: Packager屬性檔案
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# Packager屬性檔案{#packager-properties-file}

使用[!DNL flashaccess-refimpl-packager.properties]檔案來設定參考實作的Watched Folder Packager元件。 請至少務必設定授權伺服器URL、授權伺服器憑證、封裝程式憑證和金鑰保護選項。 此檔案也包含每個受監視資料夾(packager.watchfolder.source)的位置。 `n`)。對此屬性檔案中的值所做的任何更改將在下次運行監視資料夾打包器時生效（不需要重新啟動伺服器）。 但是，如果打包器中存在配置錯誤，則watched資料夾打包器線程將退出，並且需要重新啟動伺服器以重新啟動打包器線程。
