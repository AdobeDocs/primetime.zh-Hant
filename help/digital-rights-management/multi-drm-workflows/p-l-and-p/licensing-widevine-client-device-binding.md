---
description: 在某些情況下，您可能希望限制最終用戶在購買或租用內容時在多個設備上播放內容。 如果客戶使用Expressplay，則可以使用Expressplay API將用戶的Expressplay令牌綁定到用戶的電腦。
title: 設備綁定
exl-id: 96ead794-e3eb-4059-91d3-a2c351a17ea3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 設備綁定{#device-binding}

在某些情況下，您可能希望限制最終用戶在購買或租用內容時在多個設備上播放內容。 如果客戶使用Expressplay，則可以使用Expressplay API將用戶的Expressplay令牌綁定到用戶的電腦。

可以通過以下方式使用API。

1. 生成Cookie。
1. 發送虛擬令牌生成請求，生成的cookie作為查詢字串附加(cookie=`<cookie>`)或作為標題。
1. 讓用戶的電腦使用上述令牌（例如通過播放虛擬內容）向Expressplay許可證伺服器發送許可請求。

   成功後，此虛擬許可請求將用戶的device_id（由用戶設備上的DRM實現計算或生成）與Expressplay後端中的cookie相關聯。 然後，以下方式使用此cookie:

   * 在內容購買/租用時，代碼通過發送關聯的cookie( [https://www.expressplay.com/developer/restapi/#record-retrieval](https://www.expressplay.com/developer/restapi/#record-retrieval))
   * 使用購買內容的密鑰(CEK)、密鑰ID(CEKSID)、策略和其他資訊發送令牌生成請求，將上面的cookie和deviceid分別附加為 `cookie` 相關參數 `deviceid` 令牌限制參數。

   * 向用戶提供此令牌。

      此進程為綁定到用戶的device_id的內容生成令牌。 當用戶的電腦發出具有此令牌的許可證請求時，Expressplay後端將用許可證請求的deviceid交叉檢查令牌的deviceid。

      示例Expressplay權利伺服器實現此工作流。
