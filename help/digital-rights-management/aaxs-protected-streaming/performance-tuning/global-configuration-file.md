---
title: 全域組態檔
description: 全域組態檔
copied-description: true
exl-id: 109e6e5b-4bb5-43dc-b11e-50799a346a28
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# 全域組態檔{#global-configuration-file}

對效能的最大影響是使用全域組態檔flashaccess-global.xml中的設定。 這些設定包括 `<Caching>` 和 `<Logging>` 元素。

* `<Caching>` 此 `<Caching>` element控制記憶體中組態檔的快取。 此 `<Caching>` 元素具有下列語法：

   ```
   <Caching refreshDelaySeconds="..." numTenants="..."/>
   ```

   * `refreshDelaySeconds` 控制伺服器檢查組態檔更新的頻率。 以下專案的低值 `refreshDelaySeconds` 會對效能造成負面影響，而較高的值可以改善效能。 如需詳細資訊，請參閱 `refreshDelaySeconds`，請參閱「[更新組態檔](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)「。

   * `numTenants` 指定租使用者的數量。 低於租使用者數的值可能會影響效能，因為對其他租使用者的請求會導致快取遺漏。 設定資料的快取遺漏對效能有負面影響。 因此，Adobe建議您將此值設定為高於為伺服器設定的租使用者數量，除非有記憶體限制需要考量。

* `<Logging>` 此 `<Logging>` element會指定記錄層級以及記錄檔的捲動頻率。 此 `<Logging>` 元素具有下列語法：

   ```
   <Logging level="..." rollingFrequency=""/>
   ```

   * `level` 指定要記錄的訊息。 「DEBUG」值會產生許多記錄訊息，並可能對效能造成負面影響。 Adobe建議將「WARN」設定為最佳效能。 但是，這個值可能會遺失必要的執行階段資訊，例如授權稽核。 若要以最低的效能影響保留有價值的記錄資訊，請使用「INFO」值。
   * `rollingFrequency` 指定記錄檔的頻率 *已滾動*. 滾動是新記錄檔變成使用中記錄檔的過程，而先前使用的記錄檔不再寫入，且會視為滾動。 滾動間隔可設為「分鐘」、「每小時」、「每日兩次」、「每日」、「每週」、「每月」或「從不」。

另請參閱 *使用Adobe存取SDK保護內容* 以取得效能最佳化的其他秘訣。
