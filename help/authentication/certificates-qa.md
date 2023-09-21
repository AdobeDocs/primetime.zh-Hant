---
title: 憑證問答
description: 憑證問答
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 憑證問答 {#certificates-q}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要Adobe的目前授權。 不允許未經授權的使用。

</br>

**問題1：** 是否可以在iOS和Android之間註冊憑證？

**答：** iOS和Android的憑證在目前設定中相同。 原生憑證可用於兩種平台。

</br>

**第2季：** 相同的iOS憑證可以當做生產和中繼環境的主要和備份憑證嗎？ 如果不建議使用，您可以提供說明嗎？

**答：** 設定與主要和備份憑證相同的憑證沒有意義。 我們擁有主要和備份憑證的概念，因此我們可以為程式設計師設定多個憑證，以備主要憑證過期或被撤銷時使用。 擁有備份憑證可讓程式設計師有時間變更主要憑證，而不會影響發行環境。 但您可以對生產設定檔和中繼設定檔使用相同的一組主要和備份憑證。

</br>

**問題3：** 使用新彈性TempPass的網頁是否需要新的憑證？

**答：** 憑證（以及任何憑證）是在Media Company &amp; Programmer層級設定。 FlexibleTempPass是MVPD，您不需要為其設定任何憑證，因此，如果您整合現有程式設計師與彈性TempPass，將會使用已在程式設計師/媒體公司層級設定的憑證。
