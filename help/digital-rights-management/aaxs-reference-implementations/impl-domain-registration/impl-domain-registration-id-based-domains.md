---
seo-title: 基於身份的域
title: 基於身份的域
uuid: 34cad19b-1adb-4e0c-ac59-50632f6988f7
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 基於身份的域 {#identity-based-domains}

在此使用案例中，每個已驗證的用戶都有自己的域，並允許一定數量的設備加入域。 要將此類型的域與引用實施一起使用，需要建立指定域註冊的策略。 指定網域伺服器URL的伺服器主機和連接埠，並指定需要使用者名稱／密碼驗證。

參考實現實現了以下域註冊邏輯：

1. 確定要分配給此用戶的域名。 網域名稱將從驗證 `namequalifier:username`Token中擷取**。 如果沒有驗證Token，則傳回錯誤DOM_AUTHENTICATION_REQUIRED(503)。
1. 查閱表格中的網域 `DomainServerInfo` 名稱。 如果找不到條目，請將條目插入表中（預設值是驗證要求，最大域成員資格=5）。
1. 檢查設備是否已向域註冊：

   1. 查找表中的域 `UserDomainMembership` 名。 對於找到的每個機器ID，請與請求中的機器ID比較。 如果這是新機器，請將條目添加到表 `UserDomainMembership` 中。 接著，在表格中尋找相符的 `UserDomainRefCount` 記錄。 如果此電腦GUID不存在條目，請添加記錄。

   1. 如果是新裝置且已達到最大會籍，則傳回錯誤DOM_LIMIT_REACHED(502)。

1. 在DomainKeys表格中查閱此網域的所有網域索引鍵。

   1. 如果 `DomainServerInfo` 指出需要轉換密鑰，請生成新密鑰對，將其保存在表中 `DomainKeys` （密鑰版本高於現有最高密鑰版本1），並重置中的「需要轉換密鑰」標誌 `DomainServerInfo`。

   1. 對於每個域密鑰，生成域憑據。

參考實現，實現了下列域註銷邏輯：

1. 確定要分配給此用戶的域名。 網域名稱將是namequalifier: *username* ，會從驗證Token中擷取。 如果沒有驗證Token，則傳回錯誤DOM_AUTHENTICATION_REQUIRED(503)。
1. 在表格中查閱請求的網 `DomainServerInfo` 域名。
1. 查閱表格中的網域 `UserDomainMembership` 名稱。 對於找到的每個機器ID，請與請求中的機器ID比較。 在表中查找相應的 `UserDomainRefCount` 條目。 如果找不到匹配項，則返回錯誤DEREG_DENIED(401)。

1. 如果這不是預覽請求，請從表格中刪除該 `UserDomainRefCount` 條目。 如果該表中沒有用於電腦的條目，請從中刪除該條目， `UserDomainMembership` 並在中設定「需要密鑰變換」標 `DomainServerInfo`志。

在這種使用情況下，允許每個用戶註冊少量的電腦，因此我們可以使用完整的電腦ID和方法來準 `matches()` 確電腦。 不過，由於使用者可在這部機器上註冊多次（透過不同瀏覽器中的多個AIR應用程式或播放器），因此伺服器也需要維持參考計數，以便正確計算取消註冊。 在放棄機器上的所有網域Token之前，無法將取消註冊視為完成。
