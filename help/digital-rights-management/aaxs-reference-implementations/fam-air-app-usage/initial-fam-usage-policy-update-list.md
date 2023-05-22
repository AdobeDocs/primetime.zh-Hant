---
title: 策略更新清單
description: 策略更新清單
copied-description: true
exl-id: 78078e95-775e-4c64-ab0f-d8bf644f3aee
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# 策略更新清單 {#policy-update-list}

可以使用策略更新清單將策略更改與許可證伺服器通信。 如果策略在用於打包內容後被修改，則希望許可證伺服器知道策略的最新版本，以便該版本可用於頒發許可證。

要首次建立策略更新清單，請按一下 **[!UICONTROL Add policies]** 查看伺服器上的所有可用策略。 對於自用於打包內容後已更新的任何策略，請選擇 **[!UICONTROL update]** 按鈕。

如果您不再希望使用策略來頒發任何許可證，並且該策略已用於打包內容，則可能希望撤消該策略。 為此，請選擇 **[!UICONTROL revoke]** 按鈕。 選擇所需策略後，選擇 **[!UICONTROL Create Policy Update List]**。 名為 [!DNL PolicyUpdateList.dat] 將保存在 [!DNL Resources] 目錄。

要修改現有策略更新清單，請按一下 **[!UICONTROL Add policies]** 查看伺服器上的所有可用策略。 選擇要添加或撤消的附加策略。 「策略更新清單」中的現有條目可以在螢幕的上半部分更改。 已標籤的策略 **[!UICONTROL updated]** 可能已更改為 **[!UICONTROL revoked]**&#x200B;但一旦策略 **[!UICONTROL revoked]**，無法將其更改回 **[!UICONTROL updated]**。

完成所需更改後，選擇 **[!UICONTROL Create Policy Update List]**&#x200B;的 [!DNL PolicyUpdateList.dat] 檔案。 如果策略已在策略更新清單中，且自上次生成清單後已更新，則當再次生成策略更新清單時，將使用策略的最新版本。
