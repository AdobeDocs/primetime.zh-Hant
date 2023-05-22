---
title: 播放受保護內容所需的設備功能
description: 播放受保護內容所需的設備功能
copied-description: true
exl-id: 540fbb53-ec1a-43be-b51b-9937ed31e384
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 播放受保護內容所需的設備功能 {#device-capabilities-required-to-play-protected-content}

所需的設備功能指定訪問內容所需的硬體功能。 有關硬體功能的資訊可用於使用移植套件的設備。

以下屬性可標識設備功能：

<table id="table_v3n_fks_n4"> 
 <tbody> 
  <tr> 
   <td><b>屬性</b> </td> 
   <td><b>支援的值</b> </td> 
   <td><b>匹配條件</b> </td> 
   <td><b>說明</b> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">非用戶可訪問的匯流排 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true"或"false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">完全匹配 </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">如果為true，則設備不得具有用戶可訪問的匯流排。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">硬體信任根 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true"或"false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">完全匹配 </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">如果為true，則設備必須具有信任的硬體根。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Adobe PrimetimeDRM客戶端2.0.2版及更高版本支援此使用規則。 舊客戶端的行為取決於許可證伺服器支援的最低客戶端版本。
>
>請參閱 [最低客戶端版本](../../../../protecting-content/setting-up-the-sdk/setup-dev-env.md)。
