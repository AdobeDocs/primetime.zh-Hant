---
description: 由Adobe PrimetimeDRM Server for Protected Streaming應用程式生成的日誌檔案位於LicenseServer.LogRoot指定的目錄中。
title: 日誌檔案
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# 日誌檔案{#log-files}

由Adobe PrimetimeDRM Server for Protected Streaming應用程式生成的日誌檔案位於LicenseServer.LogRoot指定的目錄中。

>[!NOTE]
>
>如果當前日誌檔案在伺服器運行時被刪除或移動，則不能重新建立日誌檔案。 因此，某些日誌資訊可能會被刪除。

## 日誌目錄結構{#section_F490A483D60145ADBC21038914C39203}

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

## 全局日誌檔案{#section_1CFA90748142439C9F3BE380969539DA}

全局日誌檔案`flashaccess-global.log`位於&#x200B;*LicenseServer.LogRoot*&#x200B;中。 日誌可以包括在伺服器初始化期間Adobe PrimetimeDRM Java SDK或日誌消息可能已生成的日誌消息。

## 分區日誌檔案{#section_5660137CD6AA40519E72A4315534846B}

分區日誌檔案`flashaccess-partition.log`位於`<LicenseServer.LogRoot>/flashaccesserver`目錄中。 它包含在處理授權要求期間產生的記錄訊息。

## 租用戶日誌檔案{#section_F0257CC0831647F18A746B4F02E3E910}

每個租用戶的租用戶日誌檔案`flashaccess-tenant.log`位於`<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`中。 租用戶記錄包含稽核資訊，說明為此租用戶產生的每個授權。
