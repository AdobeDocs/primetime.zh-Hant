---
title: 許可證伺服器屬性檔案
description: 許可證伺服器屬性檔案
copied-description: true
exl-id: 07cd9866-c29b-476e-a63f-9c5272ccd678
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# 許可證伺服器屬性檔案{#license-server-properties-file}

許可證伺服器引用在 [!DNL flashaccess-refimpl.properties] 的子菜單。 您可以直接參考該檔案以瞭解有關特定值的詳細資訊以及有關每個屬性的使用資訊。 於2014年12月16日， [!DNL resources] 引用實現的目錄( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`)。

**憑據**  — 屬性檔案包括Adobe您所發出的憑據的位置設定。 您可以在 [!DNL .pfx] 檔案，或為HSM上儲存的憑據提供別名和密碼。 您至少需要配置與傳輸憑據和許可證伺服器憑據相關的屬性。 指定憑據檔案相對於在中指定的目錄的位置 `config.resourcesDirectory` 屬性。

**Flash媒體Rights Management伺服器** - `flashaccess-refimpl.properties` 檔案還包括幾個與打包內容相關的屬性。 這些屬性僅用於Flash媒體Rights Management伺服器1.x元資料轉換。 修改此屬性檔案中的值後，如果更改生效，請重新啟動許可證伺服器。
