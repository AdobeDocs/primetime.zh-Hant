---
title: Watched資料夾屬性
description: Watched資料夾屬性
copied-description: true
exl-id: e86518d4-2a16-45c7-aa96-189f677c3ee6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Watched資料夾屬性 {#watched-folder-properties}

每個watched資料夾都包含名為的檔案 [!DNL properties/watchfolder.properties]. 此檔案包含置入此資料夾之內容的封裝選項，包括要加密的內容以及要套用哪些原則。 對屬性檔案中的值所做的任何變更會在下次執行watched資料夾封裝程式時生效（您不需要重新啟動伺服器）。

如果封裝程式屬性檔案中有設定錯誤，封裝程式執行緒就會停止。 若要繼續watched資料夾封裝程式，請重新啟動伺服器。 如果watched資料夾屬性檔案中發生設定錯誤，則會從封裝程式處理的資料夾清單中暫時移除watched資料夾。 若要將watched資料夾新增回清單，請重新啟動伺服器或修改封裝程式屬性檔案。 如果在封裝特定檔案期間發生錯誤（例如，因為檔案已損毀），則會略過檔案，並處理資料夾中的其餘檔案。
