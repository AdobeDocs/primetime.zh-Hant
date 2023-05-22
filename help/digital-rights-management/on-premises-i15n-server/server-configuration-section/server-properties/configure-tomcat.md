---
title: 配置Tomcat
description: 配置Tomcat
copied-description: true
exl-id: 766b66dd-6070-4b0d-a860-a426fca05e56
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 配置Tomcat{#configure-tomcat}

在個性化伺服器上，修改Tomcat的 [!DNL conf/server.xml] 檔案以在訪問日誌中包含其他資訊。 您可以將此資訊用於報告目的。

1. 查找 `AccessLogValve` 在 [!DNL server.xml] 並修改模式，如下所示：

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` 將記錄 `x-forwarded-for` 標題。 如果使用Apache反向代理將請求轉發到Tomcat伺服器，則此標頭將包含原始客戶端的IP地址，而 `%h` 記錄Apache伺服器的IP地址。 `%{request-id}r` 將記錄請求標識符，該標識符與個性化應用程式日誌中包含的請求ID相對應。

1. 編輯 [!DNL conf/server.xml] 並設定 `unpackwars` 屬性為false。

   對於個性化和密鑰生成伺服器，最好進行編輯 [!DNL conf/server.xml] 並設定 `unpackwars` 屬性 `false`。 否則，在更新WAR時，您可能也必須清除已打包的WAR資料夾。

>[!NOTE]
>
>將來的DRM客戶端將要求您啟用和配置可用於Tomcat的CORS（跨源資源共用）篩選器。 目前，沒有DRM客戶端具有此要求。
