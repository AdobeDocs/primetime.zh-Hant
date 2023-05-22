---
title: 用戶元資料功能
description: 用戶元資料功能
exl-id: 9fd68885-7b3a-4af0-a090-6f1f16efd2a1
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 0%

---

# 用戶元資料 {#user-metadata}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>
</br>

## 導言 {#intro}

用戶元資料功能使程式設計師能夠訪問由MVPD維護的不同類型的用戶特定資料。  用戶元資料類型包括郵遞區號、家長評級、用戶ID等。  *用戶* 元資料是以前可用的擴展 *靜態* 元資料（驗證令牌TTL、授權令牌TTL和設備ID）。


用戶元資料關鍵點：

- 在驗證和授權流程期間傳遞給程式設計師的應用程式
- 值保存在標籤中
- 如果不同的MVPD以不同格式提供資料，則值可以標準化
- 使用程式設計師密鑰（如郵遞區號）可以加密某些參數
- 通過配置更改，Adobe提供特定值

## 獲取用戶元資料 {#obtaining}

通過AccessEnabler程式設計師可以使用用戶元資料 `getMetadata()` 函式和通過 `/usermetadata` 端點。  有關使用的詳細資訊，請參閱平台API文檔 `getMetadata()` 及其相應的回調 `setMetadataStatus()` （或用於無客戶端API中使用的端點和參數）。

程式設計師通過為要獲取的元資料類型提供密鑰來獲取元資料： `getMetadata(key)`。  

元資料返回如下： `setMetadataStatus(key, encrypted, data)`:

| 參數 | 類型 | 說明 |
| ----------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `key` | 字串 | 指定請求的元資料類型 |
| `encrypted` | 布爾型 | 一個布爾標誌，表示是否加密了&quot;value&quot;。 如果為&quot;true&quot;，則&quot;value&quot;實際上將是實際值的JSON Web加密表示。 |
| `data` | 對象 | 包含元資料表示形式的JSON對象 |

 

資料參數的結構、值因類型而異：

