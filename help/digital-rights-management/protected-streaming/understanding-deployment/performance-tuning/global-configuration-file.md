---
description: 本主題介紹與效能相關的注意事項。 全局配置檔案中名為flashaccess-global.xml的任何設定都會影響效能。
title: 全局配置檔案
exl-id: 52d41476-d352-4c02-8af6-25c0fe6bcaa7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 效能調整 {#performance-tuning}

本主題介紹與效能相關的注意事項。 全局配置檔案中名為flashaccess-global.xml的任何設定都會影響效能。

## 全局配置檔案 {#global-configuration-file}

配置檔案包括以下設定元素：

* `<Caching>` 的 `<Caching>` 元素控制記憶體中配置檔案的快取。 的 `<Caching>` 元素支援以下語法：

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` 控制伺服器檢查配置檔案更新的頻率。 低值 `refreshDelaySeconds` 負面影響效能，而更高的值可改善效能。

   請參閱 *正在更新配置檔案* 的 `refreshDelaySeconds`。

* `numTenants` 指定租戶數。 低於租戶數量的值會影響效能，因為對剩餘租戶的請求會導致快取丟失。 任何配置資料的快取未命中都會對效能產生負面影響。 因此，建議將此值設定得高於為伺服器配置的租戶數量，除非需要考慮記憶體限制。

* `<Logging>` 的 `<Logging>` 元素指定日誌記錄級別和滾動日誌檔案的頻率。 的 `<Logging>` 元素支援以下語法：

   ```
   <Logging level="..." rollingFrequency="..."/>
   ```

* `<level>`  `level` 為日誌指定消息。 值 `DEBUG` 生成許多日誌消息，這可能對效能產生負面影響。 建議您應用 `WARN` 獲得最佳效能。 但是，此值可能會導致丟失基本的運行時資訊，如許可證審核。 如果希望以最小的效能影響保存日誌資訊，則需要應用 `INFO`。

* `<rollingFrequency>`  `rollingFrequency` 指定日誌檔案的頻率 *卷*。 *`Rolling`* 是將任何新日誌檔案指定為活動日誌的進程。 因此，不能再修改以前活動的日誌檔案，因此將其視為 *`rolled`*。 可以將滾動間隔設定為 `MINUTELY`。 `HOURLY`。 `TWICE-DAILY`。 `DAILY`。 `WEEKLY`。 `MONTHLY`或 `NEVER`。

請參閱 *使用Adobe PrimetimeDRM SDK保護內容* 有關如何優化效能的提示。
