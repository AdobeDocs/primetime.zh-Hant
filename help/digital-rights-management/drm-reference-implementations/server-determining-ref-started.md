---
description: 'null'
seo-description: 'null'
seo-title: 檢查許可證伺服器是否正確啟動
title: 檢查許可證伺服器是否正確啟動
uuid: a6a034c9-b3c4-4e26-b901-d2c132c00c52
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# 檢查許可證伺服器是否正確啟動 {#check-whether-the-license-server-started-properly}

有幾種方法可判斷您的「參考實作授權伺服器」是否已正確啟動。 一種方法是檢查日 [!DNL catalina.log] 志，但這可能不夠，因為許可證伺服器會登錄到自己的日誌檔案。
1. 檢查您的 [!DNL AdobeFlashAccess.log] 檔案。

   Reference Implementation授權伺服器會在此處寫入記錄資訊。 此日誌檔案的位置由檔案指示， [!DNL log4j.xml] 可修改為指向任何位置。 預設情況下，日誌檔案將複製到運行 `catalina` Tomcat指令碼的工作目錄。
1. 前往下列URL，並確認文字「License Server is setup correctly（授權伺服器已正確設定）」已顯示：
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
