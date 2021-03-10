---
description: 本主題說明與效能相關的考量事項。 全域設定檔中任何名為flashaccess-global.xml的設定都會影響效能。
title: 全局配置檔案
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# 效能調整{#performance-tuning}

本主題說明與效能相關的考量事項。 全域設定檔中任何名為flashaccess-global.xml的設定都會影響效能。

## 全局配置檔案{#global-configuration-file}

配置檔案包含下列設定元素：

* `<Caching>` 該元 `<Caching>` 素控制記憶體中配置檔案的快取。`<Caching>`元素支援下列語法：

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` 控制伺服器檢查配置檔案更新的頻率。`refreshDelaySeconds`的低值會對效能產生負面影響，而較高的值則會改善效能。

   有關`refreshDelaySeconds`的詳細資訊，請參閱&#x200B;*更新配置檔案*。

* `numTenants` 指定租戶數。低於租戶數的值會影響效能，因為對剩餘租戶的請求會導致快取遺失。 任何配置資料的快取丟失都會對效能產生負面影響。 因此，建議您將此值設定為高於為伺服器配置的租戶數，除非您需要考慮記憶體限制。

* `<Logging>` 元 `<Logging>` 素指定記錄層級和記錄檔案的頻率。`<Logging>`元素支援下列語法：

   ```
   <Logging level="..." rollingFrequency="..."/>
   ```

* `<level>`  `level` 指定日誌的消息。值`DEBUG`會產生許多日誌消息，這可能對效能產生負面影響。 建議您套用`WARN`的設定，以取得最佳效能。 但是，此值可能會遺失必要的執行階段資訊，例如授權稽核。 如果希望以最低的效能影響保存日誌資訊，則需要應用`INFO`值。

* `<rollingFrequency>`  `rollingFrequency` 指定記錄檔的滾 *動頻率*。*`Rolling`* 是將任何新日誌檔案指定為活動日誌的進程。因此，以前活動的日誌檔案不再被修改，因此被視為&#x200B;*`rolled`*。 您可以將滾動間隔設定為`MINUTELY`、`HOURLY`、`TWICE-DAILY`、`DAILY`、`WEEKLY`、`MONTHLY`或`NEVER`。

如需如何最佳化效能的秘訣，請參閱&#x200B;*使用Adobe PrimetimeDRM SDK保護內容*。