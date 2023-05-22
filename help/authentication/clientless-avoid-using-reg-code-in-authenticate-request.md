---
title: 避免在/authenticate請求中使用'&'reg_code
description: 避免在/authenticate請求中使用'&'reg_code
exl-id: c0ecb6f9-2167-498c-8a2d-a692425b31c5
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# 避免在/authenticate請求中使用&#39;&amp;&#39;reg_code {#clientless-avoid-using-reg_code-in-authenticate-request}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>



## 問題

IE 9瀏覽器將「\®」解釋為特殊命令，並將其轉換為®。 

## 解釋

如果 `/authenticate` 請求的組成如下……

 

```
    <FQDN>authenticate? requestor_id=someRequestor&reg_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

...IE瀏覽器將按照如下方式進行解釋，並將以此格式發送到Adobe:

 

```
    <FQDN>authenticate?requestor_id=someRequestor&reg;_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

請求者\_id將解釋為univision®\_code=EKAFMFI，因為沒有「&amp;」，並且Adobe將找不到 `regCode` 參數，將令牌與關聯。  AuthN令牌有可能根本不會建立，在這種情況下 `/checkauthn` 呼叫將找不到任何令牌。



## 解決方案

以下選項之一應解決此問題：

1. 避免使用 `&reg_code` 其他查詢字串參數之間的參數。  將其移到請求URL中的第一個query-string參數，使請求URL如下所示：\
    

       &lt;fqdn>authenticate?reg_code =EKAFMFI&amp;requestor_id=someRequestor&amp;domain_name=someRequestor.com&amp;noflash=true&amp;mso_id=someMvpd&amp;redirect_url=someRequestor.redirect.url.html
   

   這樣， `&reg` 參數不會被錯誤解釋。

1. 規範化 `&reg_code` 使用 `&amp;reg_code`。

1. 如果AuthN令牌建立失敗，Adobe可以引入新功能，以響應身份驗證調用將錯誤代碼發回第2螢幕。
