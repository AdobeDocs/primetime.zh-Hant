---
title: 全局配置檔案
description: 全局配置檔案
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# 全局配置檔案{#global-configuration-file}

對效能的最大影響是使用全域設定檔案flashaccess-global.xml中的設定。 這些設定包括`<Caching>`和`<Logging>`元素。

* `<Caching>` 該元 `<Caching>` 素控制記憶體中配置檔案的快取。`<Caching>`元素具有下列語法：

   ```
   <Caching refreshDelaySeconds="..." numTenants="..."/>
   ```

   * `refreshDelaySeconds` 控制伺服器檢查配置檔案更新的頻率。`refreshDelaySeconds`的低值會對效能產生負面影響，而較高的值則會改善效能。 有關`refreshDelaySeconds`的詳細資訊，請參閱「[更新配置檔案](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)」。

   * `numTenants` 指定租戶數。低於租戶數的值可能會影響效能，因為對剩餘租戶的請求會導致快取遺失。 配置資料的快取丟失會對效能產生負面影響。 因此，Adobe建議您將此值設定為高於為伺服器配置的租戶數，除非需要考慮記憶體限制。

* `<Logging>` 元素 `<Logging>` 指定記錄級別以及記錄檔案的滾動頻率。`<Logging>`元素具有下列語法：

   ```
   <Logging level="..." rollingFrequency=""/>
   ```

   * `level` 指定要記錄的消息。值「DEBUG」會產生大量的記錄檔訊息，而且會對效能造成負面影響。 Adobe建議設定&quot;WARN&quot;以獲得最佳效能。 但是，這種價值確實有可能丟失基本的運行時資訊，如許可證審核。 要以最低的效能影響保留有價值的日誌資訊，請使用「INFO」值。
   * `rollingFrequency` 指定記錄檔的滾 *動頻率*。滾動是新日誌檔案變為活動日誌的過程，而先前的活動日誌檔案不再寫入並被視為滾動。 滾動間隔可設為「MINUTELY」、「HOURLY」、「TWIPE-DAILY」、「DAILY」、「WEEKLY」、「MONTHLY」或「NEVER」。

如需最佳化效能的其他秘訣，請參閱&#x200B;*使用Adobe存取SDK保護內容。*
