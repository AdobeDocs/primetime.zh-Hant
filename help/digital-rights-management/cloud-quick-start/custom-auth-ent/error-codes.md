---
title: BEES錯誤代碼
description: BEES錯誤代碼
copied-description: true
exl-id: 36c83ee9-7e28-442e-8076-691a1bd43a01
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# BEES錯誤代碼 {#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

如果在BEES檢查期間出錯， `DRMErrorEvent` 將返回給客戶。 您可以分析此事件的屬性以查找有關失敗性質的詳細資訊。 下面列出了可能的錯誤代碼的子集。

| 錯誤 | 說明 |
|---|---|
| `3304:305` | 試圖處理驗證/授權請求的Mighine Cloud DRM的常規授權錯誤。 通常與BEES問題不相關。 如果始終遇到此錯誤，您應將故障單連同診斷資訊提交給Mighine Cloud DRM團隊。 |
| `3329:0` | 應用程式特定錯誤（來自BEES授權程式）。 如果未返回子錯誤代碼，則錯誤文本將顯示問題的詳細資訊。 例如，分析響應時出現問題，或BEES伺服器無法訪問。 |
| `3329:<HTTP error code>` | BEES伺服器發出了200以外的HTTP響應。 HTTP錯誤代碼將在子錯誤代碼欄位中返回給客戶端。 這可能表示配置問題或BEES伺服器中斷。 |
| `3329:<x>` | BEES伺服器不允許許可請求。 子錯誤代碼和錯誤文本由JSON響應中的BEES伺服器指定 `error` 和 `errorText` 屬性。 此類響應不應被視為錯誤，而應視為來自BEES伺服器的常規拒絕響應。 |
