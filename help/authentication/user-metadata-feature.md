---
title: 使用者中繼資料功能
description: 使用者中繼資料功能
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 0%

---



# 使用者中繼資料 {#user-metadata}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

</br>
</br>

## 簡介 {#intro}

「使用者中繼資料」功能可讓程式設計人員存取由MVPD維護的不同類型使用者特定資料。  使用者中繼資料類型包括郵遞區號、父級評等、使用者ID等。  *使用者* 中繼資料是先前可用之擴充功能 *靜態* 中繼資料（驗證Token TTL、授權Token TTL和裝置ID）。


用戶元資料關鍵點：

- 在驗證和授權流程期間傳遞給程式設計師的應用程式
- 值會儲存在Token中
- 如果不同的MVPD以不同格式提供資料，則可以標準化值
- 某些參數可以使用程式設計師的密鑰（例如郵遞區號）進行加密
- 特定值可由Adobe透過組態變更使用

## 取得使用者中繼資料 {#obtaining}

程式設計師可通過AccessEnabler獲得用戶元資料 `getMetadata()` 函式和透過 `/usermetadata` 端點。  如需使用的詳細資訊，請參閱平台API檔案 `getMetadata()` 及其對應的回呼 `setMetadataStatus()` （或用於無用戶端API中使用的端點和參數）。

程式設計師通過為想要獲取的元資料類型提供鍵來獲取元資料： `getMetadata(key)`.  

傳回中繼資料的方式如下： `setMetadataStatus(key, encrypted, data)`:

| 參數 | 類型 | 說明 |
| ----------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `key` | 字串 | 指定請求的元資料類型 |
| `encrypted` | 布林值 | 表示是否加密「value」的布林值標幟。 如果此值為「true」，則「value」實際上會是實際值的JSON網頁加密表示法。 |
| `data` | 物件 | 包含中繼資料表示的JSON物件 |

 

資料參數的結構，值會因類型而異：

