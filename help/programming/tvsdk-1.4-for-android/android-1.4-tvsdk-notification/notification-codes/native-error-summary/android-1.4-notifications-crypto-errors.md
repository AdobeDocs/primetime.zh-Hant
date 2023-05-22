---
description: Adobe視頻引擎的加密模組在NATIVE_ERROR元資料對象中返回這些通知。
title: NATIVE_ERROR加密值
exl-id: 9f34d893-d5b1-4bfe-a590-27deccb6d08d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 8%

---

# 本機錯誤(_E):加密值{#native-error-crypto-values}

Adobe視頻引擎的加密模組在NATIVE_ERROR元資料對象中返回這些通知。

| NATIVE_ERROR_CODE元資料鍵的值 | NATIVE_ERROR_NAME元資料鍵的值 | 意義 |
|---|---|---|
| 300 | `CRYPTO_ALGORITHM_NOT_SUPPORTED` | 不支援使用的算法。 |
| 301 | `CRYPTO_ERROR_CORRUPTED_DATA` | 資料已損壞。 |
| 302 | `CRYPTO_ERROR_BUFFER_TOO_SMALL` | 緩衝區太小。 |
| 303 | `CRYPTO_ERROR_BAD_CERTIFICATE` | 證書錯誤。 |
| 304 | `CRYPTO_ERROR_DIGEST_UPDATE` | 摘要更新。 |
| 305 | `CRYPTO_ERROR_DIGEST_FINISH` | 摘要完成。 |
| 306 | `CRYPTO_ERROR_BAD_PARAMETER` | 參數錯誤。 |
