---
title: 策略更新清單
description: 策略更新清單
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# 策略更新清單{#policy-update-list}

您可以使用「策略更新清單」將策略更改通知給許可證伺服器。 如果原則在用來封裝內容後被修改，則希望授權伺服器知道該原則的最新版本，以便使用該版本來發行授權。

要首次建立策略更新清單，請按一下&#x200B;**[!UICONTROL Add policies]**&#x200B;以查看伺服器上的所有可用策略。 對於自使用策略來包裝內容以來已更新的策略，請選擇&#x200B;**[!UICONTROL update]**&#x200B;單選按鈕。

如果您不想再使用原則來核發任何授權，而原則已用來封裝內容，則可能希望撤銷原則。 要執行此操作，請選擇&#x200B;**[!UICONTROL revoke]**&#x200B;單選按鈕。 選擇所需策略後，選擇&#x200B;**[!UICONTROL Create Policy Update List]**。 名為[!DNL PolicyUpdateList.dat]的檔案將保存在[!DNL Resources]目錄中。

要修改現有策略更新清單，請按一下&#x200B;**[!UICONTROL Add policies]**&#x200B;查看伺服器上的所有可用策略。 選擇要添加或撤銷的其他策略。 「策略更新清單」中的現有條目可以在螢幕的上半部分進行更改。 標籤為&#x200B;**[!UICONTROL updated]**&#x200B;的策略可以更改為&#x200B;**[!UICONTROL revoked]**，但一旦策略為&#x200B;**[!UICONTROL revoked]**，則不能將其更改回&#x200B;**[!UICONTROL updated]**。

完成所需的更改後，選擇&#x200B;**[!UICONTROL Create Policy Update List]** ，然後重新生成[!DNL PolicyUpdateList.dat]檔案。 如果策略已在策略更新清單中且自上次生成清單後更新，則當再次生成策略更新清單時，將使用策略的最新版本。
