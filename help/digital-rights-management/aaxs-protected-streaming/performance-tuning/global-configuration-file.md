---
seo-title: 全局配置檔案
title: 全局配置檔案
uuid: 48c45f56-55c2-4526-b854-5552caf21541
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 全局配置檔案{#global-configuration-file}

對效能的最大影響是使用全域設定檔案flashaccess-global.xml中的設定。 這些設定包括 `<Caching>` 和 `<Logging>` 元素。

* `<Caching>` 元素 `<Caching>` 控制記憶體中配置檔案的快取。 元素 `<Caching>` 具有下列語法：

   ```
   <Caching refreshDelaySeconds="..." numTenants="..."/>
   ```

   * `refreshDelaySeconds` 控制伺服器檢查配置檔案更新的頻率。 低值對效能 `refreshDelaySeconds` 有負面影響，而高值可以改善效能。 有關的詳細信 `refreshDelaySeconds`息，請參[閱「更新配置檔案](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)」。

   * `numTenants` 指定租戶數。 低於租戶數的值可能會影響效能，因為對剩餘租戶的請求會導致快取遺失。 配置資料的快取丟失會對效能產生負面影響。 因此，Adobe建議您將此值設定為高於為伺服器設定的租戶數目，除非需考慮記憶體限制。

* `<Logging>` 元素 `<Logging>` 指定記錄級別以及記錄檔案的滾動頻率。 元素 `<Logging>` 具有下列語法：

   ```
   <Logging level="..." rollingFrequency=""/>
   ```

   * `level` 指定要記錄的消息。 值「DEBUG」會產生大量的記錄檔訊息，而且會對效能造成負面影響。 Adobe建議設定「WARN」以取得最佳效能。 但是，這種價值確實有可能丟失基本的運行時資訊，如許可證審核。 要以最低的效能影響保留有價值的日誌資訊，請使用「INFO」值。
   * `rollingFrequency` 指定記錄檔的滾 *動頻率*。 滾動是新日誌檔案變為活動日誌的過程，而先前的活動日誌檔案不再寫入並被視為滾動。 滾動間隔可設為「MINUTELY」、「HOURLY」、「TWIPE-DAILY」、「DAILY」、「WEEKLY」、「MONTHLY」或「NEVER」。

如需 *最佳化效能的其他秘訣，請參閱使用Adobe Access SDK for Protecting Content* 。
