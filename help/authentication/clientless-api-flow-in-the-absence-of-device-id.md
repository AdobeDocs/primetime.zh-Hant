---
title: 缺少裝置ID時的無使用者端API流程
description: 缺少裝置ID時的無使用者端API流程
exl-id: 6549a6d6-03a9-4d95-99fb-d3ada832323d
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# 缺少裝置ID時的無使用者端API流程 {#clientless-api-flow-in-the-absence-of-device-id}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要Adobe的目前授權。 不允許未經授權的使用。

</br>


## 問題

並非所有智慧型裝置應用程式都能提供唯一的裝置ID。  由於deviceId是必要引數，若未傳遞，服務會傳回400錯誤。


## 臨時解決方案/因應措施

對於沒有裝置ID的使用者端：

1. 第一次使用呼叫註冊代碼服務 `deviceId=dummy`
1. 從回應中擷取UUID。 UUID可在註冊代碼回應（XML和JSON回應格式）的「id」元素中使用。
1. 再次致電註冊服務。 這次，通過 `deviceId=<uuid obtained in step #2>`
1. 在主控台UI上顯示步驟3中取得的註冊代碼


完成這些步驟後，Adobe Primetime驗證會使用UUID做為裝置ID。 將此裝置ID (UUID)儲存在裝置的本機儲存空間中。 萬一使用者產生新的註冊代碼，您應再次執行步驟1到4，然後將先前儲存的裝置ID (UUID)取代為新裝置ID。



## 永久解決方案

Adobe將在未來版本中變更此設定，方法是透過 `deviceId` 建立登入程式碼時，選用的裝載，並使用UUID做為權杖金鑰而非 `deviceId`，時間 `deviceId` 不存在。

<!--
## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)
-->
