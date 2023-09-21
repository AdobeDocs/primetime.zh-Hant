---
title: 疑難排解和偵錯
description: 疑難排解和偵錯
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# 疑難排解和偵錯 {#troubleshooting-debugging}

PrimetimeAd Insertion提供的工具可識別和診斷視訊傳送所有階段可能發生的問題，例如CDN傳送錯誤、廣告創意錯誤或使用者端連線錯誤。

PrimetimeAd Insertion透過支援詳細記錄 [BootstrapAPI引數](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true` 或 `ptdebug=AdCall` 至啟動程式URL。 記錄檔會輸出至HTTP回應標頭和PrimetimeAd Insertion主控台。 此引數僅適用於本地化測試，不適用於生產串流。 如需啟用詳細記錄時訊息型別的詳細資訊，請參閱 [ptdebug記錄詳細記錄中的事件](verbose-logging.md#ptdebug-logging-events).

PrimetimeAd Insertion也可對所有具有X-ADOBE-AI-X1標題的請求提供效能偵錯，這可用於測量任何指定請求上的效能和廣告插入。 無論是否啟用詳細記錄功能，都可以使用此請求標頭。 如需詳細資訊，請參閱 [詳細資訊標題： X-ADBE-PTAI-X1](debugging-headers.md).
