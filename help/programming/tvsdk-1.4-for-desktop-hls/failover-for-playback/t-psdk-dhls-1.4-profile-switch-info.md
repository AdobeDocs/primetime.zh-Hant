---
description: 當媒體播放器將其目前的設定檔切換至新的設定檔時，您可以擷取關於切換的資訊，包括切換的時間、寬度和高度資訊，或是使用不同位元速率的原因。
title: 取得設定檔切換器的相關資訊
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# 取得設定檔切換器的相關資訊{#get-information-about-profile-switch}

當媒體播放器將其目前的設定檔切換至新的設定檔時，您可以擷取關於切換的資訊，包括切換的時間、寬度和高度資訊，或是使用不同位元速率的原因。

1. 聆聽 `ProfileEvent.PROFILE_CHANGED` 事件。

   TVSDK媒體播放器在其最適化位元速率切換演演算法因網路或電腦狀況而切換至另一個設定檔時，會排程此事件。 （當位元速率或週期變更時。）
1. 發生事件時，請檢查下列屬性，以取得關於交換器的資訊：

   * `profile`：所使用新設定檔的識別碼。
   * `time`：切換發生的資料流時間。
   * `description`：位元速率變更原因的文字說明，以分號分隔的索引鍵/值配對字串。 最多包含一個 `Reason` 和一個 `Bitrate`. 如果資訊無法使用或位元速率未變更，則此字串為空白。

     <table id="table_E400FD9C57FF40CBAC14AF6847CD8301"> 
       <thead> 
         <tr> 
         <th colname="col1" class="entry"> 金鑰名稱 </th> 
         <th colname="col2" class="entry"> 可能的值 </th> 
         </tr> 
       </thead>
       <tbody> 
         <tr> 
         <td colname="col1"> <span class="codeph"> 原因 </span> </td> 
         <td colname="col2"> 
          <ul id="ul_37DDE3F297634ED6B47DF5D73F969369"> 
          <li id="li_E374B029E1AF40689D70A9D30E057C5B">網路適配 </li> 
          <li id="li_753862EEF1C9474EA8E20C89F5EF5D8D">搜尋 </li> 
          <li id="li_EC14923F92CF4D11A47928A8D2DE6D8B">設定檔不受支援 </li> 
          <li id="li_695AB4A89C9D4833AF6D8B6424FC912B">容錯移轉 </li> 
          </ul> </td> 
         </tr> 
         <tr> 
         <td colname="col1"> <span class="codeph"> 位元速率 </span> </td> 
         <td colname="col2"> 
          <ul id="ul_1B49BD90A91147359712E1AFD8877E23"> 
          <li id="li_1C8E593C65D34742B14A8D0EAD43E0A9"> <span class="codeph"> 向上 </span>：位元速率增加 </li> 
          <li id="li_B1A00E3985A849B6855E15CF70D79BB8"> <span class="codeph"> 向下 </span>：位元速率降低 </li> 
          </ul> </td> 
         </tr> 
       </tbody> 
       </table>

     以下是傳回的一些範例 `description` 字串：

     ```
     "Bitrate::=up;Reason::=Network Adaptation;" 
     
     "Bitrate::=down;Reason::=Failover;"
     ```

   * `width`：整數，指出寬度（畫素）。
   * `height`：整數，表示高度（畫素）。

     >[!NOTE]
     >
     >寬度和高度資料必須包含在 `RESOLUTION` M3U8資訊清單中的標籤。 如果資訊未包含在M3U8中，則寬度和高度屬性會設為0，因為這些屬性不是設定檔資訊的一部分。

<!--<a id="example_A713D420AE2E4E3CB7B78C6BC732BE90"></a>-->

例如：

```
_player.addEventListener(ProfileEvent.PROFILE_CHANGED, onProfileChange); 
private function onProfileChange(event:ProfileEvent):void { 
    _logger.info("#onProfileChange Current profile/bitrate has changed.  
      {0} for reason {1} of resolution [ {2} , {3} ]",  
      event.profile, event.description, event.width, event.height); 
}
```
