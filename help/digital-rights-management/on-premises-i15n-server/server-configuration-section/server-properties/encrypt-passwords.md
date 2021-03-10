---
title: 加密密碼
description: 加密密碼
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '54'
ht-degree: 0%

---


# 加密密碼{#encrypt-passwords}

屬性檔案包含幾個不應以純文字檔案形式輸入的口令值。 使用以下命令加密這些值：

`java -jar adobe-flashaccess-i15n-setup.jar password`

此命令將輸出加密口令，然後在屬性檔案中使用該口令。

>[!NOTE]
>這不是用於加密許可證伺服器密碼的實用程式。

