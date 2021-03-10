---
description: 檢查串流和播放清單（資料清單）的限制和要求。
title: 內容與資訊清單需求
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---


# 內容與資訊清單需求{#content-and-manifest-requirements}

檢查串流和播放清單（資料清單）的限制和要求。

<table id="table_D7C38CD3B4D24C3D9A3B55D8CEFE7366"> 
 <tbody> 
  <tr> 
   <td colname="col1"> 內容區段持續時間 </td> 
   <td colname="col2"> 區段的持續時間不得超過資訊清單檔案中指定的目標持續時間。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 內容需求 </td> 
   <td colname="col2"> 每個TS段都應以關鍵幀開始。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> HLS內容 </td> 
   <td colname="col2"> <p>請記住： 
     <ul id="ul_B226605345EA46F69DA1380E16826117"> 
      <li id="li_6564DC0E879544BB8513DD2D1CFBA8DE">不支援AAC-SSR音訊。 </li> 
      <li id="li_B73CAEBE4347406EA4DB25551B444BDA">不支援音訊轉碼器AC3和增強型AC3。 </li> 
      <li id="li_5986DD33C0FE485D99D4C00E2E6012CA">HLS流具有不連續性，但不支援不不連續性標籤。 </li> 
      <li id="li_FED8686372DF4A39BAABC531BA4EB137">HLS Live不支援時間戳記變換。 </li> 
      <li id="li_565CFBEAD9874BA48F6E25B0893BF131">HLS Live串流的DVR視窗中的廣告無法解決。 </li> 
      <li id="li_7D22EA32C94240D79EDDA96D9E72FE8F">AES-128加密內容不支援位元組範圍。 </li> 
     </ul></p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 虛線內容 </td> 
   <td colname="col2"> <p>請記住： 
     <ul id="ul_9D33C2418F9F49DEAE0E642301726F89"> 
      <li id="li_74C69A21A7BD4831B92F0D57900E1CB1">對於即時串流——支援動態類型的即時描述檔。 </li> 
      <li id="li_0C8743DB152047819D23C9F180998AD7">對於VOD串流——支援靜態類型的即時描述檔。 </li> 
      <li id="li_FBC6828663FB413798A4BDAF0B9831AA">針對VOD串流——不會針對廣告工作流程認證隨選設定檔。 </li> 
      <li id="li_4393B9B1F6144BDEAE484C879750ED23">不支援播放含有多個句號的DASH串流。 </li> 
      <li id="li_6A2CEC4E974C4D44A45F5503A1A9D8D0">支援透過協助工具標籤發出信號的內嵌標題(608/708)。 </li> 
      <li id="li_EDE93DF4F3A64A53BA80877F701A8F0D">不支援分割／分段的VTT檔案。 </li> 
      <li id="li_8897F73611194030A490A4FF1178364C">無法認證帶內自訂標籤的串流。 </li> 
     </ul></p> </td> 
  </tr> 
 </tbody> 
</table>

