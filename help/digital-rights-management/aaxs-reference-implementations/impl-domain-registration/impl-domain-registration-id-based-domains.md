---
title: 基於身份的域
description: 基於身份的域
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---


# 基於身份的域{#identity-based-domains}

在此使用案例中，每個已驗證的用戶都有自己的域，並允許一定數量的設備加入域。 要將此類型的域與引用實施一起使用，需要建立指定域註冊的策略。 指定網域伺服器URL的伺服器主機和連接埠，並指定需要使用者名稱／密碼驗證。

參考實現實現了以下域註冊邏輯：

1. 確定要分配給此用戶的域名。 網域名稱將是* `namequalifier:username`*從驗證Token中擷取。 如果沒有驗證Token，則傳回錯誤DOM_AUTHENTICATION_REQUIRED(503)。
1. 在`DomainServerInfo`表格中查閱網域名稱。 如果找不到條目，請將條目插入表中（預設值是驗證要求，最大域成員資格=5）。
1. 檢查設備是否已向域註冊：

   1. 在`UserDomainMembership`表格中查閱網域名稱。 對於找到的每個機器ID，請與請求中的機器ID比較。 如果這是新機器，請將條目添加到`UserDomainMembership`表中。 接著，在`UserDomainRefCount`表格中尋找相符記錄。 如果此電腦GUID不存在條目，請添加記錄。

   1. 如果是新裝置且已達到最大會籍，則傳回錯誤DOM_LIMIT_REACHED(502)。

1. 在DomainKeys表格中查閱此網域的所有網域索引鍵。

   1. 如果`DomainServerInfo`指出需要轉換密鑰，請生成新密鑰對，將其保存在`DomainKeys`表中（密鑰版本高於現有最高密鑰版本1），並重置`DomainServerInfo`中的「需要轉換密鑰」標誌。

   1. 對於每個域密鑰，生成域憑據。

參考實現，實現了下列域註銷邏輯：

1. 確定要分配給此用戶的域名。 網域名稱為&#x200B;*namequalifier:username*，會從驗證Token中擷取。 如果沒有驗證Token，則傳回錯誤DOM_AUTHENTICATION_REQUIRED(503)。
1. 在`DomainServerInfo`表格中查閱請求的網域名稱。
1. 在`UserDomainMembership`表格中查閱網域名稱。 對於找到的每個機器ID，請與請求中的機器ID比較。 在`UserDomainRefCount`表中查找相應的條目。 如果找不到匹配項，則返回錯誤DEREG_DENIED(401)。

1. 如果這不是預覽請求，請從`UserDomainRefCount`表格中刪除項目。 如果該表中沒有該電腦的條目，請從`UserDomainMembership`中刪除該條目，並在`DomainServerInfo`中設定「需要密鑰變換」標誌。

在這種使用情況下，允許每個用戶註冊少量的電腦，因此我們可以使用完整的電腦ID和`matches()`方法來準確計算電腦。 不過，由於使用者可在這部機器上註冊多次（透過不同瀏覽器中的多個AIR應用程式或播放器），因此伺服器也需要維持參考計數，以便正確計算取消註冊。 在放棄機器上的所有網域Token之前，無法將取消註冊視為完成。
