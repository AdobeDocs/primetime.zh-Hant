---
title: 加密密碼
description: 加密密碼
copied-description: true
exl-id: 97b78e00-e5e3-4a9d-8eab-fcf96d3b1219
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '54'
ht-degree: 0%

---

# 加密密碼{#encrypt-passwords}

屬性檔案包含數個密碼值，您不應該輸入為純文字。 使用以下命令加密這些值：

`java -jar adobe-flashaccess-i15n-setup.jar password`

此命令將輸出加密的密碼，然後您將其用於屬性檔案中。

>[!NOTE]
>這不是用來加密授權伺服器密碼的公用程式。
