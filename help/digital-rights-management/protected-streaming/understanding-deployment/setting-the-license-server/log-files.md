---
description: 由Adobe PrimetimeDRM伺服器為受保護的流式處理應用程式生成的日誌檔案位於LicenseServer.LogRoot指定的目錄中。
title: 日誌檔案
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# 日誌檔案{#log-files}

由Adobe PrimetimeDRM伺服器為受保護的流式處理應用程式生成的日誌檔案位於LicenseServer.LogRoot指定的目錄中。

>[!NOTE]
>
>如果當前日誌檔案在伺服器運行時被刪除或移動，則不能重新建立日誌檔案。 因此，可能會刪除一些日誌資訊。

## 日誌目錄結構 {#section_F490A483D60145ADBC21038914C39203}

日誌目錄是為便於使用而構建的。 日誌目錄具有以下結構：

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

## 全局日誌檔案 {#section_1CFA90748142439C9F3BE380969539DA}

全局日誌檔案， `flashaccess-global.log`，位於 *LicenseServer.LogRoot*。 該日誌可包括Adobe PrimetimeDRM Java SDK或日誌消息在伺服器初始化期間可能已生成的日誌消息。

## 分區日誌檔案 {#section_5660137CD6AA40519E72A4315534846B}

分區日誌檔案， `flashaccess-partition.log`的 `<LicenseServer.LogRoot>/flashaccesserver` 的子菜單。 它包括在處理許可證請求期間生成的日誌消息。

## 租戶日誌檔案 {#section_F0257CC0831647F18A746B4F02E3E910}

每個租戶的租戶日誌檔案， `flashaccess-tenant.log`，位於 `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`。 租戶日誌包括描述為此租戶生成的每個許可證的審核資訊。
