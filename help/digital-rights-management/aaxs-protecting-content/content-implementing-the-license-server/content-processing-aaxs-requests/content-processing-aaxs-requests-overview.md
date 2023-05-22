---
title: 概述
description: 概述
copied-description: true
exl-id: d284b279-d261-4573-825d-919a551b3194
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# 概述{#overview}

處理請求的一般方法是建立處理程式、分析請求、設定響應資料或錯誤代碼並關閉處理程式。

用於處理單個請求/響應交互的基類是 `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`。 實例 `HandlerConfiguration` 類用於初始化處理程式。 `HandlerConfiguration` 儲存伺服器配置資訊，包括傳輸憑據、時間戳容差、策略更新清單和吊銷清單。處理程式讀取請求資料並將請求解析到的實例中 `RequestMessageBase`。 調用方可以檢查請求中的資訊，並決定是返回錯誤還是成功響應（子類） `RequestMessageBase` 提供一種設定響應資料的方法)。

如果請求成功，請設定響應資料；否則調用 `RequestMessageBase.setErrorData()` 失敗。 始終通過調用 `close()` 方法(建議 `close()` 被叫來 `finally` 塊 `try` )。 查看 `MessageHandlerBase` API參考文檔，用於有關如何調用處理程式的示例。

>[!NOTE]
>
>應發送HTTP狀態代碼200(OK)以響應處理程式處理的所有請求。 如果由於伺服器錯誤而無法建立處理程式，則伺服器可能會使用其他狀態代碼(如500（內部伺服器錯誤）)進行響應。

客戶端將打包時指定的許可證伺服器URL用作發送到許可證伺服器的所有請求的基本URL。 例如，如果伺服器URL指定為「ht」<span></span>tps://licenseserver.com/path」，客戶端將向「ht」發送請求<span></span>tps://licenseserver.com/path/flashaccess/...」 有關每種請求類型所用特定路徑的詳細資訊，請參閱以下各節。 在實施許可證伺服器時，確保伺服器響應每種請求類型所需的路徑。

許可請求可以包含驗證令牌。 如果使用了用戶名/密碼身份驗證，則請求可能包含 `AuthenticationToken` 由 `AuthenticationHandler`，並且SDK將確保令牌在頒發許可證之前有效。
