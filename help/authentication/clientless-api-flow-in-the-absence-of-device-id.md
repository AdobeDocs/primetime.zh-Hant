---
title: 沒有設備ID時的無客戶端API流
description: 沒有設備ID時的無客戶端API流
exl-id: 6549a6d6-03a9-4d95-99fb-d3ada832323d
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# 沒有設備ID時的無客戶端API流 {#clientless-api-flow-in-the-absence-of-device-id}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>


## 問題

並非所有智慧設備應用都能夠提供唯一的設備ID。  由於deviceId是強制參數，因此如果未傳遞該參數，服務將返回400錯誤。


## 臨時解決方案/解決方法

對於無設備ID的客戶端：

1. 首次呼叫註冊代碼服務 `deviceId=dummy`
1. 從響應中提取UUID。 UUID在註冊代碼響應（XML和JSON響應格式）的「id」元素中可用。
1. 再次呼叫註冊服務。 這次，過去 `deviceId=<uuid obtained in step #2>`
1. 在控制台UI上顯示步驟3中獲取的註冊代碼


完成這些步驟後，Adobe Primetime身份驗證將使用UUID作為設備ID。 將此設備ID(UUID)儲存在設備的本地儲存中。 如果用戶生成新註冊代碼，您應再次運行步驟1至4，然後用新的設備ID(UUID)替換先前儲存的設備ID。



## 永久解決方案

Adobe將在以後的版本中通過 `deviceId` 建立reg代碼時的可選負載，並使用UUID作為令牌密鑰，而不是 `deviceId`, `deviceId` 不存在。

<!--
## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)
-->
