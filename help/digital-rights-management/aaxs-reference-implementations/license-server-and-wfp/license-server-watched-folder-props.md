---
title: 監視的資料夾屬性
description: 監視的資料夾屬性
copied-description: true
exl-id: e86518d4-2a16-45c7-aa96-189f677c3ee6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# 監視的資料夾屬性 {#watched-folder-properties}

每個受監視資料夾都包含一個名為 [!DNL properties/watchfolder.properties]。 此檔案包含放置在此資料夾中的內容的打包選項，包括要加密的內容和要應用的策略。 對屬性檔案中的值所做的任何更改將在下次運行受監視資料夾打包程式時生效（您不需要重新啟動伺服器）。

如果打包器屬性檔案中存在配置錯誤，打包器線程將停止。 要恢復受監視的資料夾打包程式，請重新啟動伺服器。 如果受監視的資料夾屬性檔案中存在配置錯誤，則從打包程式處理的資料夾清單中臨時刪除受監視的資料夾。 要將監視的資料夾重新添加到清單，請重新啟動伺服器或修改打包器屬性檔案。 如果在打包特定檔案時出錯（例如，因為檔案已損壞），則會跳過該檔案並處理資料夾中的其餘檔案。
