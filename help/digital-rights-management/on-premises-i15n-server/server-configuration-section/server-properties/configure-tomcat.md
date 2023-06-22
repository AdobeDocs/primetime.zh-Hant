---
title: 設定Tomcat
description: 設定Tomcat
copied-description: true
exl-id: 766b66dd-6070-4b0d-a860-a426fca05e56
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 設定Tomcat{#configure-tomcat}

在「個人化」伺服器上，修改Tomcat的 [!DNL conf/server.xml] 檔案，以在存取記錄中包含其他資訊。 您可以將此資訊用於報告目的。

1. 找出 `AccessLogValve` 在 [!DNL server.xml] 並修改模式，如下所示：

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` 將記錄以下專案的值： `x-forwarded-for` 標頭。 如果您使用Apache反向Proxy將請求轉送至Tomcat伺服器，此標頭將包含原始使用者端的IP位址，而 `%h` 記錄Apache伺服器的IP位址。 `%{request-id}r` 將記錄要求識別碼，此識別碼會對應至個人化應用程式記錄中包含的要求ID。

1. 編輯 [!DNL conf/server.xml] 並設定 `unpackwars` 屬性為false。

   對於「個人化」和「金鑰產生」伺服器而言，最好編輯一下 [!DNL conf/server.xml] 並設定 `unpackwars` 屬性至 `false`. 否則，當您更新WAR時，可能還必須清除解壓縮的WAR資料夾。

>[!NOTE]
>
>未來的DRM使用者端會要求您啟用並設定可用於Tomcat的CORS （跨原始資源共用）篩選器。 目前沒有任何DRM使用者端有此需求。
