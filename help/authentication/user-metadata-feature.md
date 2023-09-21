---
title: 使用者中繼資料功能
description: 使用者中繼資料功能
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1649'
ht-degree: 0%

---

# 使用者中繼資料 {#user-metadata}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要Adobe的目前授權。 不允許未經授權的使用。

</br>
</br>

## 簡介 {#intro}

使用者中繼資料功能可讓程式設計師存取由MVPD維護的不同使用者特定資料型別。  使用者中繼資料型別包括郵遞區號、家長分級、使用者ID等。  *使用者* 中繼資料是先前可用之擴充功能 *靜態* 中繼資料（驗證權杖TTL、授權權杖TTL和裝置ID）。


使用者中繼資料關鍵點：

- 在驗證和授權流程期間傳遞給程式設計師的應用程式
- 值會儲存在權杖中
- 如果不同的MVPD提供不同格式的資料，則可標準化值
- 部分引數可使用程式設計人員的金鑰（例如郵遞區號）加密
- 特定值可透過設定變更由Adobe提供

## 取得使用者中繼資料 {#obtaining}

程式設計師可透過AccessEnabler使用使用者中繼資料 `getMetadata()` 函式並透過 `/usermetadata` 無使用者端API中的端點。  請參閱平台API檔案，瞭解使用的詳細資訊 `getMetadata()` 及其對應的回呼 `setMetadataStatus()` （或用於無使用者端API中使用的端點和引數）。

程式設計師為要取得的中繼資料型別提供索引鍵，以取得中繼資料： `getMetadata(key)`.

中繼資料的傳回方式如下： `setMetadataStatus(key, encrypted, data)`：

| 引數 | 型別 | 說明 |
| ----------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `key` | 字串 | 指定要求的中繼資料型別 |
| `encrypted` | 布林值 | 表示「value」是否已加密的布林值標幟。 如果這是「true」，則「value」實際上將會是JSON Web加密的實際值表示法。 |
| `data` | 物件 | 包含中繼資料表示的JSON物件 |



資料引數的結構，值會因型別而異：

