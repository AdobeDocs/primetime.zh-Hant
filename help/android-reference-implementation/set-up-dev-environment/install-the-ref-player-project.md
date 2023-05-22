---
description: TVSDK黃金時段參考是圍繞TVSDK和AVE框架構建的Android應用程式。
title: 構建黃金時段參考實現
exl-id: d2950f2b-06d7-4fc8-a031-5f058ce47545
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# 構建黃金時段參考實現 {#build-the-primetime-reference-implementation}

TVSDK黃金時段參考是圍繞TVSDK和AVE框架構建的Android應用程式。

要在Eclipse中設定和構建Mighine Reference項目：

1. 下載TVSDK Android zip檔案，並將其解壓縮到您將記住的某個位置的目錄中。
1. 啟動Eclipse。
1. 選擇 **[!UICONTROL File]** > **[!UICONTROL Import]**。
1. 選擇 **[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**。
1. 按一下 **[!UICONTROL Next]**。
1. 使用 **[!UICONTROL Browse]** 按鈕 **[!UICONTROL Root Directory]** 的 [!DNL samples/PrimetimeReference/src] 解壓TVSDK Android zip檔案。
1. 選擇要導入的以下項目： **[!UICONTROL appcompat]**。 **[!UICONTROL PrimetimeReference]**。
1. 按一下 **[!UICONTROL Finish]**。
1. 選擇  **[!UICONTROL Project]** > **[!UICONTROL Build Project]** 來構建項目。

   如果將項目設定為自動生成，則無需執行此步驟。
1. 如果要在工作區中包括test項目，請將test項目與MighineReference項目關聯：
   1. 重複步驟3。 到6
   1. 選擇要導入的以下項目： `PrimetimeReference\tests`。
   1. 按一下 **[!UICONTROL Finish]**。

      test項目對CatalogActivity項目具有依賴關係，因此您需要將test項目與CatalogActivity項目關聯。
   1. 按一下右鍵 **[!UICONTROL tests]** 選擇 **[!UICONTROL Properties]**。
   1. 選擇 **[!UICONTROL Projects]** 頁籤。
   1. 按一下 **[!UICONTROL Add...]**
   1. 選擇目錄活動。
   1. 按一下 **[!UICONTROL OK]** 的子菜單。
   1. 按一下 **[!UICONTROL OK]** ，可退出「屬性」頁。
   1. 選擇  **[!UICONTROL Project]** > **[!UICONTROL Build Project]** 來構建項目。

      如果將項目設定為自動生成，則無需執行此步驟。
