---
title: 播放受保護內容所需的裝置功能
description: 播放受保護內容所需的裝置功能
copied-description: true
exl-id: 540fbb53-ec1a-43be-b51b-9937ed31e384
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 播放受保護內容所需的裝置功能 {#device-capabilities-required-to-play-protected-content}

所需的裝置功能指定存取內容所需的硬體功能。 使用移植工具組的裝置可取得硬體功能的相關資訊。

下列屬性可識別裝置功能：

<table id="table_v3n_fks_n4"> 
 <tbody> 
  <tr> 
   <td><b>屬性</b> </td> 
   <td><b>支援的值</b> </td> 
   <td><b>符合條件</b> </td> 
   <td><b>說明</b> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">非使用者可存取的匯流排 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true"或"false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">完全相符 </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">如果為true，則裝置不能有使用者可存取的匯流排。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">信任的硬體根目錄 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true"或"false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">完全相符 </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">如果為true，則裝置必須具有信任的硬體根目錄。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Adobe Primetime DRM使用者端2.0.2版及更新版本支援此使用規則。 舊版使用者端的行為取決於授權伺服器支援的最低使用者端版本。
>
>另請參閱 [最低使用者端版本](../../../../protecting-content/setting-up-the-sdk/setup-dev-env.md).
