---
description: 密碼加擾器實用程式為Adobe PrimetimeDRM伺服器加密受保護流配置檔案的密碼。
title: 密碼加擾器
exl-id: 9cedd3e5-01db-4ea9-bf23-8767987fc26c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 密碼加擾器 {#password-scrambler}

密碼加擾器實用程式為Adobe PrimetimeDRM伺服器加密受保護流配置檔案的密碼。

要運行擾碼器，請鍵入：

```
Scrambler.bat  
<i class="+ topic ph hi-d="" i "="">
  password 
</i class="+ topic>
```

或

```
java -jar libs/flashaccess-scrambler.jar  
<i class="+ topic ph hi-d="" i "="">
  password  
</i class="+ topic>
```

實用程式顯示以下消息：

```
Encrypted password:  
<i class="+ topic ph hi-d="" i "="">
  scrambled-password 
</i class="+ topic>
```

在中指定的所有密碼 [!DNL flashaccess-global.xml] 和 [!DNL flashaccess-tenant.xml] 檔案必須加密。

>[!NOTE]
>
>黃金時段DRM伺服器中用於受保護流的密碼加擾器實用程式不能與隨參考實施許可證伺服器提供的加擾器互換。
