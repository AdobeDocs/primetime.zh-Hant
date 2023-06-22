---
description: Adobe Primetime DRM伺服器Protected Streaming應用程式產生的記錄檔位於LicenseServer.LogRoot指定的目錄中。
title: 記錄檔
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# 記錄檔{#log-files}

Adobe Primetime DRM伺服器Protected Streaming應用程式產生的記錄檔位於LicenseServer.LogRoot指定的目錄中。

>[!NOTE]
>
>如果伺服器執行時刪除或移動目前的記錄檔，則可能無法重新建立記錄檔。 因此，某些記錄資訊可能會被刪除。

## 記錄目錄結構 {#section_F490A483D60145ADBC21038914C39203}

記錄目錄的結構化便於使用。 記錄目錄具有下列結構：

```
<i class="+ topic ph hi-d="" i "="">
 LicenseServer.LogRoot/ 
 flashaccess-global.log 
     flashaccessserver/ 
         flashaccess-partition.log 
         tenants/ 
             
 <i class="+ topic ph hi-d="" i "="">
  tenantname/ 
                  flashaccess-tenant.log
 </i class="+ topic>
</i class="+ topic>
```

## 全域記錄檔 {#section_1CFA90748142439C9F3BE380969539DA}

全域記錄檔， `flashaccess-global.log`，位於 *LicenseServer.LogRoot*. 記錄檔可能包含Adobe Primetime DRM Java SDK的記錄檔訊息，或是在伺服器初始化期間產生的記錄檔訊息。

## 資料分割記錄檔 {#section_5660137CD6AA40519E72A4315534846B}

分割記錄檔， `flashaccess-partition.log`，位於 `<LicenseServer.LogRoot>/flashaccesserver` 目錄。 它包含在處理授權請求期間產生的記錄訊息。

## 租使用者記錄檔 {#section_F0257CC0831647F18A746B4F02E3E910}

每個租使用者的租使用者記錄檔， `flashaccess-tenant.log`，位於 `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`. 租使用者記錄檔包含稽核資訊，說明為此租使用者產生的每個授權。
