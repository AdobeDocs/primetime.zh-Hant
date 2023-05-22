---
title: 檢查許可證伺服器是否已正確啟動
description: 檢查許可證伺服器是否已正確啟動
copied-description: true
exl-id: 05995a75-9468-4237-9091-a07606297772
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# 檢查許可證伺服器是否已正確啟動 {#check-whether-the-license-server-started-properly}

有幾種方法可確定您的參考實施許可證伺服器是否已正確啟動。 一種方法是 [!DNL catalina.log] 日誌，但這可能不夠，因為許可證伺服器會登錄到其自己的日誌檔案。
1. 檢查 [!DNL AdobeFlashAccess.log] 的子菜單。

   這是參考實施許可證伺服器寫入日誌資訊的位置。 此日誌檔案的位置由 [!DNL log4j.xml] 可修改為指向任何位置。 預設情況下，日誌檔案將複製到運行日誌的工作目錄 `catalina` Tomcat指令碼。
1. 轉到以下URL，並驗證是否顯示了「License Server is setup correctly（許可證伺服器設定正確）」文本：
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
