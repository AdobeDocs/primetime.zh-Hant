---
description: 本主題說明與效能相關的考量事項。 全域設定檔中任何名為flashaccess-global.xml的設定都會影響效能。
seo-description: 本主題說明與效能相關的考量事項。 全域設定檔中任何名為flashaccess-global.xml的設定都會影響效能。
seo-title: 全局配置檔案
title: 全局配置檔案
uuid: 254925b5-d441-4a35-ad6f-f99db5de7591
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# 效能調整 {#performance-tuning}

本主題說明與效能相關的考量事項。 全域設定檔中任何名為flashaccess-global.xml的設定都會影響效能。

## 全局配置檔案 {#global-configuration-file}

配置檔案包含下列設定元素：

* `<Caching>` 元素 `<Caching>` 控制記憶體中配置檔案的快取。 元素 `<Caching>` 支援下列語法：

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` 控制伺服器檢查配置檔案更新的頻率。 負面值低會影 `refreshDelaySeconds` 響效能，但值高則會改善效能。

   有關 *的詳細資訊* ，請參閱更新配置檔案 `refreshDelaySeconds`。

* `numTenants` 指定租戶數。 低於租戶數的值會影響效能，因為對剩餘租戶的請求會導致快取遺失。 任何配置資料的快取丟失都會對效能產生負面影響。 因此，建議您將此值設定為高於為伺服器配置的租戶數，除非您需要考慮記憶體限制。

* `<Logging>` 元 `<Logging>` 素指定記錄級別和記錄日誌檔案的頻率。 元素 `<Logging>` 支援下列語法：

   ```
   <Logging level="..." rollingFrequency="..."/>
   ```

* `<level>`  指 `level` 定日誌消息。 值會產生 `DEBUG` 許多記錄訊息，這可能會對效能造成負面影響。 建議您套用設定，以取得最 `WARN` 佳效能。 但是，此值可能會遺失必要的執行階段資訊，例如授權稽核。 如果要以最低的效能影響保存日誌資訊，則需要應用值 `INFO`。

* `<rollingFrequency>`  指 `rollingFrequency` 定日誌檔案的滾 *動頻率*。 *`Rolling`* 是將任何新日誌檔案指定為活動日誌的進程。 因此，以前活動的日誌檔案將不再被修改並被考慮 *`rolled`*。 您可以將滾動間隔設 `MINUTELY`置為、 `HOURLY`、 `TWICE-DAILY`、 `DAILY`、 `WEEKLY``MONTHLY`或 `NEVER`。

如需 *如何最佳化效能的秘訣* ，請參閱使用Adobe Primetime DRM SDK以保護內容。