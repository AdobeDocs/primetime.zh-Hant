---
title: 打包器屬性檔案
description: 打包器屬性檔案
copied-description: true
exl-id: 7d78576b-fd77-460d-92d9-c2e69e37006e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# 打包器屬性檔案 {#packager-properties-file}

使用 [!DNL flashaccess-refimpl-packager.properties] 檔案，以配置引用實現的「監視資料夾包」元件。 至少要設定許可證伺服器URL、許可證伺服器證書、打包器憑據和密鑰保護選項。 此檔案還包含每個受監視資料夾(packager.watchfolder.source)的位置。 `n`). 對此屬性檔案中的值所做的任何更改將在下次運行受監視資料夾打包程式時生效（不需要重新啟動伺服器）。 但是，如果打包器中存在配置錯誤，則會退出受監視的資料夾打包器線程，並且需要重新啟動伺服器以重新啟動打包器線程。
