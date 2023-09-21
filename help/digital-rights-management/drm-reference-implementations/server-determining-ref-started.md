---
title: 檢查授權伺服器是否正確啟動
description: 檢查授權伺服器是否正確啟動
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# 檢查授權伺服器是否正確啟動 {#check-whether-the-license-server-started-properly}

有數種方式可判斷您的參考實作授權伺服器是否已正確啟動。 一種方式是檢視 [!DNL catalina.log] 記錄，但這可能還不夠，因為授權伺服器會記錄到自己的記錄檔。
1. 檢查您的 [!DNL AdobeFlashAccess.log] 檔案。

   這是「參考實作」授權伺服器寫入記錄資訊的位置。 此記錄檔的位置由您的 [!DNL log4j.xml] 和檔案，可修改為指向任何位置。 依預設，記錄檔會複製到您執行的工作目錄 `catalina` Tomcat指令碼。
1. 前往下列URL，並確認顯示「License Server已正確設定」文字：
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
