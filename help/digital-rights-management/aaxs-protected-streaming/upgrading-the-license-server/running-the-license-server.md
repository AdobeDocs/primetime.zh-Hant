---
description: 若要升級執行Adobe Access Server for Protected Streaming的伺服器，請將應用程式伺服器上部署的flashaccessserver.war檔案取代為包含最新Adobe存取權的檔案。 如果您想要使用上述的新設定選項，請更新伺服器的flashaccess-tenant.xml。 您也需要將jsafe.dll或libjsafe.so更新為包含於最新Adobe存取中的版本。
title: 執行適用於受保護串流的Adobe Access Server
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 執行適用於受保護串流的Adobe Access Server{#running-the-adobe-access-server-for-protected-streaming}

若要升級執行Adobe Access Server for Protected Streaming的伺服器，請將應用程式伺服器上部署的flashaccessserver.war檔案取代為包含最新Adobe存取權的檔案。 如果您想要使用上述的新設定選項，請更新伺服器的flashaccess-tenant.xml。 您也需要將jsafe.dll或libjsafe.so更新為包含於最新Adobe存取中的版本。

在執行Adobe Access Server for Protected Streaming之前，Adobe建議您使用授權伺服器隨附的公用程式來驗證設定檔是否有效。 如需詳細資訊，請參閱&quot;[設定驗證器](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)「。

若要啟動Tomcat和授權伺服器，請從Tomcat的bin目錄執行「catalina.bat start」或「catalina.sh start」。

伺服器啟動後，請開啟 *https:// license-server-host：port/flashaccessserver/tenant-name/flashaccess/license/v1* 在瀏覽器視窗中。 如果租使用者設定已成功載入，則會顯示確認訊息。
