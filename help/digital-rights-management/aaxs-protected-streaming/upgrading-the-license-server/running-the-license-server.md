---
description: 若要升級執行Adobe Access Server for Protected Streaming的伺服器，請將部署在應用程式伺服器上的flashaccessserver.war檔案，取代為包含最新Adobe存取權的檔案。 如果您想要使用上述新設定選項，請更新伺服器的flashaccess-tenant.xml。 您也需要將jsafe.dll或libjsafe.so更新為包含於最新Adobe存取中的版本。
title: 執行適用於受保護串流的Adobe Access Server
exl-id: 02ba87c9-d4ec-4d39-926e-5d98b1858349
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 執行適用於受保護串流的Adobe Access Server{#running-the-adobe-access-server-for-protected-streaming}

若要升級執行Adobe Access Server for Protected Streaming的伺服器，請將部署在應用程式伺服器上的flashaccessserver.war檔案，取代為包含最新Adobe存取權的檔案。 如果您想要使用上述新設定選項，請更新伺服器的flashaccess-tenant.xml。 您也需要將jsafe.dll或libjsafe.so更新為包含於最新Adobe存取中的版本。

在執行Adobe Access Server for Protected Streaming之前，Adobe建議您使用授權伺服器隨附的公用程式來驗證設定檔是否有效。 如需詳細資訊，請參閱「[設定驗證器](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)「。

若要啟動Tomcat和授權伺服器，請從Tomcat的bin目錄執行「catalina.bat start」或「catalina.sh start」。

伺服器啟動後，請開啟「 」，確認伺服器已正確設定 *https:// license-server-host：port/flashaccessserver/tenant-name/flashaccess/license/v1* 在瀏覽器視窗中。 如果租使用者設定已成功載入，則會顯示確認訊息。
