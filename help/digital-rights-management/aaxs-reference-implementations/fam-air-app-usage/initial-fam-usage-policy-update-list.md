---
seo-title: 策略更新清單
title: 策略更新清單
uuid: ecc74b66-5b53-4ec3-9641-8b78929e2932
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 策略更新清單 {#policy-update-list}

您可以使用「策略更新清單」將策略更改通知給許可證伺服器。 如果原則在用來封裝內容後被修改，則希望授權伺服器知道該原則的最新版本，以便使用該版本來發行授權。

要首次建立策略更新清單，請按一下以查 **[!UICONTROL Add policies]** 看伺服器上的所有可用策略。 對於自使用策略來包裝內容以來已更新的策略，請選擇單選按鈕 **[!UICONTROL update]** 。

如果您不想再使用原則來核發任何授權，而原則已用來封裝內容，則可能希望撤銷原則。 若要這麼做，請選取選 **[!UICONTROL revoke]** 項按鈕。 選擇所需策略後，選擇 **[!UICONTROL Create Policy Update List]**。 名為的文 [!DNL PolicyUpdateList.dat] 件將保存在「目 [!DNL Resources] 錄」中。

要修改現有策略更新清單，請按一下以 **[!UICONTROL Add policies]** 查看伺服器上的所有可用策略。 選擇要添加或撤銷的其他策略。 「策略更新清單」中的現有條目可以在螢幕的上半部分進行更改。 標籤的策略 **[!UICONTROL updated]** 可以更改為 **[!UICONTROL revoked]**，但一旦策略 **[!UICONTROL revoked]**&#x200B;被更改為，則不能將其更改為 **[!UICONTROL updated]**。

完成所需的更改後，選擇 **[!UICONTROL Create Policy Update List]**&#x200B;並重新生 [!DNL PolicyUpdateList.dat] 成檔案。 如果策略已在策略更新清單中且自上次生成清單後更新，則當再次生成策略更新清單時，將使用策略的最新版本。
