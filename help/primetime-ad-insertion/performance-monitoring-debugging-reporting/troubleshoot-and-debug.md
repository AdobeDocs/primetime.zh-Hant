---
title: 疑難排解與除錯
description: 疑難排解與除錯
copied-description: true
exl-id: 1fcacd29-627d-4536-a746-16ddcfc8bc34
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# 疑難排解與除錯{#troubleshooting-debugging}

PrimetimeAd Insertion提供工具來識別和診斷視訊傳送所有階段可能發生的問題，例如CDN傳送錯誤、創意錯誤或用戶端連接錯誤。

PrimetimeAd Insertion支援通過[BootstrapAPI參數](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true`或`ptdebug=AdCall`對引導URL進行詳細記錄。 記錄檔會同時輸出至HTTP回應標題和PrimetimeAd Insertion主控台。 此參數僅用於本地化測試，而非生產串流。 如需啟用詳細記錄時訊息類型的詳細資訊，請參閱詳細記錄中的[ptdebug記錄事件](verbose-logging.md#ptdebug-logging-events)。

PrimetimeAd Insertion也提供X-ADBE-AI-X1標題的所有要求效能除錯功能，可用來測量任何指定要求的效能和廣告插入。 無論是否啟用詳細記錄，此請求標題都可用。 如需詳細資訊，請參閱[詳細標題：X-ADBE-PTAI-X1](debugging-headers.md)。
