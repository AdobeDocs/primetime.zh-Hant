---
seo-title: 概觀
title: 概觀
uuid: 870c32f5-1119-4fec-abed-25e51dd1ebe3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 概觀{#overview}

處理請求的一般方法是建立處理常式、剖析請求、設定回應資料或錯誤碼，並關閉處理常式。

用於處理單個請求／響應交互的基類為 `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`。 類的實例用 `HandlerConfiguration` 於初始化處理程式。 `HandlerConfiguration` 儲存伺服器配置資訊，包括傳輸憑據、時間戳容限、策略更新清單和撤銷清單。處理程式讀取請求資料並將請求解析為實例 `RequestMessageBase`。 呼叫者可以檢查請求中的資訊並決定是返回錯誤還是成功響應(子類 `RequestMessageBase` 提供設定響應資料的方法)。

如果請求成功，請設定響應資料；否則，在失 `RequestMessageBase.setErrorData()` 敗時調用。 一律以叫用方法來結 `close()` 束實作(建議在 `close()` 陳述式的 `finally` 區塊中呼叫 `try` )。 如需如 `MessageHandlerBase` 何叫用處理常式的範例，請參閱API參考檔案。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>HTTP狀態碼200(OK)應會針對處理常式處理的所有要求而傳送。 如果由於伺服器錯誤而無法建立處理常式，伺服器可能會以其他狀態碼(例如500（內部伺服器錯誤）)回應。

用戶端會使用封裝時指定的授權伺服器URL，做為傳送至授權伺服器的所有要求的基本URL。 例如，如果伺服器URL指定為&quot;<span></span>https://licenseserver.com/path&quot;，則用戶端會傳送要求至&quot;<span></span>https://licenseserver.com/path/flashaccess/...&quot;。 如需每種請求類型所使用之特定路徑的詳細資訊，請參閱下列章節。 實作授權伺服器時，請確定伺服器回應每種請求類型所需的路徑。

授權要求可包含驗證Token。 如果使用使用者名稱／密碼驗證，則請求可能包含 `AuthenticationToken` 由所產生的 `AuthenticationHandler`，而SDK將在核發授權前確保Token有效。
