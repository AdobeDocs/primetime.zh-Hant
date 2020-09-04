---
description: Adobe Primetime DRM Server for Protected Streaming應用程式產生的記錄檔位於LicenseServer.LogRoot所指定的目錄中。
seo-description: Adobe Primetime DRM Server for Protected Streaming應用程式產生的記錄檔位於LicenseServer.LogRoot所指定的目錄中。
seo-title: 日誌檔案
title: 日誌檔案
uuid: 4498fe60-65af-4f99-8f9b-e85013d0c9e9
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# 日誌檔案{#log-files}

Adobe Primetime DRM Server for Protected Streaming應用程式產生的記錄檔位於LicenseServer.LogRoot所指定的目錄中。

>[!NOTE]
>
>如果當前日誌檔案在伺服器運行時被刪除或移動，則不能重新建立日誌檔案。 因此，某些日誌資訊可能會被刪除。

## 日誌目錄結構 {#section_F490A483D60145ADBC21038914C39203}

日誌目錄的結構化是為了便於使用。 日誌目錄具有以下結構：

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

全域記錄檔 `flashaccess-global.log`位於 *LicenseServer.LogRoot中*。 日誌可包括Adobe Primetime DRM Java SDK或日誌消息在伺服器初始化期間可能生成的日誌消息。

## 分區日誌檔案 {#section_5660137CD6AA40519E72A4315534846B}

分區日誌文 `flashaccess-partition.log`件位於目 `<LicenseServer.LogRoot>/flashaccesserver` 錄中。 它包含在處理授權要求期間產生的記錄訊息。

## 租用戶記錄檔 {#section_F0257CC0831647F18A746B4F02E3E910}

每個租用戶的租用戶日 `flashaccess-tenant.log`志檔案位於 `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`。 租用戶記錄包含稽核資訊，說明為此租用戶產生的每個授權。
