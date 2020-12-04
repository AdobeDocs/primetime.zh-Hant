---
description: 若要升級執行Adobe Access Server的受保護串流伺服器，請將部署在應用程式伺服器上的flashaccessserver.war檔案取代為最新Adobe Access隨附的檔案。 如果您想要使用上述新的設定選項，請更新您伺服器的flashaccess-tenant.xml。 您也需要將jsafe.dll或libjsafe.so更新至最新Adobe Access隨附的版本。
seo-description: 若要升級執行Adobe Access Server的受保護串流伺服器，請將部署在應用程式伺服器上的flashaccessserver.war檔案取代為最新Adobe Access隨附的檔案。 如果您想要使用上述新的設定選項，請更新您伺服器的flashaccess-tenant.xml。 您也需要將jsafe.dll或libjsafe.so更新至最新Adobe Access隨附的版本。
seo-title: 執行Adobe Access Server以進行受保護的串流
title: 執行Adobe Access Server以進行受保護的串流
uuid: 3819500d-ad2f-49eb-8aa4-e50a55461608
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# 執行Adobe Access Server for Protected Streaming{#running-the-adobe-access-server-for-protected-streaming}

若要升級執行Adobe Access Server的受保護串流伺服器，請將部署在應用程式伺服器上的flashaccessserver.war檔案取代為最新Adobe Access隨附的檔案。 如果您想要使用上述新的設定選項，請更新您伺服器的flashaccess-tenant.xml。 您也需要將jsafe.dll或libjsafe.so更新至最新Adobe Access隨附的版本。

在執行Adobe Access Server for Protected Streaming之前，Adobe建議您使用授權伺服器隨附的公用程式來驗證組態檔是否有效。 如需詳細資訊，請參閱「[Configuration Validator](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)」。

要啟動Tomcat和許可證伺服器，請從Tomcat的bin目錄運行&quot;catalina.bat start&quot;或&quot;catalina.sh start&quot;。

啟動伺服器後，請在瀏覽器視窗中開啟&#x200B;*https:// license-server-host:port/flashaccessserver/tenant-name/flashaccess/license/v1*，以確認其已正確設定。 如果租用戶設定已成功載入，則會顯示確認訊息。
