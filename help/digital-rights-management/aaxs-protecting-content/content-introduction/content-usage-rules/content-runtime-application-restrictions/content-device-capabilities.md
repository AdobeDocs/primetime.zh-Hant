---
title: 播放受保護內容所需的設備功能
description: 播放受保護內容所需的設備功能
copied-description: true
exl-id: 5f2089e9-3176-46a7-9998-2dad0e77e453
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# 播放受保護內容所需的設備功能 {#device-capabilities-required-to-play-protected-content}

指定訪問內容所需的硬體功能。 有關硬體功能的資訊可用於使用移植套件的設備。

設備功能可由下表中指定的屬性標識：

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
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">埃克斯塔特 </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">如果為true，則設備必須具有信任的硬體根。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Adobe訪問客戶端2.0.2版及更高版本支援此使用規則。 舊客戶端的行為取決於許可證伺服器支援的最低客戶端版本。 看， [最低客戶端版本](../../../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md)。
