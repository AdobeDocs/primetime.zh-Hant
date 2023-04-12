---
title: 訂閱者區段和時間範圍
description: 定義同類群組或選取訂閱者區段，以評估帳戶共用的可能性和通道檢視器的模式，以在帳戶IQ中使用圖形工具和報表。
exl-id: c38cde37-70d9-486d-b8d0-7c1cbd2baf2e
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# 訂閱者區段和時間範圍 {#cohorts-segments}

登入帳戶IQ時，頂端會有一個面板可讓您定義訂閱者 [區段](/help/AccountIQ/product-concepts.md#segment-segmet-def) 篩選檢視報表的結果，以供訂閱者共用行為和模式使用。

<!--![](assets/segment-timeframe-panel.png)-->

+++程式設計師的段選擇面板

![](assets/segment-panel-programmer.png)

<!--![](assets/filter-panel.png)-->

下列下拉式清單選項可用來定義區段：

**區段中的MVPD**

此 **區段中的MVPD** 選取器可讓您選擇 [MVPD](/help/AccountIQ/product-concepts.md#mvpd-def) （個人或群組），您要檢視其訂閱者的帳戶共用報表。

在此選取器中，除了選取個別MVPD外，您也可以選取下列群組：

* [前10個以共用分數顯示的MVPD](/help/AccountIQ/product-concepts.md#top-mvpds-def)

* [前10個MVPD（依使用量）](/help/AccountIQ/product-concepts.md#top-mvpds-def)

* [前10個MVPD（依帳戶）](/help/AccountIQ/product-concepts.md#top-mvpds-def)

* [隔離模式](/help/AccountIQ/isolation-mode.md)

**區段中的管道**

當您以程式設計師使用者身分登入時，您可以選取通道以檢視其帳戶共用分析。 使用 **區段中的管道** 下拉式選項，選取貴組織中的個別或多個管道。

+++

+++MVPD的區段選取面板

![](assets/segment-panel-mvpd.png)

下列下拉式清單選項可用來定義區段：

**區段中的管道**

此 **區段中的管道** 選取器可讓您進一步縮小篩選器，以選取與所選MVPD對應的頻道。

* [共用分數前10名程式設計師](/help/AccountIQ/product-concepts.md#top-mvpds-def)

* [前10名程式設計師（按使用情況）](/help/AccountIQ/product-concepts.md#top-mvpds-def)

* [前10名程式設計師（按帳戶）](/help/AccountIQ/product-concepts.md#top-mvpds-def)

**區段中的MVPD**

以MVPD使用者身分登入時，您的名稱會顯示在 **區段中的MVPD**.

+++




<!--For example, you can define your segment as the "subscribers of the MVPD A that watched the channels X, Y, and Z".-->



## 粒度和時間範圍 {#granularity-timeframe}

此 **粒度和時間範圍** 選取器可讓您指定要檢視訂閱者共用行為的日期、持續時間或時間大小。

![粒度和時間範圍](assets/granularity-timeframe-weekwise.png)

因此，使用這些控制項，您可以將問題陳述式定義為「在5月觀看頻道X、Y和Z的MVPD A的訂閱者」。

