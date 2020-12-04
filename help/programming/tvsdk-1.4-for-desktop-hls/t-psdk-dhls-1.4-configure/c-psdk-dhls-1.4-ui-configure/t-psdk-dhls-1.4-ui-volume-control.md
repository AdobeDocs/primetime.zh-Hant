---
description: 您可以設定音量的使用者介面控制項。
seo-description: 您可以設定音量的使用者介面控制項。
seo-title: 提供音量控制
title: 提供音量控制
uuid: c51e99b6-efd1-414e-9ef7-77bd53e0d6c0
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---


# 提供卷控制{#provide-volume-control}

您可以設定音量的使用者介面控制項。

1. 等待MediaPlayer實例處於此命令的有效狀態。

   除「已發佈」(RELEASED)之外的任何狀態都有效。
1. 在`MediaPlayer`實例上調用volume set method以設定音頻音量。

   ```
   public function set volume(value:Number):void
   ```

   卷的值表示請求的卷佔最大卷的比例，其中0為靜默，1為最大卷。

   <table id="table_144A2B1260374FBE8D976194F602DDC7"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> 如果指定的卷為 </th> 
      <th colname="col2" class="entry"> 產生的卷為 </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> 小於0 </td> 
      <td colname="col2"> 0 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> 介於0和1之間 </td> 
      <td colname="col2"> 指定的卷 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> 大於1 </td> 
      <td colname="col2"> 值除以100，並設為下列其中一個值： 
      <ul id="ul_8C2282F0EDC44A408820F5768709214F"> 
      <li id="li_B00BC6F4812D4000891358F762C8E492">如果介於0和1之間，則結果為 </li> 
      <li id="li_03B7F30662554F299320040CAC2DEB7A">1，如果結果大於1 </li> 
      </ul> <p>提示： 此邏輯會根據舊版的 
      <span class="codeph">phrates/primetime-sdk-name</span>，其中卷值介於0到100之間。 </p> </td> 
   </tr> 
   </tbody> 
   </table>
