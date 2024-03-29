---
title: 播放受保護內容所需的裝置功能
description: 播放受保護內容所需的裝置功能
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# 播放受保護內容所需的裝置功能 {#device-capabilities-required-to-play-protected-content}

指定存取內容所需的硬體功能。 使用移植套件的裝置可取得有關硬體功能的資訊。

裝置功能可由下表中指定的屬性來識別：

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
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">精確匹配 </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">如果為true，則裝置必須有信任的硬體根目錄。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Adobe Access使用者端2.0.2版及更新版本支援此使用規則。 較舊使用者端上的行為取決於授權伺服器支援的最低使用者端版本。 請參閱， [最低使用者端版本](../../../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md).
