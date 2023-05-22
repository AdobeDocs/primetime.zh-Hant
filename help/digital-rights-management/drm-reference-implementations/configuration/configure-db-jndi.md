---
title: 配置許可證伺服器資料庫
description: 配置許可證伺服器資料庫
copied-description: true
exl-id: 1d5d988e-d22a-4405-8f39-1763f1f65094
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 配置許可證伺服器資料庫{#configure-the-license-server-database}

要通過設定資料庫架構和用示例資料填充資料庫來配置示例資料庫：

1. 開啟MySQL命令行。

   **在Windows上 —** 按一下  **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]**

   **在Linux上，等等**  — 類型 `MySQL`。

1. 執行以下SQL指令碼：

   mysql>源&quot; `"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`&quot;

   此指令碼添加用戶帳戶 `dbuser`，通過Web應用程式建立連接，並建立資料庫模式。

   >[!NOTE]
   >
   >確保沒有分號( `;`)。

1. 編輯 `PopulateSampleDB.sql` 指令碼，用於填充表中的示例資料以包含測試資料。

   此指令碼位於 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\` 的子菜單。
1. 執行 [!DNL PopulateSampleDB] 指令碼，以按您在步驟2中所做的操作填充資料。

   >[!NOTE]
   >
   >你第一次運行 [!DNL CreateSampleDB.sql] 指令碼出現以下錯誤：

   您可以安全地忽略此錯誤。 它僅在您第一次運行此指令碼時發生。

您需要配置使用Jakarta-Commons資料庫連接池的資料庫連接池(DBCP)。 JNDI資料源測試DB配置為利用此應用程式伺服器連接池。 要將資料庫連接更改為指向不在localhost上的MySQL伺服器，請修改以下檔案之一：

* 的 [!DNL META-INF\context.xml] 檔案，它指定許可證伺服器資料庫中位於 [!DNL flashaccess.war] 的子菜單。

* 的 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml` 的子菜單。

並使用更新的檔案重新建立WAR檔案。

要更改這些參數中的任何一個，請編輯 [!DNL context.xml] 檔案 [!DNL WebContent] 目錄，然後使用Ant指令碼重新建立WAR檔案。 要優化資料庫，請更改此檔案中的JNDI資料源設定。

如果在Eclipse中調試「參考實施」項目，請添加 `$CATALINA_HOME\lib\tomcat-dbcp.jar` 運行/調試配置。

>[!NOTE]
>
>如果運行 [!DNL flashaccess.war] 檔案，不需要此步驟。
