---
description: 當媒體播放器將其當前配置式切換到新配置式時，您可以檢索有關交換機的資訊，包括交換機何時切換、寬度和高度資訊，或使用不同位速率的原因。
title: 取得設定檔切換的相關資訊
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# 獲取有關配置式交換機的資訊{#get-information-about-profile-switch}

當媒體播放器將其當前配置式切換到新配置式時，您可以檢索有關交換機的資訊，包括交換機何時切換、寬度和高度資訊，或使用不同位速率的原因。

1. 監聽`ProfileEvent.PROFILE_CHANGED`事件。

   當TVSDK媒體播放器的可調式位元速率切換演算法因網路或機器狀況而切換至其他描述檔時，就會調度此事件。 （當位元速率或句點變更時）。
1. 發生事件時，請查看以下屬性以獲得有關交換機的資訊：

   * `profile`:使用之新描述檔的識別碼。
   * `time`:發生切換的流時間。
   * `description`:位元速率變更原因的文字說明，以分號分隔的鍵／值配對字串。最多包含一個`Reason`和一個`Bitrate`。 如果資訊不可用或位元速率未變更，則此字串為空。

   <table id="table_E400FD9C57FF40CBAC14AF6847CD8301"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> 密鑰名稱 </th> 
      <th colname="col2" class="entry"> 可能的值 </th> 
      </tr> 
    </thead>
    <tbody> 
      <tr> 
      <td colname="col1"> <span class="codeph"> 原因  </span> </td> 
      <td colname="col2"> 
       <ul id="ul_37DDE3F297634ED6B47DF5D73F969369"> 
       <li id="li_E374B029E1AF40689D70A9D30E057C5B">網路適應 </li> 
       <li id="li_753862EEF1C9474EA8E20C89F5EF5D8D">搜尋 </li> 
       <li id="li_EC14923F92CF4D11A47928A8D2DE6D8B">不支援描述檔 </li> 
       <li id="li_695AB4A89C9D4833AF6D8B6424FC912B">故障切換 </li> 
       </ul> </td> 
      </tr> 
      <tr> 
      <td colname="col1"> <span class="codeph"> 位元速率  </span> </td> 
      <td colname="col2"> 
       <ul id="ul_1B49BD90A91147359712E1AFD8877E23"> 
       <li id="li_1C8E593C65D34742B14A8D0EAD43E0A9"> <span class="codeph"> 向上 </span>:位元速率增加 </li> 
       <li id="li_B1A00E3985A849B6855E15CF70D79BB8"> <span class="codeph"> 向下 </span>:位元速率降低 </li> 
       </ul> </td> 
      </tr> 
    </tbody>
</table>

    以下是傳回的&#39;description&#39;字串：
    
    &quot;
    &quot;Bitrate::=up;Reason::=Network Adapation;&quot;
    
    &quot;Bitrate::=down;Reason::=Failover;&quot;
    
    
    &quot;* &quot;width&grave;:以像素表示寬度的整數。
    * 「高度」:以像素表示高度的整數。
    
    >[!NOTE]
    >
    >寬度和高度資料只有包含在M3U8資訊清單的「RESOLUTION」標籤中時才可用。如果M3U8中未包含該資訊，則寬度和高度屬性將設定為0，因為它們不是配置檔案資訊的一部分。

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
