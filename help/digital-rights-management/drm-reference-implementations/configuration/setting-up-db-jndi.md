---
title: 設定授權伺服器資料庫
description: 設定授權伺服器資料庫
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# 設定授權伺服器資料庫{#set-up-the-license-server-database}

參考實作授權伺服器需要資料庫來支援下列專案：

* 使用者驗證
* 使用模式示範商業規則
* 中繼資料轉換
* 網域支援

匿名授權贏取不需要資料庫必須執行。

>[!NOTE]
>
>此程式僅適用於Microsoft Windows。 若為其他作業系統，請參閱作業系統相關檔案，或參閱MySQL檔案。

若要執行授權伺服器，您必須安裝並設定MySQL：

1. 在DVD上，前往 [!DNL Third Party\MySQL\Installer\5.1] 資料夾並啟動安裝程式。
1. 完成MySQL安裝。
1. 選取 **[!UICONTROL Configure MySQL Server Now]** 以啟動設定精靈。
1. 在第五個畫面之前，請使用預設設定或選取測試的特定設定。
1. 在第五個畫面中，選取 **[!UICONTROL Online Transaction Processing (OLTP)]** 或 **[!UICONTROL Manual Setting]** 並輸入允許的連線數目上限。
1. 記下根密碼。
1. 若要重新安裝MySQL，如果您需要稍後啟動伺服器，請完成下列步驟：
   1. 刪除 *系統磁碟機：* 資料夾。

      此資料夾位於 [!DNL \Documents and Settings\All Users\Application Data\MySQL].
   1. 刪除舊的MySQL安裝資料夾。

      例如， *系統磁碟機：*，此區域位於 [!DNL \Program Files\MySQL\MySQL Server 5.1].
1. 若要安裝MySQL JDBC驅動程式5.1.7，請複製 [!DNL mysql-connector-java-5.1.7-bin.jar] 中的檔案 [!DNL Third Party\MySQL\Installer\5.1] DVD上的資料夾 [!DNL ...\Tomcat6.0\lib] 目錄。

   >[!NOTE]
   >
   >MySQL JDBC驅動程式5.1.7可搭配Tomcat 6.0使用。不再支援舊版Tomcat。
