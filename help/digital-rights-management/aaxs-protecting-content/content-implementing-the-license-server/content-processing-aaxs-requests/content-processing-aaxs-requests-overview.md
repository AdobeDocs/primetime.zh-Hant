---
title: 概觀
description: 概觀
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# 概觀{#overview}

處理要求的一般方法是建立處理常式、剖析要求、設定回應資料或錯誤碼，以及關閉處理常式。

用來處理單一請求/回應互動的基底類別是 `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. 的例項 `HandlerConfiguration` 類別是用來初始化處理常式。 `HandlerConfiguration` 儲存伺服器組態資訊，包括傳輸認證、時間戳記公差、原則更新清單及撤銷清單。處理常式會讀取要求資料，並將要求剖析成 `RequestMessageBase`. 呼叫者可以檢查要求中的資訊，並決定是否傳回錯誤或成功的回應(的子類別 `RequestMessageBase` 提供設定回應資料的方法)。

如果要求成功，請設定回應資料；否則，會叫用 `RequestMessageBase.setErrorData()` 失敗時。 一律透過叫用 `close()` 方法(建議您 `close()` 在中呼叫 `finally` 區塊 `try` 陳述式)。 請參閱 `MessageHandlerBase` API參考檔案，以取得如何叫用處理常式的範例。

>[!NOTE]
>
>應該傳送HTTP狀態碼200 （確定）以回應處理常式處理的所有要求。 如果因伺服器錯誤而無法建立處理常式，則伺服器可能會以其他狀態代碼回應，例如500 （內部伺服器錯誤）。

使用者端使用封裝時指定的授權伺服器URL，作為傳送給授權伺服器之所有要求的基底URL。 例如，如果將伺服器URL指定為「ht」<span></span>tps://licenseserver.com/path」，使用者端會將要求傳送至<span></span>tps://licenseserver.com/path/flashaccess/...」。 如需各種請求型別使用之特定路徑的詳細資訊，請參閱下列章節。 實作您的授權伺服器時，請確定伺服器會回應每種型別要求所需的路徑。

授權請求可包含驗證權杖。 如果使用使用者名稱/密碼驗證，請求可能包含 `AuthenticationToken` 產生者： `AuthenticationHandler`，且SDK會在核發授權之前確認權杖有效。
