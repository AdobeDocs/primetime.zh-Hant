---
title: 故障排除和調試
description: 故障排除和調試
copied-description: true
exl-id: 1fcacd29-627d-4536-a746-16ddcfc8bc34
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# 故障排除和調試 {#troubleshooting-debugging}

黃金時段Ad Insertion提供工具，用於識別和診斷視頻交付的所有階段中可能發生的問題，如CDN交付錯誤、創意錯誤或客戶端連接錯誤。

黃金時段Ad Insertion支援通過 [BootstrapAPI參數](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true` 或 `ptdebug=AdCall` 到引導URL。 日誌將輸出到HTTP響應頭和黃金時段Ad Insertion控制台。 此參數僅用於本地化測試，而不用於生產流。 有關啟用詳細記錄時消息類型的詳細資訊，請參見 [ptdebug日誌記錄事件詳細記錄](verbose-logging.md#ptdebug-logging-events)。

黃金時段Ad Insertion還使用X-ADBE-AI-X1報頭為所有請求提供效能調試，該報頭可用於測量任何給定請求的效能和廣告插入。 無論是否啟用詳細記錄，此請求標頭都可用。 有關詳細資訊，請參見 [詳細標頭：X-ADBE-PTAI-X1](debugging-headers.md)。
