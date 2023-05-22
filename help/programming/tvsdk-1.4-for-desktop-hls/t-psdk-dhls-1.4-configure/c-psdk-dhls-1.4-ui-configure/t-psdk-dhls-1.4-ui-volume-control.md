---
description: 可以設定聲音音量的用戶介面控制項。
title: 提供音量控制
exl-id: 058d79d2-35cc-4238-8fc1-2820a2d91ffb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 提供音量控制{#provide-volume-control}

可以設定聲音音量的用戶介面控制項。

1. 等待MediaPlayer實例處於此命令的有效狀態。

   除RELEASED外的任何狀態都有效。
1. 在上調用卷集方法 `MediaPlayer` 實例，以設定音頻卷。

   ```
   public function set volume(value:Number):void
   ```

   卷的值表示請求的卷佔最大卷的比例，其中0為靜默，1為最大卷。

   <table id="table_144A2B1260374FBE8D976194F602DDC7"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> 如果指定的卷為 </th> 
      <th colname="col2" class="entry"> 生成的卷為 </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> 小於0 </td> 
      <td colname="col2"> 0 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> 0到1之間 </td> 
      <td colname="col2"> 指定的卷 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> 大於1 </td> 
      <td colname="col2"> 值除以100，並設定為以下值之一： 
      <ul id="ul_8C2282F0EDC44A408820F5768709214F"> 
      <li id="li_B00BC6F4812D4000891358F762C8E492">如果介於0和1之間，則結果 </li> 
      <li id="li_03B7F30662554F299320040CAC2DEB7A">如果結果大於1，則為1 </li> 
      </ul> <p>提示：此邏輯處理基於以前版本的客戶端提供的值 
      <span class="codeph">短語/黃金時段sdk名稱</span>，其中卷值介於0到100之間。 </p> </td> 
   </tr> 
   </tbody> 
   </table>
