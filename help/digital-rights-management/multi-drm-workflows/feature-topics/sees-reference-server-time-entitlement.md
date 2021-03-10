---
description: 使用SEES瞭解如何使用ExpressPlay啟用以時間為基礎的權益服務。
title: 參考服務時間型權益
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# 參考服務：時間型權益{#reference-service-time-based-entitlement}

使用SEES瞭解如何使用ExpressPlay啟用以時間為基礎的權益服務。

SEES會從用戶端接收「權益要求」（請參閱「公用API」區段）。 SEES伺服器根據`contentID`查找CEK和IV，添加`expirationTime`，並將請求轉發到ExpressPlay伺服器。 最終的ExpressPlay Token有時限。 請參閱下方的「以時間為基礎的權益」順序圖。![](assets/fees-time-based.png)

**表1:用戶端傳送的授權參數**

| 查詢參數 | 說明 | 必要 |
|---|---|---|
| `contentKey` | 內容加密密鑰的16位元組十六進位字串表示 | 是 |
| `iv` | 內容加密的16位元組十六進位字串表示法IV | 是 |
| `rentalDuration` | 租金的持續時間（以秒為單位）（預設值= 0） | 否 |

**表2:SEES伺服器新增的Token限制參數**

<table id="table_E979FAD7A61A4832A46667301939FAEB">  
 <thead> 
  <tr> 
   <th class="entry"> 查詢參數 </th> 
   <th class="entry"> 說明 </th> 
   <th class="entry"> 需要？ </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> expirationTime</span> </td> 
   <td>此代號的過期時間。 此值必須是<a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" type="external"> RFC 3339</a>日期／時間格式的字串(「Z」區域指示符（「祖魯時間」），或前面帶有「+」符號的整數。 RFC 3339日期／時間的示例為<span class="codeph"> 2006-04-14T12:01:10Z</span>。 <p>如果該值是RFC 3339日期／時間格式中的字串，則表示令牌的絕對到期日／時間。 如果值是前面有'+'符號的整數，則會將其解讀為從發出該標籤有效的秒數。 例如，<span class="codeph"> +60</span>指定一分鐘。 Token存留期上限（且預設值，若未指定）為30天。 指定'+'符號時，請使用編碼格式"%2B"。 </p> </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>