| 金鑰 | 值類型 | 範例 | 說明 |
| --- | --- | --- | --- |
| `zip` | JSON陣列 | \[&quot;77754&quot;, &quot;12345&quot;\] | 郵遞區號 |
| `householdID` | JSON字串 | 「1o7241p」 | 家庭識別碼。 如果MVPD不支援子帳戶，則會與 `userID` |
| `maxRating` | JSON物件 | { MPAA:&quot;NR&quot;, <br>  VCHIP:&quot;X&quot;  <br>  URL:&quot;http://manage.my/parental&quot; } | 用戶的最高父級評分 |
| `userID` | JSON字串 | 「1o7241p」 | 使用者識別碼。 若MVPD支援子帳戶，且使用者不是主要帳戶， `userID` 將不同於 `householdID`. |
| `channelID` | JSON陣列 | \[ &quot;channel-1&quot;, &quot;channel-2&quot; \] | 使用者有權檢視的管道清單 |
| `is_hoh` | JSON字串 | &quot;1&quot; | 用於標識用戶是否為戶主的標誌 |
| `encryptedZip` | JSON字串 | &quot;&quot; | Comcast會公開加密的郵遞區號 |
| `typeID` | JSON字串 | 主要 | 用於標識用戶帳戶是否為主/次帳戶的標誌 |
| `primaryOID` | JSON字串 | &quot;uuid1e19ec9-012c-124f-b520-acaf118d16a0&quot; | 家庭識別碼。 若 `typeID` 為主要，將包含 `userID` |
| hba_status | 布林值 | &quot;true&quot; &quot;false&quot; | 布林值標幟，表示是否針對特定整合啟用了首頁式驗證 |
| allowMirroring | 布林值 | &quot;true&quot; &quot;false&quot; | 指示是否允許此設備進行螢幕鏡像 |

>[!NOTE]
>
> **注意：** 若資料參數已加密， **郵遞區號**，則中繼資料索引鍵的表示將是JSON字串，而非陣列或物件。


**重要：** 程式設計師可用的實際用戶元資料取決於MVPD提供的內容。  必須先與MVPD簽署法律合約，敏感使用者中繼資料（例如zipcode）才能在生產環境中使用。

</br>


| 名稱 | 詳細資料 | 需要加密 | 註解 |
| --- | --- | --- | --- |
| 使用者ID | 如MVPD所提供 | 否 | 這是隨後依Adobe雜湊的值，會公開於媒體Token和sendTrackingData()回呼中。<br><br>此案例的雜湊是基於歷史原因而完成<br><br>此ID可以是家庭ID或子帳戶ID。 這通常未指定，而只是當時使用的登入相連結的ID（可能是主要帳戶或子帳戶） |
| 上游使用者ID | 由MVPD提供，僅用於併發監視流 | 否 | 在MVPD和程式設計人員網站和應用程式之間強制實施併發限制時，會使用此值。 <br><br>此ID也可包含併發監控原則<br><br>對於大部分的MVPD，此值等於使用者ID |
| 家庭用戶ID | 由MVPD提供，主要用於家長控制流程 | 否 | 允許程式設計師了解家庭與子帳戶使用情形的ID。<br><br>如果沒有真正的評等，有時候會以「家長控制」替代（如果使用者以可觀看的家庭帳戶登入，則無法顯示評等的內容）<br><br>MVPD的呈現方式有許多差異，例如家庭使用者ID、戶主ID、戶主旗標等。 |
| 戶主 | 如果經常賬戶是戶主，則發出信號 | 否 | 見上文 |
| 類型ID /主要ID | 家庭帳戶標識符 | 否 | AT&amp;T家長的具體指標。<br><br>類型ID =識別使用者帳戶是否為主要/次要帳戶的標幟<br><br>主OID =家庭標識符。 如果TypeID為Primary，則會包含userID的值 |
| 最高評分 | 經常帳戶的允許評級上限 | 否 | 允許程式設計師過濾出不適合帳戶的內容。<br><br>具有MPAA或VCHIP評等 |
| Channel Line Up | 使用者套件中可用的管道清單 | 否 | 用於快速允許/從聚合多個網路的入口中刪除各種通道</br></br> *請注意，預檢授權通常可讓此使用更具彈性，而應改用* <br><br>OLCA規範允許在AuthN響應中將其作為AttributeStatement |
| HBA狀態 | 指示是否通過HBA進行了身份驗證 | 否 |  |
| 郵遞區號 | 使用者的帳單郵遞區號 | 是 | 用於廣播或體育活動<br><br>也可隨AuthZ回應提供，以進行快速更新<br><br>敏感資料，需要MVPD法律協定 |
| 加密的郵遞區號 | 使用者的帳單郵遞區號(Comcast) | 是 | 如上，但由Comcast加密 |
| 語言 | 使用者語言設定 | 否 | 用於根據用戶首選項顯示消息 |
| 允許鏡像 | 指示是否允許此設備進行螢幕鏡像 | 否 |  |



## 可用中繼資料 {#available_metadata}

下表列出Adobe Primetime驗證生態系統中使用者中繼資料的目前狀態：


|  | **法律資訊&#x200B;**<br><br>**協定&#x200B;**<br><br>**已簽名（僅郵遞區號）** | **使用者ID **<br><br>**在AuthN上** | **Zipcode **<br><br>**在AuthN/Z上** | **評等&#x200B;**<br><br>**在AuthN/Z上** | **家庭&#x200B;**<br><br>**驗證N/Z上的ID** | **AuthN上的通道ID** | **AuthN戶主** | **AuthN上的類型ID** | **AuthN上的主OID** | 語言 | 上游使用者ID **在AuthN上** | HBA狀態 | OnNet | inHome | 允許在AuthZ上鏡像 | **附註** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **正式名稱** | n/a | `userID` | `zip` | `maxRating` | `householdID` | `channelID` | is_hoh | typeID | primaryOID | 語言 | upstreamUserID | hba_status | onNet | inHome | allowMirroring | 1.對於AuthN — 必須更改OiosamlMetadataParser，以便所有解析器都啟用此新屬性 <br>2.  針對AuthZ — 沒有通用方式，因為授權實作是MVPD專屬 |
| **需要加密** | n/a | **否** | **是** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** |  |
| **敏感** | n/a | **否** | **是** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** |  |  |
| **AdobeIdP** | **是** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是** | **是** | **是** | **是** | **否** | **是** | **否** | **否** | **否** | **否** | 不需要任何法律協定，可以啟用。 |
| **同步** | **是** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是** | **是** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | **法律協定未涵蓋所有代理的MVPD。**   <br>這是Syncor的一般支援，可能不會匯總至其所有MVPD。 |
| 碟 | **否** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | 與所有Syncor MVPD以及upstreamUserID共用相同的清單。 |
| 康卡斯特 | **否** | **是** | **否** | **是（僅限AuthZ）** | **是（僅限AuthZ）** | **否** | **否** | **否** | **否** | **否** | **是** | **是** | **否** | **否** | **否** |  |
| **AT&amp;T** | **是** | **是** | **是（僅限AuthN）** | **否** | **是（僅限AuthN）** | **否** | **否** | **是** | **是** | **否** | **是** | **否** | **否** | **否** | **否** | 已簽署法律協定。 |
| **卡布萊維申** | **是** | **是** | **是（僅限AuthN）** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | 已簽署法律協定。 |
| **HTC** | **否** | **是** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| **馬西隆代理** | **是** | **是** | **是（僅限AuthN）** | **否** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | 已簽署法律協定。 |
| **代理Clearleap** | **是** | **是** | **是（僅限AuthN）** | **是（僅限AuthZ）** | **否** | **否** | **否** | **否** | **否** | **是** | **是** | **否** | **否** | **否** | **否** | 已簽署法律協定。 |
| 羅傑斯 | **否** | **是** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| RCN | **是** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| 憲章 | **是** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| Verizon | **否** | **是** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **是** | **否** | **否** | **否** |  |
| 東連 | **否** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| 代理GLDS | **否** | **是** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| DTV | **是** | **是** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| 考克斯 | **否** | **是** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| 科熱科 | **否** | **是** | **是（僅限AuthN）** | **否** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| Videotron | **否** | **是** | **是（僅限AuthN）** | **否** | **是*** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | 使用與userID相同的值公開houselID |
| 光譜 | **是** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **是** | **否** | **否** | **是** |  |
| **所有其他&#x200B;**<br><br>**MVPD** | **否** | **是** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | **尚未達成法律協定，生產環境無法使用敏感中繼資料。**  <br>對於所有MVPD，使用者ID都可供使用，不需額外工作。 |


新類型可供使用並新增至Adobe Primetime驗證系統時，使用者中繼資料類型清單將會擴充。

## 程式碼範例 {#code_samples}

- [程式碼範例1](#code_sample1)
- [程式碼範例2(Mock getMetadata)](#code_sample2)


### 程式碼範例1 {#code_sample1}

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
 

### 程式碼範例2(Mock getMetadata) {#code_sample2}

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
 

如需您特定平台的詳細資訊，或若要深入了解MVPD端處理使用者中繼資料的方式，請參閱下方「相關資訊」中的適當連結。  

<!---

## Related Information {#related}

- ActionScript - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaData)
- JavaScript - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaData)
- iOS - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaStatus)
- Android - [getMetadata()](#getMetadata), [setMetadataStatus()](#setMetadaStatus)
- Clientless - [AuthN Metadata](#authn_metadata)
- [MVPD Integration Guide: User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
-->
