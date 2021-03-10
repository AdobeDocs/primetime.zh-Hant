---
title: 配置Tomcat
description: 配置Tomcat
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# 配置Tomcat{#configure-tomcat}

在個人化伺服器上，修改Tomcat的[!DNL conf/server.xml]檔案，以在訪問日誌中包含其他資訊。 您可將此資訊用於報告用途。

1. 找到[!DNL server.xml]中`AccessLogValve`的配置並修改模式，如下所示：

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` 將記錄標題的 `x-forwarded-for` 值。如果使用Apache反向代理將請求轉發到Tomcat伺服器，則此標頭將包含原始客戶機的IP地址，而`%h`則記錄Apache伺服器的IP地址。 `%{request-id}r` 將會記錄請求識別碼，此識別碼與個人化應用程式記錄中包含的請求ID相對應。

1. 編輯[!DNL conf/server.xml]，並將`unpackwars`屬性設為false。

   對於個性化和密鑰生成伺服器，最好編輯[!DNL conf/server.xml]並將`unpackwars`屬性設定為`false`。 否則，在更新WAR時，可能還需要清除未打包的WAR資料夾。

>[!NOTE]
>
>未來的DRM用戶端將要求您啟用並設定Tomcat可用的CORS（跨原始資源共用）篩選器。 目前，沒有DRM客戶端具有此要求。

