---
description: 「TVSDK Primetime參考」是以TVSDK和AVE架構為基礎的Android應用程式。
title: 建立Primetime參考實作
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 1%

---


# 建立Primetime參考實作{#build-the-primetime-reference-implementation}

「TVSDK Primetime參考」是以TVSDK和AVE架構為基礎的Android應用程式。

若要在Eclipse中設定和建立Primetime參考專案：

1. 下載TVSDK Android zip檔案，並將它解壓縮至您會記得的目錄。
1. 啟動Eclipse。
1. 選擇&#x200B;**[!UICONTROL File]** > **[!UICONTROL Import]**。
1. 選擇&#x200B;**[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**。
1. 按一下 **[!UICONTROL Next]**.
1. 使用&#x200B;**[!UICONTROL Browse]**&#x200B;按鈕，在&#x200B;**[!UICONTROL Root Directory]**&#x200B;欄位中填入您解壓縮TVSDK Android zip檔案的[!DNL samples/PrimetimeReference/src]下方的目錄。
1. 選擇要導入的以下項目：**[!UICONTROL appcompat]**、**[!UICONTROL PrimetimeReference]**。
1. 按一下 **[!UICONTROL Finish]**.
1. 選擇&#x200B;**[!UICONTROL Project]** > **[!UICONTROL Build Project]**&#x200B;以構建項目。

   如果將項目設定為自動生成，則不需要此步驟。
1. 如果您想要在工作區中包含測試專案，請將測試專案與PrimetimeReference專案建立關聯：
   1. 重複步驟3。 到6號。
   1. 選擇要導入的以下項目：`PrimetimeReference\tests`。
   1. 按一下 **[!UICONTROL Finish]**.

      測試項目依賴於CatalogActivity項目，因此您需要將測試項目與CatalogActivity項目關聯。
   1. 按一下右鍵&#x200B;**[!UICONTROL tests]**&#x200B;並選擇&#x200B;**[!UICONTROL Properties]**。
   1. 在「Java Build Path」（Java構建路徑）下選擇&#x200B;**[!UICONTROL Projects]**&#x200B;頁籤。
   1. 按一下 **[!UICONTROL Add...]**
   1. 選擇目錄活動。
   1. 按一下&#x200B;**[!UICONTROL OK]**&#x200B;添加項目。
   1. 按一下&#x200B;**[!UICONTROL OK]**&#x200B;退出「屬性」頁。
   1. 選擇&#x200B;**[!UICONTROL Project]** > **[!UICONTROL Build Project]**&#x200B;以構建項目。

      如果將項目設定為自動生成，則不需要此步驟。
