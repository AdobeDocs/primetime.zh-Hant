---
description: 與SEES一起查看如何使用ExpressPlay啟用基於時間的權利服務。
title: 參考服務基於時間的權利
exl-id: a37b0e71-ba7b-4f03-9866-5e8b062e0b7d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# 參考服務：基於時間的權利 {#reference-service-time-based-entitlement}

與SEES一起查看如何使用ExpressPlay啟用基於時間的權利服務。

SEES從客戶端接收權利請求（請參閱「公共API」部分）。 SEES伺服器根據 `contentID`的 `expirationTime`，並將請求轉發到ExpressPlay伺服器。 最後的ExpressPlay令牌是時間限制的。 請參閱下面的基於時間的權利序列圖。 ![](assets/fees-time-based.png)

**表1:客戶端發送的許可證參數**

| 查詢參數 | 說明 | 必需 |
|---|---|---|
| `contentKey` | 內容加密密鑰的16位元組十六進位字串表示 | 是 |
| `iv` | 內容加密IV的16位元組十六進位字串表示 | 是 |
| `rentalDuration` | 租用的持續時間（秒）（預設值= 0） | 否 |

**表2:由SEES伺服器添加的令牌限制參數**

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
   <td><span class="codeph"> 到期時間</span> </td> 
   <td>此令牌的過期時間。 此值必須是中的字串 <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" type="external"> RFC 3339</a> 「Z」區域指示符（「祖魯時間」）中的日期/時間格式，或前面帶「+」符號的整數。 RFC 3339的一個示例是 <span class="codeph"> 2006-04-14T12:01:10Z</span>。 <p>如果該值是RFC 3339日期/時間格式的字串，則表示令牌的絕對到期日/時間。 如果值是前面帶有「+」符號的整數，則會將其解釋為令牌有效的發出後的相對秒數。 比如說， <span class="codeph"> +60</span> 指定一分鐘。 最大(和預設（如果未指定）令牌生存期為30天。 指定「+」符號時，請使用編碼格式「%2B」。 </p> </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>
