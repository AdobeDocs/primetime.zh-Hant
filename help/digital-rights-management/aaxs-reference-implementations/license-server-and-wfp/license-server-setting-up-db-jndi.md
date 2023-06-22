---
title: 設定資料庫和設定JNDI資料來源
description: 設定資料庫和設定JNDI資料來源
copied-description: true
exl-id: ed22f095-924b-4792-8a10-e7548fab2c3b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 設定資料庫和設定JNDI資料來源 {#setting-up-the-database-and-configuring-the-jndi-datasource}

參考實作授權伺服器需要資料庫來支援下列功能：

* 使用者驗證
* 使用模式示範商業規則
* 中繼資料轉換
* 網域支援

匿名授權贏取不需要執行資料庫。

>[!NOTE]
>
>本節中的指示適用於Microsoft Windows平台。 若為其他作業系統，請參閱作業系統的說明檔案，或參閱MySQL說明檔案。

若要執行授權伺服器，您必須安裝並設定MySQL 5.1.34：

1. 執行MySQL安裝程式(位於DVD上的第三個Party\MySQL\Installer\5.1資料夾)。
1. 在安裝程式結束時，檢查 **[!UICONTROL Configure MySQL Server Now]** 以啟動設定精靈。 使用預設設定或選取測試用途的特定設定，但您必須在第5個畫面中選取的設定除外 **[!UICONTROL Online Transaction Processing (OLTP)]** 或 **[!UICONTROL Manual Setting]** 並輸入允許的最大連線數目。

1. 記下root密碼。
1. 如果您需要重新安裝MySQL，請依照下列步驟操作，以避免之後啟動伺服器時發生問題：

   * 刪除資料夾 *系統磁碟機：* [!DNL \Documents and Settings\All Users\Application Data\MySQL].

   * 刪除舊的MySQL安裝資料夾：例如， *系統磁碟機：* [!DNL \Program Files\MySQL\MySQL Server 5.1].

接下來，您需要安裝MySQL JDBC驅動程式5.1.7。若要這麼做，請複製 [!DNL mysql-connector-java-5.1.7-bin.jar] (可在 [!DNL Third Party\MySQL\Installer\5.1] 資料夾)至Tomcat Server lib目錄： [!DNL ...\Tomcat6.0\lib].

>[!NOTE]
>
>MySQL JDBC驅動程式5.1.7可搭配Tomcat 6.0使用。不支援舊版Tomcat。

設定資料庫結構描述並將範例資料填入資料庫中，以設定範例資料庫。 要執行此操作，請執行下列步驟：

1. 前往  **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]** .
1. 輸入密碼後，執行下列SQL指令碼以新增使用者帳戶 `dbuser` 用於透過Web應用程式建立連線並建立資料庫架構(請確保結尾沒有「；」。 只要按Enter即可。)：

   ```
       mysql> source “Reference Implementation\Server\dbscript\createsampledb.sql”
   ```

1. 編輯在表格中填入範例資料的指令碼，以包含用於測試的資料： [!DNL Reference Implementation\Server\dbscript\PopulateSampleDB.sql].
1. 執行此指令碼以像在步驟2中一樣填入資料。

>[!NOTE]
>
>第一次執行 [!DNL CreateSampleDB.sql] 指令碼：您會收到下列錯誤：

*錯誤1396 (HY000)： &#39;dbuser&#39;@&#39;localhost&#39;查詢正常的DROP USER作業失敗，0列受到影響（0.00秒）。*

您可以安全地忽略此錯誤。 這只會發生在您第一次執行此指令碼時。

此時您需要設定資料庫連線集區(DBCP)。 DBCP使用Jakarta-Commons資料庫連線集區。 JNDI資料來源TestDB已設定為使用此應用程式伺服器連線集區。 若要將資料庫連線變更為指向不在本機主機上的MySQL伺服器，請修改 [!DNL META-INF\context.xml] 檔案（指定授權伺服器資料庫的位置、使用者名稱和密碼），位於 [!DNL flashaccess.war]，或修改 [!DNL \Reference Implementation\Server\refimpl\WebContent\META-INF\context.xml] 並使用更新後的檔案重新建立WAR檔案。 若要變更這些引數，請編輯 [!DNL context.xml] 位在WebContent目錄中，並使用Ant指令碼重新建立WAR檔案。 若要調整資料庫，請變更此檔案中的JNDI資料來源設定值。

如果您在Eclipse中偵錯參考實作專案，您需要新增 `$CATALINA_HOME\lib\tomcat-dbcp.jar` 至您的執行/偵錯設定。 如果您執行 [!DNL flashaccess.war] 獨立Tomcat 6.0伺服器上的檔案。
