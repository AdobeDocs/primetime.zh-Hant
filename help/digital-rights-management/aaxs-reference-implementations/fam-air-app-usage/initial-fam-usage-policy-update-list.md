---
title: 原則更新清單
description: 原則更新清單
copied-description: true
exl-id: 78078e95-775e-4c64-ab0f-d8bf644f3aee
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# 原則更新清單 {#policy-update-list}

您可以使用原則更新清單將原則變更傳達給授權伺服器。 如果在使用原則封裝內容後修改原則，最好讓授權伺服器知道原則的最新版本，以便使用版本發行授權。

若要第一次建立原則更新清單，請按一下 **[!UICONTROL Add policies]** 以檢視伺服器上所有可用的原則。 對於自用於封裝內容以來更新的任何原則，請選取 **[!UICONTROL update]** 選項按鈕。

如果您不想再使用原則來核發任何授權，而且原則已用來封裝內容，您可能會想要撤銷原則。 若要這麼做，請選取 **[!UICONTROL revoke]** 選項按鈕。 選取所需原則後，選擇 **[!UICONTROL Create Policy Update List]**. 名為的檔案 [!DNL PolicyUpdateList.dat] 將會儲存在 [!DNL Resources] 目錄。

若要修改現有的原則更新清單，請按一下 **[!UICONTROL Add policies]** 以檢視伺服器上所有可用的原則。 選擇要新增或撤銷的其他原則。 原則更新清單中的現有專案可以在畫面的上方區段中變更。 標示的原則 **[!UICONTROL updated]** 可變更為 **[!UICONTROL revoked]**，但一旦原則變成 **[!UICONTROL revoked]**，無法變更回 **[!UICONTROL updated]**.

完成所需的變更後，請選擇 **[!UICONTROL Create Policy Update List]**，以及 [!DNL PolicyUpdateList.dat] 檔案會重新產生。 如果原則已經在原則更新清單中，並且自上次產生清單以來已更新，則在再次產生原則更新清單時，將使用最新版本的原則。
