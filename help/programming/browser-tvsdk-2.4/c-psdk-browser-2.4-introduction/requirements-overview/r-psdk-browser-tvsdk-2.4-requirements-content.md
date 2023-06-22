---
description: 檢查串流和播放清單（資訊清單）的限制和需求。
title: 內容和資訊清單需求
exl-id: 53fdd771-06ea-496f-9591-6ed4d5011f8d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# 內容和資訊清單需求{#content-and-manifest-requirements}

檢查串流和播放清單（資訊清單）的限制和需求。

<table id="table_D7C38CD3B4D24C3D9A3B55D8CEFE7366"> 
 <tbody> 
  <tr> 
   <td colname="col1"> 內容區段持續時間 </td> 
   <td colname="col2"> 區段的持續時間不得超過資訊清單檔案中指定的目標持續時間。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 內容需求 </td> 
   <td colname="col2"> 每個TS區段都應該以關鍵框架開頭。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> HLS內容 </td> 
   <td colname="col2"> <p>請記住以下事項： 
     <ul id="ul_B226605345EA46F69DA1380E16826117"> 
      <li id="li_6564DC0E879544BB8513DD2D1CFBA8DE">不支援AAC-SSR音訊。 </li> 
      <li id="li_B73CAEBE4347406EA4DB25551B444BDA">不支援音訊轉碼器AC3和增強型AC3。 </li> 
      <li id="li_5986DD33C0FE485D99D4C00E2E6012CA">HLS串流具有不連續性，但不支援不連續性標籤。 </li> 
      <li id="li_FED8686372DF4A39BAABC531BA4EB137">HLS Live不支援時間戳記滑動。 </li> 
      <li id="li_565CFBEAD9874BA48F6E25B0893BF131">HLS即時資料流的DVR視窗中的廣告未解析。 </li> 
      <li id="li_7D22EA32C94240D79EDDA96D9E72FE8F">AES-128加密內容不支援位元組範圍。 </li> 
     </ul></p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 虛線內容 </td> 
   <td colname="col2"> <p>請記住以下事項： 
     <ul id="ul_9D33C2418F9F49DEAE0E642301726F89"> 
      <li id="li_74C69A21A7BD4831B92F0D57900E1CB1">對於即時資料流 — 支援動態型別的即時設定檔。 </li> 
      <li id="li_0C8743DB152047819D23C9F180998AD7">對於VOD資料流 — 支援靜態型別的即時設定檔。 </li> 
      <li id="li_FBC6828663FB413798A4BDAF0B9831AA">對於VOD資料流 — 隨選設定檔未針對廣告工作流程進行認證。 </li> 
      <li id="li_4393B9B1F6144BDEAE484C879750ED23">不支援播放具有多個句點的DASH資料流。 </li> 
      <li id="li_6A2CEC4E974C4D44A45F5503A1A9D8D0">支援透過Accessibility標籤訊號的內嵌註解(608/708)。 </li> 
      <li id="li_EDE93DF4F3A64A53BA80877F701A8F0D">不支援片段/分段的VTT檔案。 </li> 
      <li id="li_8897F73611194030A490A4FF1178364C">未認證具有頻帶內自訂標籤的資料流。 </li> 
     </ul></p> </td> 
  </tr> 
 </tbody> 
</table>
