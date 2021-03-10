---
title: 檢查許可證伺服器是否正確啟動
description: 檢查許可證伺服器是否正確啟動
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# 檢查許可證伺服器是否正確啟動{#check-whether-the-license-server-started-properly}

有幾種方法可判斷您的「參考實作授權伺服器」是否已正確啟動。 一種方法是檢查[!DNL catalina.log]日誌，但這可能不夠，因為許可證伺服器會登錄到其自己的日誌檔案。
1. 檢查[!DNL AdobeFlashAccess.log]檔案。

   Reference Implementation授權伺服器會在此處寫入記錄資訊。 此日誌檔案的位置由[!DNL log4j.xml]檔案指示，可修改為指向任何位置。 預設情況下，日誌檔案將複製到運行`catalina` Tomcat指令碼的工作目錄。
1. 前往下列URL，並確認文字「License Server is setup correctly（授權伺服器已正確設定）」已顯示：
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
