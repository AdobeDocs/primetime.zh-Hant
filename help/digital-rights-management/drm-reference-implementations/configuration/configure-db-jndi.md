---
title: 配置許可證伺服器資料庫
description: 配置許可證伺服器資料庫
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# 配置許可證伺服器資料庫{#configure-the-license-server-database}

要通過設定資料庫模式並用示例資料填充資料庫來配置示例資料庫，請執行以下操作：

1. 開啟MySQL命令行。

   **在Windows上-** 按一下  **[!UICONTROL Window's Start Menu]** >  **[!UICONTROL MySQL]** >  **[!UICONTROL MySQL Server 5.1]** >  **[!UICONTROL MySQL Command Line Client]**

   **在Linux等** -鍵 `MySQL`入。

1. 執行以下SQL指令碼：

   mysql>源&quot;`"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`&quot;

   此指令碼添加用戶帳戶`dbuser`，通過Web應用程式建立連接，並建立資料庫模式。

   >[!NOTE]
   >
   >確保指令碼末尾沒有分號(`;`)。

1. 編輯`PopulateSampleDB.sql`指令碼，該指令碼會填入表格中的範例資料，以包含您測試的資料。

   此指令碼位於`[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\`資料夾中。
1. 執行[!DNL PopulateSampleDB]指令碼，以填入步驟2中的資料。

   >[!NOTE]
   >
   >第一次運行[!DNL CreateSampleDB.sql]指令碼時，會出現以下錯誤：

   您可以安全地忽略此錯誤。 只有在您第一次執行此指令碼時才會發生。

您需要配置使用Jakarta-Commons Database Connection Pool的資料庫連接池(DBCP)。 JNDI資料源TestDB配置為利用此應用程式伺服器連接池。 要將資料庫連接更改為指向不在localhost上的MySQL伺服器，請修改以下檔案之一：

* [!DNL META-INF\context.xml]檔案，它指定許可證伺服器資料庫在[!DNL flashaccess.war]檔案中的位置、用戶名和口令。

* `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml`檔案。

並使用更新的檔案重新建立WAR檔案。

要更改這些參數中的任何參數，請編輯[!DNL WebContent]目錄中的[!DNL context.xml]檔案，然後使用Ant指令碼重新建立WAR檔案。 要調整資料庫，請更改此檔案中的JNDI資料源設定。

如果您在Eclipse中除錯「參考實作」專案，請將`$CATALINA_HOME\lib\tomcat-dbcp.jar`新增至您的執行／除錯設定。

>[!NOTE]
>
>如果在獨立的Tomcat 6.0伺服器上運行[!DNL flashaccess.war]檔案，則不需要此步驟。

