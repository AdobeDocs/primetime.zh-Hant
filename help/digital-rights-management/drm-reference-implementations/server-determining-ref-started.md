---
title: 檢查授權伺服器是否正確啟動
description: 檢查授權伺服器是否正確啟動
copied-description: true
exl-id: 05995a75-9468-4237-9091-a07606297772
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# 檢查授權伺服器是否正確啟動 {#check-whether-the-license-server-started-properly}

有數種方式可判斷您的Reference Implementation License Server是否已正確啟動。 一種方式是檢視 [!DNL catalina.log] 記錄，但這可能不夠，因為授權伺服器會記錄到自己的記錄檔。
1. 檢查您的 [!DNL AdobeFlashAccess.log] 檔案。

   這是Reference Implementation授權伺服器寫入記錄資訊的位置。 此記錄檔的位置由以下指示： [!DNL log4j.xml] 檔案，並可修改為指向任何位置。 依預設，記錄檔會複製到您執行 `catalina` Tomcat指令碼。
1. 前往下列URL，並確認顯示「License Server已正確設定」文字：
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
