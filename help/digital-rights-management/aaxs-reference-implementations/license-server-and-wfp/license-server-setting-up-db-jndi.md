---
title: 設定資料庫和配置JNDI資料源
description: 設定資料庫和配置JNDI資料源
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---


# 設定資料庫並配置JNDI資料源{#setting-up-the-database-and-configuring-the-jndi-datasource}

參考實作授權伺服器需要有資料庫來支援下列功能：

* 使用者驗證
* 使用模式示範業務規則
* 中繼資料轉換
* 網域支援

匿名授權獲取不需要執行資料庫。

>[!NOTE]
>
>本節中的說明適用於Microsoft Windows平台。 如需其他作業系統，請參閱作業系統的檔案或MySQL檔案。

要運行許可證伺服器，您需要安裝和配置MySQL 5.1.34:

1. 運行MySQL安裝程式(位於DVD的「第三個Party\MySQL\Installer\5.1資料夾」中)。
1. 在安裝過程結束時，選中&#x200B;**[!UICONTROL Configure MySQL Server Now]**&#x200B;以啟動配置嚮導。 請使用預設設定或選擇特定設定以供測試之用，但第5個畫面上您必須選取&#x200B;**[!UICONTROL Online Transaction Processing (OLTP)]**&#x200B;或&#x200B;**[!UICONTROL Manual Setting]**&#x200B;並輸入允許的連線數上限。

1. 記下根密碼。
1. 如果需要重新安裝MySQL，請遵循下列步驟，以避免後續啟動伺服器時出現問題：

   * 刪除資料夾&#x200B;*系統驅動器：* [!DNL \Documents and Settings\All Users\Application Data\MySQL]。

   * 刪除舊的MySQL安裝資料夾：例如，*系統驅動器：* [!DNL \Program Files\MySQL\MySQL Server 5.1]。

接下來，您需要安裝MySQL JDBC驅動程式5.1.7。要執行此操作，請將[!DNL mysql-connector-java-5.1.7-bin.jar]（位於DVD上的[!DNL Third Party\MySQL\Installer\5.1]資料夾中）複製到Tomcat Server lib目錄：[!DNL ...\Tomcat6.0\lib]。

>[!NOTE]
>
>MySQL JDBC驅動程式5.1.7可與Tomcat 6.0一起使用。不支援舊版Tomcat。

通過設定資料庫模式並用示例資料填充資料庫來設定示例資料庫。 若要這麼做，請執行下列步驟：

1. 前往&#x200B;**[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]**。
1. 在鍵入口令後，請執行以下SQL指令碼以添加通過Web應用程式建立連接的用戶帳戶`dbuser`並建立資料庫模式（請確保最後沒有&quot;;&quot;）。 只要按Enter鍵。):

   ```
       mysql> source “Reference Implementation\Server\dbscript\createsampledb.sql”
   ```

1. 編輯填入表格中範例資料的指令碼，以納入您測試的資料：[!DNL Reference Implementation\Server\dbscript\PopulateSampleDB.sql]。
1. 執行此指令碼以像在步驟2中那樣填充資料。

>[!NOTE]
>
>第一次運行[!DNL CreateSampleDB.sql]指令碼時，您將收到以下錯誤：

*錯誤1396(HY000):「dbuser」@「localhost」查詢確定的操作DROP USER失敗，0行受影響（0.00秒）。*

您可以安全地忽略此錯誤。 這只會在您第一次執行此指令碼時發生。

此時，您需要配置資料庫連接池(DBCP)。 DBCP使用Jakarta-Commons資料庫連接池。 JNDI資料源TestDB配置為利用此應用程式伺服器連接池。 要將資料庫連接更改為指向不在localhost上的MySQL伺服器，請修改位於[!DNL flashaccess.war]中的[!DNL META-INF\context.xml]檔案（該檔案指定許可證伺服器資料庫的位置、用戶名和密碼），或者修改[!DNL \Reference Implementation\Server\refimpl\WebContent\META-INF\context.xml]，然後使用更新的檔案重新建立WAR檔案。 要更改這些參數中的任何參數，請編輯位於WebContent目錄中的[!DNL context.xml] ，然後使用Ant指令碼重新建立WAR檔案。 要調整資料庫，請更改此檔案中的JNDI資料源設定。

如果您在Eclipse中對「參考實作」專案進行除錯，則需要將`$CATALINA_HOME\lib\tomcat-dbcp.jar`新增至您的執行／除錯設定。 如果在獨立的Tomcat 6.0伺服器上運行[!DNL flashaccess.war]檔案，則不需要此步驟。
