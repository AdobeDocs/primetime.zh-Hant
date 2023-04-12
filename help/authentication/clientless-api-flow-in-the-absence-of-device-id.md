---
title: 沒有裝置ID時的無用戶端API流程
description: 沒有裝置ID時的無用戶端API流程
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# 沒有裝置ID時的無用戶端API流程 {#clientless-api-flow-in-the-absence-of-device-id}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

</br>


## 問題

並非所有智慧裝置應用程式都能提供唯一裝置ID。  由於deviceId是必要參數，若未傳遞，服務會傳回400錯誤。


## 臨時解決方案/解決方案

對於沒有設備ID的客戶端：

1. 第一次使用呼叫註冊代碼服務 `deviceId=dummy`
1. 從回應中擷取UUID。 UUID可在註冊程式碼回應（XML和JSON回應格式）的「id」元素中使用。
1. 再次呼叫註冊服務。 這次，通過 `deviceId=<uuid obtained in step #2>`
1. 在主控台UI上顯示在步驟3中取得的註冊代碼


完成這些步驟後，Adobe Primetime驗證會使用UUID做為裝置ID。 將此裝置ID(UUID)儲存在裝置的本機儲存體中。 如果使用者產生新註冊代碼，您應再次執行步驟1到4，然後以新的裝置ID(UUID)取代先前儲存的裝置ID。



## 永久解決方案

Adobe會在未來的版本中，借由 `deviceId` 建立登錄程式碼時的選用裝載，並使用UUID做為代號金鑰，而非使用 `deviceId`，當 `deviceId` 不存在。

<!--
## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)
-->