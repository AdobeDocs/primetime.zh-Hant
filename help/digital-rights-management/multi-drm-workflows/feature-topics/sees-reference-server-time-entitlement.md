---
description: 與SEES合作，瞭解如何使用ExpressPlay啟用以時間為基礎的軟體權利檔案服務。
title: 參考服務基於時間的權益
exl-id: a37b0e71-ba7b-4f03-9866-5e8b062e0b7d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# 參考服務：以時間為基礎的權益 {#reference-service-time-based-entitlement}

與SEES合作，瞭解如何使用ExpressPlay啟用以時間為基礎的軟體權利檔案服務。

SEE會收到來自使用者端的權益請求（請參閱公開API區段）。 SEES伺服器會根據 `contentID`，新增 `expirationTime`，並將要求轉送至ExpressPlay伺服器。 最後的ExpressPlay權杖是時間限制。 請參閱下列以時間為基礎的軟體權利檔案順序圖表。 ![](assets/fees-time-based.png)

**表1：使用者端傳送的授權引數**

| 查詢引數 | 說明 | 必填 |
|---|---|---|
| `contentKey` | 內容加密金鑰的16位元組十六進位字串表示法 | 是 |
| `iv` | 內容加密IV的16位元組十六進位字串表示法 | 是 |
| `rentalDuration` | 租用的期間（以秒為單位，預設= 0） | 否 |

**表2： SEES伺服器新增的權杖限制引數**

<table id="table_E979FAD7A61A4832A46667301939FAEB">  
 <thead> 
  <tr> 
   <th class="entry"> 查詢引數 </th> 
   <th class="entry"> 說明 </th> 
   <th class="entry"> 必填？ </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> 過期時間</span> </td> 
   <td>此權杖的到期時間。 此值必須是中的字串 <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" type="external"> RFC 3339</a> 'Z'區域指示符號中的日期/時間格式（'Zulu時間'），或是以'+'符號開頭的整數。 RFC 3339日期/時間的範例為 <span class="codeph"> 2006-04-14T12:01:10Z</span>. <p>如果值是RFC 3339日期/時間格式的字串，則表示權杖的絕對到期日/時間。 如果值是前面有'+'符號的整數，則會解譯為簽發權杖有效的相對秒數。 例如， <span class="codeph"> +60</span> 指定一分鐘。 權杖存留期的上限（以及預設值，若未指定）為30天。 指定'+'符號時，請使用編碼形式'%2B''。 </p> </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>
