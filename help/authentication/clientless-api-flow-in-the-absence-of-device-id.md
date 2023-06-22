---
title: 沒有裝置ID時的無使用者端API流程
description: 沒有裝置ID時的無使用者端API流程
exl-id: 6549a6d6-03a9-4d95-99fb-d3ada832323d
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# 沒有裝置ID時的無使用者端API流程 {#clientless-api-flow-in-the-absence-of-device-id}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

</br>


## 問題

並非所有智慧型裝置應用程式都能提供唯一的裝置ID。  由於deviceId是必要引數，如果未傳遞，服務會傳回400錯誤。


## 臨時解決方案/因應措施

對於沒有裝置ID的使用者端：

1. 第一次使用呼叫註冊代碼服務 `deviceId=dummy`
1. 從回應中擷取UUID。 UUID可在註冊代碼回應的「id」元素中使用（XML和JSON回應格式）。
1. 再次致電註冊服務。 這次，通過 `deviceId=<uuid obtained in step #2>`
1. 在主控台UI上顯示步驟3中取得的註冊代碼


完成這些步驟後，Adobe Primetime驗證將使用UUID作為裝置ID。 將此裝置ID (UUID)儲存在裝置的本機儲存空間中。 萬一使用者產生新的註冊代碼，您應再次執行步驟1到4，然後將先前儲存的裝置ID (UUID)取代為新裝置ID。



## 永久解決方案

Adobe在未來版本中會透過以下方式變更此設定： `deviceId` 建立登入程式碼時，選用的裝載，並使用UUID作為代號金鑰，而不是 `deviceId`，時間 `deviceId` 不存在。

<!--
## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)
-->
