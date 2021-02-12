---
title: 疑難排解與除錯
description: null
translation-type: tm+mt
source-git-commit: 242b5a2875ebc0e0020296ce9489dd54438b5ad0
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# 疑難排解與除錯{#troubleshooting-debugging}

Primetime廣告插入提供工具，可識別和診斷視訊傳送所有階段可能發生的問題，例如CDN傳送錯誤、廣告創意錯誤或用戶端連接錯誤。

Primetime廣告插入支援通過[引導API參數](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true`或`ptdebug=AdCall`對引導URL進行詳細記錄。 記錄檔會輸出至HTTP回應標題和Primetime廣告插入主控台。 此參數僅用於本地化測試，而非生產串流。 如需啟用詳細記錄時訊息類型的詳細資訊，請參閱詳細記錄中的[ptdebug記錄事件](verbose-logging.md#ptdebug-logging-events)。

Primetime廣告插入功能也提供X-ADBE-AI-X1標題對所有請求的效能除錯功能，可用來測量任何指定請求的效能和廣告插入。 無論是否啟用詳細記錄，此請求標題都可用。 如需詳細資訊，請參閱[詳細標題：X-ADBE-PTAI-X1](debugging-headers.md)。
