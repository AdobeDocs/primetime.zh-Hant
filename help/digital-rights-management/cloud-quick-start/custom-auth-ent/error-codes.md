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

如果在BEES檢查期間發生錯誤， `DRMErrorEvent` 將會傳回給使用者端。 您可以剖析此事件的屬性，以尋找有關失敗性質的詳細資訊。 下面列出了可能錯誤碼的子集。

| 錯誤 | 說明 |
|---|---|
| `3304:305` | Primetime Cloud DRM嘗試處理驗證/授權請求時出現一般授權錯誤。 通常與BEES問題無關。 如果持續遇到此錯誤，您應該將問題票證連同診斷資訊一起提交給Primetime Cloud DRM團隊。 |
| `3329:0` | 應用程式特定錯誤（來自BEES授權者）。 如果未傳回子錯誤代碼，錯誤文字會顯示問題的詳細資料。 例如，剖析回應時發生問題，或無法連線BEES伺服器。 |
| `3329:<HTTP error code>` | BEES伺服器已發出200以外的HTTP回應。 HTTP錯誤碼會在子錯誤碼欄位中傳回給使用者端。 這可能表示設定問題或BEES伺服器中斷。 |
| `3329:<x>` | BEES伺服器不允許授權要求。 子錯誤碼和錯誤文字由BEES伺服器在JSON回應的 `error` 和 `errorText` 屬性。 此類回應不應視為錯誤，而應視為來自BEES伺服器的定期拒絕回應。 |
