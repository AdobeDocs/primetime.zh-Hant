---
title: 播放受保護內容所需的裝置功能
description: 播放受保護內容所需的裝置功能
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# 播放受保護內容{#device-capabilities-required-to-play-protected-content}所需的裝置功能

指定存取內容所需的硬體功能。 使用移植套件的裝置可取得硬體功能的相關資訊。

設備功能可由下表中指定的屬性來標識：

<table id="table_v3n_fks_n4"> 
 <tbody> 
  <tr> 
   <td><b>屬性</b> </td> 
   <td><b>支援的值</b> </td> 
   <td><b>符合條件</b> </td> 
   <td><b>說明</b> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">非用戶可訪問匯流排 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true"或"false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">完全符合 </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">如果為true，則設備不得具有用戶可訪問的匯流排。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">硬體信任根 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true"或"false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Exact Macth </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">如果為true，則設備必須具有硬體信任根。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>此使用規則受Adobe訪問客戶端2.0.2版和更高版本的支援。 舊客戶端的行為取決於許可證伺服器支援的最低客戶端版本。 請參閱[最低客戶端版本](../../../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md)。

