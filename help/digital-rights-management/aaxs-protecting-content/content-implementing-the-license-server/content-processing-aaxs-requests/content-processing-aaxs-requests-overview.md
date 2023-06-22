---
title: 概觀
description: 概觀
copied-description: true
exl-id: d284b279-d261-4573-825d-919a551b3194
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# 概觀{#overview}

處理請求的一般方法是建立處理常式、剖析請求、設定回應資料或錯誤代碼，以及關閉處理常式。

處理單一請求/回應互動的基底類別為 `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. 的例項 `HandlerConfiguration` 類別用來初始化處理常式。 `HandlerConfiguration` 儲存伺服器組態資訊，包括傳輸認證、時間戳記公差、原則更新清單和撤銷清單。處理常式會讀取要求資料，並將要求剖析成的執行個體。 `RequestMessageBase`. 呼叫者可以檢查要求中的資訊，並決定是傳回錯誤還是成功回應(的子類別 `RequestMessageBase` 提供設定回應資料的方法)。

如果要求成功，請設定回應資料；否則會叫用 `RequestMessageBase.setErrorData()` 失敗時。 一律叫用「 」以結束實施 `close()` 方法(建議您 `close()` 在中呼叫 `finally` 區塊 `try` 陳述式)。 請參閱 `MessageHandlerBase` API參考檔案以取得如何叫用處理常式的範例。

>[!NOTE]
>
>應該傳送HTTP狀態碼200 （確定）以回應處理常式處理的所有要求。 如果因為伺服器錯誤而無法建立處理常式，伺服器可能會以其他狀態碼回應，例如500 （內部伺服器錯誤）。

使用者端使用封裝時指定的授權伺服器URL，作為傳送至授權伺服器之所有要求的基礎URL。 例如，如果將伺服器URL指定為「ht」<span></span>tps://licenseserver.com/path」，使用者端會將要求傳送至「ht」<span></span>tps://licenseserver.com/path/flashaccess/...」。 如需各種請求型別使用的特定路徑的詳細資訊，請參閱下列章節。 實作您的授權伺服器時，請確定伺服器會回應每種型別要求所需的路徑。

授權請求可包含驗證權杖。 如果使用使用者名稱/密碼驗證，請求可能包含 `AuthenticationToken` 產生者： `AuthenticationHandler`，且SDK會在核發授權之前確保權杖有效。