| 索引鍵 | 值型別 | 範例 | 說明 |
| --- | --- | --- | --- |
| `zip` | JSON陣列 | \[&quot;77754&quot;, &quot;12345&quot;\] | 郵遞區號 |
| `householdID` | JSON字串 | 「1o7241p」 | 家庭識別碼。 如果MVPD不支援附屬帳戶，這將會與 `userID` |
| `maxRating` | json物件 | { MPAA： &quot;NR&quot;， <br>  VCHIP： &quot;X&quot;，  <br>  URL： &quot;http://manage.my/parental&quot; } | 使用者的父母分級上限 |
| `userID` | JSON字串 | 「1o7241p」 | 使用者識別碼。 在MVPD支援附屬帳戶，且使用者不是主帳戶的情況下， `userID` 將不同於 `householdID`. |
| `channelID` | JSON陣列 | \[&quot;channel-1&quot;， &quot;channel-2&quot; \] | 使用者有權檢視的管道清單 |
| `is_hoh` | JSON字串 | &quot;1&quot; | 可識別使用者是否為戶主的旗標 |
| `encryptedZip` | JSON字串 | &quot;&quot; | Comcast會公開加密的郵遞區號 |
| `typeID` | JSON字串 | 主要 | 識別使用者帳戶是否為主要/次要帳戶的旗標 |
| `primaryOID` | JSON字串 | 「uuidd1e19ec9-012c-124f-b520-acaf118d16a0」 | 家庭識別碼。 如果 `typeID` 是主要，將包含 `userID` |
| hba狀態 | 布林值 | &quot;true&quot; &quot;false&quot; | 表示是否為特定整合啟用家用驗證的布林值旗標 |
| allowMirroring | 布林值 | &quot;true&quot; &quot;false&quot; | 指出此裝置是否允許熒幕映象 |

>[!NOTE]
>
> **注意：** 如果資料引數已加密(這通常適用於 **zip金鑰**，則中繼資料索引鍵的表示形式會是JSON字串，而非陣列或物件。


**重要：** 程式設計師實際可用的使用者中繼資料取決於MVPD提供的內容。  在生產環境中提供敏感的使用者中繼資料（例如郵遞區號）之前，必須與MVPD簽署法律協定。

</br>


| 名稱 | 詳細資料 | 需要加密 | 註解 |
| --- | --- | --- | --- |
| 使用者ID | 由MVPD提供 | 否 | 此值接著會由Adobe進行雜湊處理，並公開於媒體權杖和sendTrackingData()回呼中。<br><br>在此案例中，雜湊的發生是出於歷史原因<br><br>此ID可以是家庭ID或子帳戶ID。 這通常不會指定，只是與當時使用的登入連結的ID （可以是主要帳戶或子帳戶） |
| 上游使用者ID | 由MVPD提供，僅用於並行監視流程 | 否 | 在MVPD和程式設計師網站與應用程式中強制實施並行限制時，會使用此值。 <br><br>ID也可以包含並行監視原則<br><br>對於大多數MVPD，此值等於使用者ID |
| 家庭使用者ID | 由MVPD提供，主要用於家長監護流程 | 否 | 可讓程式設計師瞭解家庭與子帳戶使用情況的ID。<br><br>如果無法取得真實的分級，則有時可將其用作「家長監護」的替代專案（如果使用者以他們可以觀看的家庭帳戶登入，否則不會顯示分級內容）<br><br>MVPD的呈現方式差異很大：家庭使用者ID、戶長ID、戶長旗標等。 |
| 戶長 | 表示目前帳戶是否為戶主的旗標 | 否 | 請參閱上文 |
| 型別ID /主要ID | 家庭帳戶識別碼 | 否 | AT&amp;T戶主專用指標。<br><br>型別ID =識別使用者帳戶是否為主要/次要帳戶的旗標<br><br>主要OID =家庭識別碼。 如果TypeID是Primary，將包含userID的值 |
| 最大評分 | 目前帳戶的最大允許評等 | 否 | 可讓程式設計師篩選掉不適合帳戶的內容。<br><br>具有MPAA或VCHIP評等 |
| 頻道排列 | 使用者封裝中可用的管道清單 | 否 | 用於從彙總多個網路的入口網站快速允許/移除各種管道</br></br> *請注意，預檢授權通常可讓此使用案例更靈活，並應改用* <br><br>OLCA規格允許將此作為AuthN回應中的AttributeStatement |
| HBA狀態 | 表示是否已透過HBA進行驗證 | 否 |     |
| 郵遞區號 | 使用者的帳單郵遞區號 | 是 | 用於廣播或體育賽事<br><br>也可以隨附AuthZ回應以快速更新<br><br>敏感資料，需要MVPD法律協定 |
| 加密的郵遞區號 | 使用者的帳單郵遞區號(Comcast) | 是 | 如上所示，但由Comcast加密 |
| 語言 | 使用者語言設定 | 否 | 用於根據使用者的偏好設定顯示訊息 |
| 允許映象 | 指出此裝置是否允許熒幕映象 | 否 |     |



## 可用的中繼資料 {#available_metadata}

下表列出Adobe Primetime驗證生態系統中使用者中繼資料的目前狀態：


|     | **法律&#x200B;**<br><br>**合約&#x200B;**<br><br>**已簽署（僅限zip）** | **使用者ID **<br><br>**於AuthN** | **郵遞區號&#x200B;**<br><br>**於驗證/Z** | **評等&#x200B;**<br><br>**於驗證/Z** | **家庭&#x200B;**<br><br>**AuthN/Z上的ID** | **AuthN上的管道ID** | **AuthN上的戶長** | **AuthN上的型別ID** | **AuthN上的主要OID** | 語言 | 上游使用者ID **於AuthN** | HBA狀態 | OnNet | inHome | 允許在AuthZ上映象 | **附註** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **正式名稱** | 不適用 | `userID` | `zip` | `maxRating` | `householdID` | `channelID` | is_hoh | typeID | primaryOID | 語言 | 上游使用者ID | hba狀態 | onNet | inHome | allowMirroring | 1.對於AuthN — 必須變更OiosamlMetadataParser，以便所有剖析器都啟用這個新屬性 <br>2.  對於AuthZ — 沒有一般方法，因為授權實作是MVPD特定的 |
| **需要加密** | 不適用 | **否** | **是** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** |     |
| **敏感** | 不適用 | **否** | **是** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** |     |     |
| **AdobeIdP** | **是** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是** | **是** | **是** | **是** | **否** | **是** | **否** | **否** | **否** | **否** | 不需要法律協定，可以啟用。 |
| **Synacor** | **是** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是** | **是** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | **法律協定未涵蓋所有代理的MVPD。**   <br>這是對Synacor的一般支援 — 可能不會彙總到其所有MVPD。 |
| 碟子 | **否** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | 與所有Synacor MVPD共用相同的清單，加上upstreamUserID。 |
| Comcast | **否** | **是** | **否** | **是（僅限AuthZ）** | **是（僅限AuthZ）** | **否** | **否** | **否** | **否** | **否** | **是** | **是** | **否** | **否** | **否** |     |
| **AT&amp;T** | **是** | **是** | **是（僅限AuthN）** | **否** | **是（僅限AuthN）** | **否** | **否** | **是** | **是** | **否** | **是** | **否** | **否** | **否** | **否** | 已簽署法律合約。 |
| **Cablevision** | **是** | **是** | **是（僅限AuthN）** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | 已簽署法律合約。 |
| **宏達國際電子** | **否** | **是** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |     |
| **Proxy Masslon** | **是** | **是** | **是（僅限AuthN）** | **否** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | 已簽署法律合約。 |
| **Proxy Clearleap** | **是** | **是** | **是（僅限AuthN）** | **是（僅限AuthZ）** | **否** | **否** | **否** | **否** | **否** | **是** | **是** | **否** | **否** | **否** | **否** | 已簽署法律合約。 |
| 羅傑斯 | **否** | **是** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |     |
| RCN | **是** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |     |
| 憲章 | **是** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |     |
| Verizon | **否** | **是** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **是** | **否** | **否** | **否** |     |
| 東連結 | **否** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |     |
| Proxy GLDS | **否** | **是** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |     |
| DTV | **是** | **是** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |     |
| COX | **否** | **是** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |     |
| Cogeco | **否** | **是** | **是（僅限AuthN）** | **否** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |     |
| Videotron | **否** | **是** | **是（僅限AuthN）** | **否** | **是*** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | 公開householdID與userID的值相同 |
| 頻譜 | **是** | **是** | **是（僅限AuthN）** | **是（僅限AuthN）** | **是（僅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **是** | **否** | **否** | **是** |     |
| **所有其他&#x200B;**<br><br>**MVPDs** | **否** | **是** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | **尚無法律協定，敏感中繼資料不適用於生產。**  <br>對於所有MVPD，使用者ID不需額外工作即可取得。 |


當新的型別可用並新增到Adobe Primetime驗證系統中，使用者中繼資料型別的清單將會展開。

## 程式碼範例 {#code_samples}

- [程式碼範例1](#code_sample1)
- [程式碼範例2 （模擬getMetadata）](#code_sample2)


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


### 程式碼範例2 （模擬getMetadata） {#code_sample2}

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

<!---

For details on your particular platform, or to gain some insight into how User Metadata is processed on the MVPD side, see the appropriate link in Related Information below.  

## Related Information {#related}

- ActionScript - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaData)
- JavaScript - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaData)
- iOS - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaStatus)
- Android - [getMetadata()](#getMetadata), [setMetadataStatus()](#setMetadaStatus)
- Clientless - [AuthN Metadata](#authn_metadata)
- [MVPD Integration Guide: User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
-->
