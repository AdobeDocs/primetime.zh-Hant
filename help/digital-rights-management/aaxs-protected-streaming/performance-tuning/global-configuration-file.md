---
title: 全局配置檔案
description: 全局配置檔案
copied-description: true
exl-id: 109e6e5b-4bb5-43dc-b11e-50799a346a28
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# 全局配置檔案{#global-configuration-file}

對效能的最大影響是使用全局配置檔案flashaccess-global.xml中的設定。 這些設定包括 `<Caching>` 和 `<Logging>` 元素。

* `<Caching>` 的 `<Caching>` 元素控制記憶體中配置檔案的快取。 的 `<Caching>` 元素具有以下語法：

   ```
   <Caching refreshDelaySeconds="..." numTenants="..."/>
   ```

   * `refreshDelaySeconds` 控制伺服器檢查配置檔案更新的頻率。 低值 `refreshDelaySeconds` 對效能產生負面影響，而價值越高，效能就越好。 有關 `refreshDelaySeconds`，請參閱「」[正在更新配置檔案](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)。

   * `numTenants` 指定租戶數。 低於租戶數量的值可能會影響效能，因為對剩餘租戶的請求會導致快取丟失。 配置資料的快取缺失會對效能產生負面影響。 因此，Adobe建議將此值設定得高於為伺服器配置的租戶數，除非需要考慮記憶體限制。

* `<Logging>` 的 `<Logging>` 元素指定日誌記錄級別和滾動日誌檔案的頻率。 的 `<Logging>` 元素具有以下語法：

   ```
   <Logging level="..." rollingFrequency=""/>
   ```

   * `level` 指定要記錄的消息。 值「DEBUG」會生成大量日誌消息，並會對效能產生負面影響。 Adobe建議設定「WARN」以獲得最佳效能。 但是，該值確實有可能丟失基本的運行時資訊，如許可證審核。 要保留對效能影響最小的重要日誌資訊，請使用「INFO」值。
   * `rollingFrequency` 指定日誌檔案的頻率 *卷*。 滾動是新日誌檔案成為活動日誌的過程，而以前活動的日誌檔案不再寫入並被視為滾動。 滾動間隔可以設定為「MINUTELY」、「HOURLY」、「TWIEX-DAILY」、「DAILY」、「WEEKLY」、「MONTHLY」或「NEVER」。

請參閱 *使用Adobe訪問SDK保護內容* 有關優化效能的其他提示。
