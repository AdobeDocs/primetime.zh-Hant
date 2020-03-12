---
description: 'null'
seo-description: 'null'
seo-title: 配置許可證伺服器資料庫
title: 配置許可證伺服器資料庫
uuid: 6d34e849-1616-46bd-ad18-4f98e6c45af7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 配置許可證伺服器資料庫{#configure-the-license-server-database}

要通過設定資料庫模式並用示例資料填充資料庫來配置示例資料庫，請執行以下操作：

1. 開啟MySQL命令行。

   **在Windows上——按一** 下 **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]**

   **在Linux等** -鍵 `MySQL`入。

1. 執行以下SQL指令碼：

   mysql>源&quot; `"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`&quot;

   此指令碼添加用戶帳戶 `dbuser`，通過Web應用程式建立連接，並建立資料庫模式。

   >[!NOTE]
   >
   >請確定指令碼結尾 `;`沒有分號()。

1. 編輯填 `PopulateSampleDB.sql` 入表格中範例資料的指令碼，以包含您測試的資料。

   此指令碼位於資料夾 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\` 中。
1. 執行指 [!DNL PopulateSampleDB] 令碼以填入資料，如同您在步驟2中所做的一樣。

   >[!NOTE] {class=&quot;- topic/note &quot;}
   >
   >第一次運行指令碼時，會發 [!DNL CreateSampleDB.sql] 生以下錯誤：

   您可以安全地忽略此錯誤。 只有在您第一次執行此指令碼時才會發生。

您需要配置使用Jakarta-Commons Database Connection Pool的資料庫連接池(DBCP)。 JNDI資料源TestDB配置為利用此應用程式伺服器連接池。 要將資料庫連接更改為指向不在localhost上的MySQL伺服器，請修改以下檔案之一：

* 該 [!DNL META-INF\context.xml] 檔案，指定檔案中許可證伺服器資料庫的位置、用戶名和密 [!DNL flashaccess.war] 碼。

* 檔 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml` 案。

並使用更新的檔案重新建立WAR檔案。

要更改這些參數中的任一參數，請編 [!DNL context.xml] 輯目錄中的 [!DNL WebContent] 檔案，然後使用Ant指令碼重新建立WAR檔案。 要調整資料庫，請更改此檔案中的JNDI資料源設定。

如果您在Eclipse中除錯「參考實作」專案，請新增至 `$CATALINA_HOME\lib\tomcat-dbcp.jar` 您的執行／除錯設定。

>[!NOTE]
>
>如果在獨立 [!DNL flashaccess.war] 的Tomcat 6.0伺服器上運行檔案，則不需要此步驟。

