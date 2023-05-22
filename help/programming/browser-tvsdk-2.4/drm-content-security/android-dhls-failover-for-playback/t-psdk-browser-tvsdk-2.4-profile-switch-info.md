---
description: 當媒體播放器將其當前配置檔案切換到新配置檔案時，您可以檢索有關交換機的資訊，包括交換機何時切換、寬度和高度資訊，或使用不同比特率的原因。
title: 獲取有關配置式交換機的資訊
exl-id: 3ef4b319-dd78-4abd-9c2d-ab1d608f6cea
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---

# 獲取有關配置式交換機的資訊{#get-information-about-profile-switch}

當媒體播放器將其當前配置檔案切換到新配置檔案時，您可以檢索有關交換機的資訊，包括交換機何時切換、寬度和高度資訊，或使用不同比特率的原因。

1. 聽著 `AdobePSDK.PSDKEventType.PROFILE_CHANGED` 的子菜單。

   當瀏覽器TVSDK媒體播放器的自適應比特率切換算法由於網路或機器條件而切換到另一個配置檔案時，它會調度此事件。 （當比特率或期間更改時。）
1. 發生事件時，請檢查以下屬性以瞭解有關交換機的資訊：

   * `profile`:正在使用的新配置檔案的標識符。
   * `time`:交換機發生的流時間。
   * `description`:以分號分隔的鍵/值對的字串形式描述比特率更改的原因。 最多包含一個 `Reason` 一個 `Bitrate`。 如果資訊不可用或比特率未更改，則此字串為空。

   <table id="table_E400FD9C57FF40CBAC14AF6847CD8301"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> 密鑰名稱 </th> 
      <th colname="col2" class="entry"> 可能的值 </th> 
      </tr> 
    </thead>
    <tbody> 
      <tr> 
      <td colname="col1"> <span class="codeph"> 原因 </span> </td> 
      <td colname="col2"> 
        <ul id="ul_37DDE3F297634ED6B47DF5D73F969369"> 
        <li id="li_E374B029E1AF40689D70A9D30E057C5B">網路適應 </li> 
        <li id="li_753862EEF1C9474EA8E20C89F5EF5D8D">尋找 </li> 
        <li id="li_EC14923F92CF4D11A47928A8D2DE6D8B">不支援配置檔案 </li> 
        <li id="li_695AB4A89C9D4833AF6D8B6424FC912B">故障轉移 </li> 
        </ul> </td> 
      </tr> 
      <tr> 
      <td colname="col1"> <span class="codeph"> 比特率 </span> </td> 
      <td colname="col2"> 
        <ul id="ul_1B49BD90A91147359712E1AFD8877E23"> 
        <li id="li_1C8E593C65D34742B14A8D0EAD43E0A9"> <span class="codeph"> 向上 </span>:比特率增加 </li> 
        <li id="li_B1A00E3985A849B6855E15CF70D79BB8"> <span class="codeph"> 向下 </span>:比特率降低 </li> 
        </ul> </td> 
      </tr> 
    </tbody> 
    </table>

   以下是返回的一些示例 `description` 字串：

   ```
   "Bitrate::=up;Reason::=Network Adaptation;" 
   
   "Bitrate::=down;Reason::=Failover;"
   ```

   * `width`:整數，表示寬度（以像素為單位）。
   * `height`:整數，表示高度（以像素為單位）。

   >[!NOTE]
   >
   >寬度和高度資料僅在包含在 `RESOLUTION` 標籤。 如果M3U8中未包括該資訊，則寬度和高度屬性將設定為0，因為它們不是配置檔案資訊的一部分。
