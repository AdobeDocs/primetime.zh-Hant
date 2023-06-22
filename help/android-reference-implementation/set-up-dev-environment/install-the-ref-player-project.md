---
description: TVSDK Primetime Reference是以TVSDK和AVE架構為基礎打造的Android應用程式。
title: 建立Primetime參考實作
exl-id: d2950f2b-06d7-4fc8-a031-5f058ce47545
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# 建立Primetime參考實作 {#build-the-primetime-reference-implementation}

TVSDK Primetime Reference是以TVSDK和AVE架構為基礎打造的Android應用程式。

若要在Eclipse中設定和建置Primetime參考專案：

1. 下載TVSDK Android zip檔案，並將其解壓縮至您記得位置的目錄中。
1. 啟動Eclipse。
1. 選取 **[!UICONTROL File]** > **[!UICONTROL Import]**.
1. 選取 **[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**.
1. 按一下 **[!UICONTROL Next]**.
1. 使用 **[!UICONTROL Browse]** 按鈕以填入 **[!UICONTROL Root Directory]** 目錄在下的欄位 [!DNL samples/PrimetimeReference/src] 解壓縮TVSDK Android zip檔案至該處。
1. 選取下列要匯入的專案： **[!UICONTROL appcompat]**， **[!UICONTROL PrimetimeReference]**.
1. 按一下 **[!UICONTROL Finish]**.
1. 選取  **[!UICONTROL Project]** > **[!UICONTROL Build Project]** 以建置專案。

   如果專案設定為自動建置，則不需要執行此步驟。
1. 如果要將測試專案包含在工作區中，請將測試專案與PrimetimeReference專案相關聯：
   1. 重複步驟3。 到6。
   1. 選取要匯入的專案： `PrimetimeReference\tests`.
   1. 按一下 **[!UICONTROL Finish]**.

      測試專案與CatalogActivity專案具有相依性，因此您需要將測試專案與CatalogActivity專案相關聯。
   1. 按一下右鍵 **[!UICONTROL tests]** 並選擇 **[!UICONTROL Properties]**.
   1. 選取 **[!UICONTROL Projects]** 索引標籤中的「Java建置路徑」下方。
   1. 按一下 **[!UICONTROL Add...]**
   1. 選取CatalogActivity。
   1. 按一下 **[!UICONTROL OK]** 以新增專案。
   1. 按一下 **[!UICONTROL OK]** 以結束「屬性」頁面。
   1. 選取  **[!UICONTROL Project]** > **[!UICONTROL Build Project]** 以建置專案。

      如果專案設定為自動建置，則不需要執行此步驟。
