---
description: Adobe視訊引擎的加密模組會在NATIVE_ERROR中繼資料物件中傳回這些通知。
title: NATIVE_ERROR加密值
exl-id: 9f34d893-d5b1-4bfe-a590-27deccb6d08d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 8%

---

# NATIVE_ERROR：加密值{#native-error-crypto-values}

Adobe視訊引擎的加密模組會在NATIVE_ERROR中繼資料物件中傳回這些通知。

| NATIVE_ERROR_CODE中繼資料索引鍵的值 | NATIVE_ERROR_NAME中繼資料索引鍵的值 | 含義 |
|---|---|---|
| 300 | `CRYPTO_ALGORITHM_NOT_SUPPORTED` | 不支援正在使用的演演算法。 |
| 301 | `CRYPTO_ERROR_CORRUPTED_DATA` | 資料已損毀。 |
| 302 | `CRYPTO_ERROR_BUFFER_TOO_SMALL` | 緩衝區太小。 |
| 303 | `CRYPTO_ERROR_BAD_CERTIFICATE` | 錯誤的憑證。 |
| 304 | `CRYPTO_ERROR_DIGEST_UPDATE` | 摘要更新。 |
| 305 | `CRYPTO_ERROR_DIGEST_FINISH` | 摘要完成。 |
| 306 | `CRYPTO_ERROR_BAD_PARAMETER` | 引數錯誤。 |
