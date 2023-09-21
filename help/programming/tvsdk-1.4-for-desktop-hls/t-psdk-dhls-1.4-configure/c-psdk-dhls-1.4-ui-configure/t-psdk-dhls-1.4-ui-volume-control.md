---
description: 您可以設定音量的使用者介面控制項。
title: 提供音量控制
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 提供音量控制{#provide-volume-control}

您可以設定音量的使用者介面控制項。

1. 請等待MediaPlayer執行個體處於此命令的有效狀態。

   除RELEASED以外的任何狀態都是有效的。
1. 呼叫上的音量設定方法 `MediaPlayer` 執行個體以設定音量。

   ```
   public function set volume(value:Number):void
   ```

   磁碟區的值代表要求的磁碟區，以最大磁碟區的比例表示，其中0是靜音，1是最大磁碟區。

   <table id="table_144A2B1260374FBE8D976194F602DDC7"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> 如果指定的磁碟區為 </th> 
      <th colname="col2" class="entry"> 產生的體積塊為 </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> 小於0 </td> 
      <td colname="col2"> 0 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> 介於0和1 </td> 
      <td colname="col2"> 指定的磁碟區 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> 大於1 </td> 
      <td colname="col2"> 值除以100，並設為下列其中一個值： 
      <ul id="ul_8C2282F0EDC44A408820F5768709214F"> 
      <li id="li_B00BC6F4812D4000891358F762C8E492">如果介於0和1之間的結果 </li> 
      <li id="li_03B7F30662554F299320040CAC2DEB7A">如果結果大於1，則為1 </li> 
      </ul> <p>提示：此邏輯會根據舊版的 
      <span class="codeph">片語/primetime-sdk-name</span>，其中體積值介於0到100之間。 </p> </td> 
   </tr> 
   </tbody> 
   </table>
