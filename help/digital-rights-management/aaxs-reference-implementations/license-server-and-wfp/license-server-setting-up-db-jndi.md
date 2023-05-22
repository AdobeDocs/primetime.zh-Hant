---
title: 設定資料庫並配置JNDI資料源
description: 設定資料庫並配置JNDI資料源
copied-description: true
exl-id: ed22f095-924b-4792-8a10-e7548fab2c3b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 設定資料庫並配置JNDI資料源 {#setting-up-the-database-and-configuring-the-jndi-datasource}

引用實施許可證伺服器需要資料庫來支援以下功能：

* 用戶驗證
* 使用模型演示業務規則
* 元資料轉換
* 域支援

匿名許可證獲取不需要資料庫運行。

>[!NOTE]
>
>本節中的說明是用於MicrosoftWindows平台。 有關其他作業系統，請參閱作業系統文檔或MySQL文檔。

要運行許可證伺服器，您需要安裝和配置MySQL 5.1.34:

1. 運行MySQL安裝程式(在DVD上的第三個Party\MySQL\Installer\5.1資料夾中找到)。
1. 在安裝過程結束時，檢查 **[!UICONTROL Configure MySQL Server Now]** 的子菜單。 使用預設設定或選擇特定設定以用於測試，但第5個螢幕上必須選擇 **[!UICONTROL Online Transaction Processing (OLTP)]** 或 **[!UICONTROL Manual Setting]** 並輸入允許的最大連接數。

1. 記下根密碼。
1. 如果需要重新安裝MySQL，請按照以下步驟來避免以後啟動伺服器時出現問題：

   * 刪除資料夾 *系統驅動器：* [!DNL \Documents and Settings\All Users\Application Data\MySQL]。

   * 刪除舊的MySQL安裝資料夾：比如說， *系統驅動器：* [!DNL \Program Files\MySQL\MySQL Server 5.1]。

接下來，您需要安裝MySQL JDBC驅動程式5.1.7。為此，請複製 [!DNL mysql-connector-java-5.1.7-bin.jar] (在 [!DNL Third Party\MySQL\Installer\5.1] 資料夾)到Tomcat Server lib目錄： [!DNL ...\Tomcat6.0\lib]。

>[!NOTE]
>
>MySQL JDBC驅動程式5.1.7可與Tomcat 6.0配合使用。不支援舊版本的Tomcat。

通過設定資料庫模式並用示例資料填充資料庫來設定示例資料庫。 為此，請執行以下步驟：

1. 轉到  **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]** 。
1. 在鍵入密碼後，執行以下SQL指令碼以添加用戶帳戶 `dbuser` 用於通過Web應用程式建立連接並建立資料庫模式（確保最後沒有「；」）。 按Enter鍵。):

   ```
       mysql> source “Reference Implementation\Server\dbscript\createsampledb.sql”
   ```

1. 編輯填充表中示例資料的指令碼，以包括用於測試目的的資料： [!DNL Reference Implementation\Server\dbscript\PopulateSampleDB.sql]。
1. 執行此指令碼以像您在步驟2中所做的那樣填充資料。

>[!NOTE]
>
>你第一次運行 [!DNL CreateSampleDB.sql] 指令碼將收到以下錯誤：

*錯誤1396(HY000):「dbuser」@「localhost」查詢OK的操作DROP USER失敗，影響0行（0.00秒）。*

您可以安全地忽略此錯誤。 這僅在您第一次運行此指令碼時發生。

此時，您需要配置資料庫連接池(DBCP)。 DBCP使用Jakarta-Commons資料庫連接池。 JNDI資料源測試DB配置為利用此應用程式伺服器連接池。 要將資料庫連接更改為指向不在localhost上的MySQL伺服器，請修改 [!DNL META-INF\context.xml] 檔案（指定許可證伺服器資料庫的位置、用戶名和密碼）位於 [!DNL flashaccess.war]，修改 [!DNL \Reference Implementation\Server\refimpl\WebContent\META-INF\context.xml] 並使用更新的檔案重新建立WAR檔案。 要更改這些參數中的任何一個，請編輯 [!DNL context.xml] 位於WebContent目錄中，並使用Ant指令碼重新建立WAR檔案。 要優化資料庫，請更改此檔案中的JNDI資料源設定。

如果在Eclipse中調試「參考實施」項目，則需要添加 `$CATALINA_HOME\lib\tomcat-dbcp.jar` 運行/調試配置。 如果運行 [!DNL flashaccess.war] 檔案。
