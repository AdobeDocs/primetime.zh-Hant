---
description: 'null'
seo-description: 'null'
seo-title: 設定許可證伺服器資料庫
title: 設定許可證伺服器資料庫
uuid: aa6185f2-8e9d-4b65-971a-b7534d910580
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# 設定許可證伺服器資料庫{#set-up-the-license-server-database}

參考實施許可證伺服器需要一個資料庫來支援以下內容：

* 使用者驗證
* 使用模式示範業務規則
* 中繼資料轉換
* 網域支援

匿名獲取許可證不需要資料庫運行。

>[!NOTE]
>
>此過程僅適用於Microsoft Windows。 如需其他作業系統，請參閱作業系統的檔案或MySQL檔案。

要運行許可證伺服器，您需要安裝和配置MySQL:

1. 在DVD上，轉到資料夾 [!DNL Third Party\MySQL\Installer\5.1] 並啟動安裝程式。
1. 與MySQL安裝競爭。
1. 選擇 **[!UICONTROL Configure MySQL Server Now]** 以啟動配置嚮導。
1. 在第五個畫面之前，請使用預設設定，或為您的測試選取特定設定。
1. 在第五個螢幕上，選擇 **[!UICONTROL Online Transaction Processing (OLTP)]** 或 **[!UICONTROL Manual Setting]** 並輸入允許的最大連接數。
1. 記下根密碼。
1. 要重新安裝MySQL，如果需要稍後啟動伺服器，請完成以下步驟：
   1. 刪除系 *統驅動器：* 資料夾。

      此資料夾位於 [!DNL \Documents and Settings\All Users\Application Data\MySQL]。
   1. 刪除舊的MySQL安裝資料夾。

      例如， *系統驅動器：*，位於中 [!DNL \Program Files\MySQL\MySQL Server 5.1]。
1. 要安裝MySQL JDBC驅動程式5.1.7，請將DVD上 [!DNL mysql-connector-java-5.1.7-bin.jar] 的 [!DNL Third Party\MySQL\Installer\5.1] 資料夾中的檔案複製到 [!DNL ...\Tomcat6.0\lib] Tomcat伺服器上的目錄。

   >[!NOTE]
   >
   >MySQL JDBC驅動程式5.1.7可與Tomcat 6.0一起使用。不再支援舊版Tomcat。

