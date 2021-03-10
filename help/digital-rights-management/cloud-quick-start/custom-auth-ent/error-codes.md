---
title: BEES錯誤代碼
description: BEES錯誤代碼
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# BEES錯誤代碼{#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

如果在BEES檢查期間發生錯誤，`DRMErrorEvent`將返回給客戶端。 您可以剖析此事件的屬性，以尋找有關失敗性質的詳細資訊。 以下列出可能的錯誤代碼子集。

| 錯誤 | 說明 |
|---|---|
| `3304:305` | 嘗試處理驗證／授權要求的Primetime Cloud DRM的一般授權錯誤。 通常與BEES問題無關。 如果一致地遇到此錯誤，您應將故障單連同診斷資訊一併提交給Primetime Cloud DRM團隊。 |
| `3329:0` | 應用程式特定錯誤（來自BEES授權者）。 如果未傳回子錯誤碼，錯誤文字將會顯示問題的詳細資訊。 例如，在解析響應時發生問題，或無法訪問BEES伺服器。 |
| `3329:<HTTP error code>` | BEES伺服器發出200以外的HTTP回應。 HTTP錯誤碼會在子錯誤碼欄位中傳回給用戶端。 這可能表示配置問題或BEES伺服器中斷。 |
| `3329:<x>` | BEES伺服器不允許授權要求。 BEES伺服器會在JSON回應的`error`和`errorText`屬性中指定子錯誤碼和錯誤文字。 此類回應不應被視為錯誤，而應視為來自BEES伺服器的定期拒絕回應。 |