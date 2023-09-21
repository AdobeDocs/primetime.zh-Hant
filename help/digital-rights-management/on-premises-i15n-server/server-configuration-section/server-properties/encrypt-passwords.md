---
title: 加密密碼
description: 加密密碼
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '54'
ht-degree: 0%

---

# 加密密碼{#encrypt-passwords}

屬性檔案包含數個密碼值，您不應該輸入為純文字。 使用下列命令加密這些值：

`java -jar adobe-flashaccess-i15n-setup.jar password`

這個命令將會輸出加密的密碼，然後您會在屬性檔案中使用這個密碼。

>[!NOTE]
>這不是用來加密授權伺服器密碼的公用程式。
