---
title: Watched資料夾屬性
description: Watched資料夾屬性
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# 監視資料夾屬性{#watched-folder-properties}

每個受監視的資料夾都包含一個名為[!DNL properties/watchfolder.properties]的檔案。 此檔案包含放置在此資料夾中的內容的打包選項，包括要加密的內容以及要應用的策略。 對屬性檔案中的值所做的任何更改將在下次運行監視資料夾包時生效（您不需要重新啟動伺服器）。

如果打包器屬性檔案中存在配置錯誤，則打包器線程將停止。 要繼續監視的資料夾打包器，請重新啟動伺服器。 如果監視資料夾屬性檔案中存在配置錯誤，則會暫時從打包員處理的資料夾清單中刪除監視資料夾。 要將監視資料夾添加回清單，請重新啟動伺服器或修改包器屬性檔案。 如果在打包特定檔案時（例如，由於檔案損壞）發生錯誤，則會跳過該檔案，並處理資料夾中的其餘檔案。
