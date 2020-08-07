---
description: 'null'
seo-description: 'null'
seo-title: 播放受保護內容所需的裝置功能
title: 播放受保護內容所需的裝置功能
uuid: 1490711b-65d9-4716-8779-ae1da7d2c82c
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---


# 播放受保護內容所需的裝置功能 {#device-capabilities-required-to-play-protected-content}

所需的設備功能指定訪問內容所需的硬體功能。 使用移植套件的裝置可取得硬體功能的相關資訊。

以下屬性可識別裝置功能：

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
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">完全符合 </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">如果為true，則設備必須具有硬體信任根。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Adobe Primetime DRM用戶端2.0.2版及更新版本支援此使用規則。 舊客戶端的行為取決於許可證伺服器支援的最低客戶端版本。
>
>請參 [閱最低用戶端版本](../../../../protecting-content/setting-up-the-sdk/setup-dev-env.md)。

