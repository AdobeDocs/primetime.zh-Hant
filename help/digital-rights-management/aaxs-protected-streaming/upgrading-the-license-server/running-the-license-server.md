---
description: 要升級運行「受保護流」的Adobe Access Server的伺服器，請將部署在應用程式伺服器上的flashaccessserver.war檔案替換為最新Adobe訪問附帶的檔案。 如果希望使用上述新配置選項，請更新伺服器的flashaccess-tenant.xml。 您還需要將jsafe.dll或libjsafe.so更新到最新Adobe訪問附帶的版本。
title: 運行Adobe Access Server以進行受保護的流式處理
exl-id: 02ba87c9-d4ec-4d39-926e-5d98b1858349
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 運行Adobe Access Server以進行受保護的流式處理{#running-the-adobe-access-server-for-protected-streaming}

要升級運行「受保護流」的Adobe Access Server的伺服器，請將部署在應用程式伺服器上的flashaccessserver.war檔案替換為最新Adobe訪問附帶的檔案。 如果希望使用上述新配置選項，請更新伺服器的flashaccess-tenant.xml。 您還需要將jsafe.dll或libjsafe.so更新到最新Adobe訪問附帶的版本。

在運行用於受保護流的Adobe Access Server之前，Adobe建議使用隨許可證伺服器提供的實用程式來驗證配置檔案是否有效。 有關詳細資訊，請參閱「」[配置驗證程式](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)。

要啟動Tomcat和許可證伺服器，請從Tomcat的bin目錄運行&quot;catalina.bat start&quot;或&quot;catalina.sh start&quot;。

伺服器啟動後，通過開啟來驗證是否已正確配置 *https:// license-server-host:port/flashaccessserver/tenant name/flashaccess/license/v1* 按鈕。 如果租戶配置已成功載入，則顯示確認消息。