| 鍵 | 值類型 | 示例 | 說明 |
| --- | --- | --- | --- |
| `zip` | JSON陣列 | \[&quot;77754&quot;, &quot;12345&quot;\] | 郵遞區號 |
| `householdID` | JSON字串 | &quot;1o7241p&quot; | 家庭標識。 如果MVPD不支援子帳戶，則與 `userID` |
| `maxRating` | JSON對象 | { MPAA:&quot;NR&quot;, <br>  VCHIP:&quot;X&quot;  <br>  URL:&quot;http://manage.my/parental&quot; } | 用戶的最大家長評級 |
| `userID` | JSON字串 | &quot;1o7241p&quot; | 用戶標識符。 如果MVPD支援子帳戶，而用戶不是主帳戶， `userID` 將不同於 `householdID`。 |
| `channelID` | JSON陣列 | \[ &quot;通道–1&quot;, &quot;通道–2&quot; \] | 用戶有權查看的頻道清單 |
| `is_hoh` | JSON字串 | &quot;1&quot; | 標識用戶是否是戶主的標誌 |
| `encryptedZip` | JSON字串 | &quot;&quot; | Comcast公開加密的郵遞區號 |
| `typeID` | JSON字串 | 主要 | 標識用戶帳戶是主/次帳戶的標誌 |
| `primaryOID` | JSON字串 | &quot;uuidd1e19ec9-012c-124f-b520-acaf118d16a0&quot; | 家庭標識。 如果 `typeID` 為Primary，將包含 `userID` |
| hba_status | 布爾型 | &quot;true&quot; &quot;false&quot; | 一個布爾標誌，用於表示是否為特定整合啟用基於家庭的身份驗證 |
| 允許鏡像 | 布爾型 | &quot;true&quot; &quot;false&quot; | 指示此設備是否允許螢幕鏡像 |

>[!NOTE]
>
> **注：** 如果資料參數是加密的，則 **Zip鍵**，則元資料鍵的表示形式將是JSON字串，而不是陣列或對象。


**重要提示：** 程式設計師可用的實際用戶元資料取決於MVPD提供的內容。  必須與MVPD簽署法律協定，才能在生產環境中提供敏感用戶元資料（如zipcode）。

</br>


| 名稱 | 詳細資訊 | 需要加密 | 注釋 |
| --- | --- | --- | --- |
| 用戶ID | MVPD提供 | 否 | 這是隨後由Adobe散列並在媒體令牌和sendTrackingData()回調中公開的值。<br><br>本案的討論是出於歷史原因<br><br>此ID可以是家庭ID或子帳戶ID。 通常未指定，它只是與當時使用的登錄相關的ID（可以是主帳戶或子帳戶） |
| 上游用戶ID | 由MVPD提供，僅用於併發監視流 | 否 | 在跨MVPD和程式設計師站點和應用強制實施併發限制時，會使用此值。 <br><br>ID還可以包含併發監視策略<br><br>對於大多數MVPD，此值等於用戶ID |
| 家庭用戶ID | 由MVPD提供，主要用於家長控制流 | 否 | 允許程式設計師瞭解家庭與子帳戶使用情況的ID。<br><br>如果真的分級不可用，則有時會將其用作家長控制替代項（如果用戶已使用他們可以監視的家庭帳戶登錄，否則將不顯示分級內容）<br><br>在MVPD中，這種表示方式存在很多差異 — 家庭用戶ID、戶主ID、戶主旗等。 |
| 戶主 | 如果經常賬戶是戶主或不是戶主，則標誌 | 否 | 上 |
| 類型ID /主ID | 家庭帳戶標識符 | 否 | AT&amp;T家長的具體指標。<br><br>類型ID =標識用戶帳戶是主/次帳戶的標誌<br><br>主OID =家庭標識符。 如果TypeID為Primary，則將包含userID的值 |
| 最大評級 | 當前帳戶允許的最大評級 | 否 | 允許程式設計師篩選不適合帳戶的內容。<br><br>具有MPAA或VCHIP分級 |
| 通道向上 | 用戶包中可用的頻道清單 | 否 | 用於快速允許/從聚合多個網路的入口中刪除各種通道</br></br> *請注意，印前授權通常允許此用戶具有更大的靈活性，應改為使用* <br><br>OLCA規範允許在AuthN響應中將其作為AttributeStatement |
| HBA狀態 | 指示是否已通過HBA進行身份驗證 | 否 |  |
| 郵遞區號 | 用戶的帳單郵遞區號 | 是 | 用於廣播或體育活動<br><br>還可以提供AuthZ響應以進行快速更新<br><br>敏感資料，需要MVPD法律協定 |
| 加密的郵遞區號 | 用戶的帳單郵遞區號(Comcast) | 是 | 如上所述，但由Comcast加密 |
| 語言 | 用戶語言設定 | 否 | 用於根據用戶的首選項顯示消息 |
| 允許鏡像 | 指示此設備是否允許螢幕鏡像 | 否 |  |



## 可用元資料 {#available_metadata}

下表列出了Adobe Primetime驗證生態系統中用戶元資料的當前狀態：


|  | **法律&#x200B;**<br><br>**協定&#x200B;**<br><br>**已簽名（僅ZIP）** | **用戶ID **<br><br>**在AuthN上** | **Zipcode **<br><br>**在AuthN/Z上** | **評級&#x200B;**<br><br>**在AuthN/Z上** | **家庭&#x200B;**<br><br>**AuthN/Z上的ID** | **AuthN上的通道ID** | **AuthN家長** | **AuthN上的類型ID** | **AuthN上的主OID** | 語言 | 上游用戶ID **在AuthN上** | HBA狀態 | OnNet | 在首頁 | 允許在AuthZ上進行鏡像 | **注釋** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **正式名稱** | n/a | `userID` | `zip` | `maxRating` | `householdID` | `channelID` | 為 | 類型ID | 主OID | 語言 | 上游用戶ID | hba_status | 網上 | 在首頁 | 允許鏡像 | 1。對於AuthN — 必須更改OiosamlMetadataParser，以便所有解析器都啟用此新屬性 <br>2.  對於AuthZ — 沒有通用方法，因為授權實現是MVPD特定的 |
| **需要加密** | n/a | **否** | **是** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** |  |
| **敏感** | n/a | **否** | **是** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** |  |  |
| **AdobeIdP** | **是** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是** | **是** | **是** | **是** | **否** | **是** | **否** | **否** | **否** | **否** | 不需要法律協定，可以啟用。 |
| **同步** | **是** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是** | **是** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | **法律協定不涵蓋所有代理的MVPD。**   <br>這是對Synacor的一般支援 — 可能不會匯總到其所有MVPD。 |
| 碟 | **否** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | 與所有Synacor MVPD以及upstreamUserID共用同一清單。 |
| 孔卡斯特 | **否** | **是** | **否** | **是（僅限AuthZ）** | **是（僅限AuthZ）** | **否** | **否** | **否** | **否** | **否** | **是** | **是** | **否** | **否** | **否** |  |
| **AT&amp;T** | **是** | **是** | **是（僅限AuthN）** | **否** | **是（僅限AuthN）** | **否** | **否** | **是** | **是** | **否** | **是** | **否** | **否** | **否** | **否** | 簽署法律協定。 |
| **卡布萊維西** | **是** | **是** | **是（僅限AuthN）** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | 簽署法律協定。 |
| **宏達電** | **否** | **是** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| **馬西隆代理** | **是** | **是** | **是（僅限AuthN）** | **否** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | 簽署法律協定。 |
| **克利爾利普代理** | **是** | **是** | **是（僅限AuthN）** | **是（僅限AuthZ）** | **否** | **否** | **否** | **否** | **否** | **是** | **是** | **否** | **否** | **否** | **否** | 簽署法律協定。 |
| 羅傑斯 | **否** | **是** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| RCN | **是** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| 憲章 | **是** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| 威瑞森 | **否** | **是** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **是** | **否** | **否** | **否** |  |
| 東聯 | **否** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| 代理GLDS | **否** | **是** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| DTV | **是** | **是** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| 考克斯 | **否** | **是** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| 科切科 | **否** | **是** | **是（僅限AuthN）** | **否** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| 視頻管 | **否** | **是** | **是（僅限AuthN）** | **否** | **是*** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | 顯示與userID值相同的householdID |
| 頻譜 | **是** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **是** | **否** | **否** | **是** |  |
| **所有其他&#x200B;**<br><br>**MVPD** | **否** | **是** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | **尚未達成法律協定，敏感元資料無法用於生產。**  <br>對於所有MVPD，用戶ID都可用，無需額外工作。 |


隨著新類型的可用和添加到Adobe Primetime認證系統，用戶元資料類型清單將被擴展。

## 代碼示例 {#code_samples}

- [代碼示例1](#code_sample1)
- [代碼示例2(Mock getMetadata)](#code_sample2)


### 代碼示例1 {#code_sample1}

```
    // Assuming a reference to the AccessEnabler has been previously obtained and stored in the "ae" variable
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
      if(status ==1) {
        // User is authenticated, request metadata
        ae.getMetadata("zip");
        ae.getMetadata("maxRating");
      } else {
        ...
      }
    }
     
    // Implement the setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
      if(encrypted) {
        // The metadata value is encrypted
        // Needs to be decrypted by the programmer
         data = decrypt(data);
      }
      alert(key + "=" + data);
    }
```
 

### 代碼示例2(Mock getMetadata) {#code_sample2}

```
    // Assuming a reference to the AccessEnabler has been
    //   previously obtained and stored in the "ae" variable
     
    // Mock the getMetadata() method
    var aeMock = {
        getMetadata: function(key) {
          var data = null;
          // Set mock data based on the received key,
          // according to the format in the spec
          switch(key) {
            case 'zip': 
              data = [ "1235", "23456" ];
              break;
            case 'maxRating': 
              data = { "MPAA": "PG-13", "VCHIP": "TV-14" };
              break;
            default:
              break;
          }
          // Call the metadata status just like AccessEnabler does
          setMetadataStatus(key, false, data);
        }
     }
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
      if (status == 1) {
        // User is authenticated, request metadata using mock object
        aeMock.getMetadata("zip");
        aeMock.getMetadata("maxRating");
      } else {
        ...
      }
    }
     
    // Implement the  setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
      if (encrypted) {
        // The metadata value is encrypted, so it
        //   needs to be decrypted by the programmer
         data = decrypt(data);
      }
      alert(key + "=" + data);
    }
```
 

有關您特定平台的詳細資訊，或者要瞭解MVPD端如何處理用戶元資料，請參閱下面「相關資訊」中的相應連結。  

<!---

## Related Information {#related}

- ActionScript - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaData)
- JavaScript - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaData)
- iOS - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaStatus)
- Android - [getMetadata()](#getMetadata), [setMetadataStatus()](#setMetadaStatus)
- Clientless - [AuthN Metadata](#authn_metadata)
- [MVPD Integration Guide: User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
-->
