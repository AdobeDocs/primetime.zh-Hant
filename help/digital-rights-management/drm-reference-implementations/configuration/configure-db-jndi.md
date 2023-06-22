---
title: 設定授權伺服器資料庫
description: 設定授權伺服器資料庫
copied-description: true
exl-id: 1d5d988e-d22a-4405-8f39-1763f1f65094
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 設定授權伺服器資料庫{#configure-the-license-server-database}

若要設定範例資料庫，方法是設定資料庫綱要並填入範例資料的資料庫：

1. 開啟MySQL命令列。

   **在Windows上 —** 按一下  **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]**

   **在Linux等**  — 型別 `MySQL`.

1. 執行下列SQL指令碼：

   mysql>來源» `"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`&quot;

   此指令碼會新增使用者帳戶 `dbuser`，會透過Web應用程式建立連線，並建立資料庫架構。

   >[!NOTE]
   >
   >確定沒有分號( `;`)的後面。

1. 編輯 `PopulateSampleDB.sql` 將範例資料填入表格中的指令碼，以包含用於測試的資料。

   此指令碼位於 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\` 資料夾。
1. 執行 [!DNL PopulateSampleDB] 指令碼，可像在步驟2中一樣填入資料。

   >[!NOTE]
   >
   >第一次執行 [!DNL CreateSampleDB.sql] 指令碼發生下列錯誤：

   您可以安全地忽略此錯誤。 它只會在您第一次執行此指令碼時發生。

您需要設定使用Jakarta-Commons資料庫連線集區的「資料庫連線集區」(DBCP)。 JNDI資料來源TestDB已設定為使用此應用程式伺服器連線集區。 若要將資料庫連線變更為指向不在localhost上的MySQL伺服器，請修改下列其中一個檔案：

* 此 [!DNL META-INF\context.xml] 檔案，指定許可證伺服器資料庫的位置、使用者名稱和密碼，該資料庫位於 [!DNL flashaccess.war] 檔案。

* 此 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml` 檔案。

並使用更新後的檔案重新建立WAR檔案。

若要變更這些引數，請編輯 [!DNL context.xml] 中的檔案 [!DNL WebContent] 目錄並使用Ant指令碼來重新建立WAR檔案。 若要調整資料庫，請變更此檔案中的JNDI資料來源設定值。

如果您在Eclipse中偵錯參考實作專案，請新增 `$CATALINA_HOME\lib\tomcat-dbcp.jar` 至您的執行/偵錯設定。

>[!NOTE]
>
>如果您執行 [!DNL flashaccess.war] 獨立Tomcat 6.0伺服器上的檔案，不需要執行此步驟。
