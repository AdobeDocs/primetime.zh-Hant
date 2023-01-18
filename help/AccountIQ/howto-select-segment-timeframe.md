---
title: 定義區段和時間範圍
description: 定義區段和時間範圍
exl-id: 86fe010d-3202-4ce2-b803-ff44f5538d7e
source-git-commit: c17fb003d8c8103aac36696f696c9e3c7bb83c4f
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# 定義區段和時間範圍 {#define-segment}

帳戶IQ中的所有分析或檢視報表，都從定義區段和選取評估時間範圍開始。 [區段](/help/AccountIQ/product-concepts.md#segmet-def) 是指符合您評估條件（訂閱MVPD並檢視特定頻道）的所有訂閱者或檢視者。

![](assets/segment-panel.png)

*圖：區段和時間範圍選取*

在「帳戶IQ」的所有報表頁面頂端，有一個面板可讓您選取MVPD、頻道程式設計人員、粒度和時間範圍來定義區段。

## 區段選取 {#select-segment}

### 在區段中選取MVPD {#select-segment-mvpds}

從中選擇MVPD **區段中的MVPD** 選項：

1. 按一下或點選 **區段中的MVPD** 下拉式選項。

   >[!NOTE]
   >
   >**全部** 依預設會選取產業MVPD。 從此處，您可以選取 **前10個以共用分數顯示的MVPD**, **前10個MVPD（依使用量）**, **前10個MVPD（依帳戶）**，或個別MVPD。 不過，若要選取個別MVPD，您必須取消選取 **全部**.

1. 按一下或點選所需的MVPD。

   您可以取消選取MVPD，從選取範圍中移除MVPD。

1. 按一下或點選 **套用選取項目** 讓您的選擇生效。 否則，您會鬆開所做的選取。

   >[!NOTE]
   >
   >如果選擇「隔離」模式，則不能選擇其他MVPD。

### 在區段中選取管道 {#select-segment-channels}

要從 **區段中的管道** 選項：

1. 按一下或點選 **區段中的管道** 下拉式選項。

   >[!NOTE]
   >
   >**全部** 預設會選取您公司的程式設計師管道。 要選擇單個通道或程式設計師，必須先取消選擇 **全部**.

1. 按一下或點選所需的頻道或程式設計人員。

   中的頂層清單項目 **區段中的管道** 為 [程式設計師](/help/AccountIQ/product-concepts.md#programmer-def) 公司和程式設計師名下的清單項目是 [頻道](/help/AccountIQ/product-concepts.md#channel-def). 您可以在程式設計師下選擇單個通道，也可以選擇程式設計師，並且該程式設計師下的通道的所有活動都包含在報表和圖形結果中。

   ![](assets/programmer-channels.png)


   *圖：頻道選擇器中列出的程式設計師和頻道*

   >[!IMPORTANT]
   >
   >在程式設計師下選擇單個渠道的結果與選擇程式設計師的結果不同。
   >
   >
   >當您選取個別管道時，這些管道的活動在某些報表中會個別劃分。 但是，當您選擇所有這些管道的父程式設計師時，這些管道的所有活動都將包括在內，但不會在報表中單獨劃分。

1. 按一下或點選 **套用選取項目** 讓您的選擇生效。

>[!NOTE]
>
>在MVPD或程式設計員下拉菜單中，不能選擇超過10個項。

### 取消選擇MVPD和通道 {#deselect-segment-mvpds-channels}

除了在 **區段中的MVPD** 和 **區段中的管道** 區段選取器中，您可以透過下列方式，取消選取先前選取的MVPD和頻道：

* 選取 **移除** 圖示(![移除圖示](assets/remove-icon.png))，以取得區段選取器下方顯示的所選MVPD和頻道名稱。

* 您也可以使用 **清除選取項目** 移除所有先前選取的MVPD或通道。

![](assets/segment-panel-selection.png)

*圖：區段和時間範圍面板中選取的MVPD和頻道*

## 粒度和時間範圍選擇 {#granularity-timeframe}

要選擇評估時段，請執行以下操作：

1. 選取 **粒度和時間範圍** 日期選擇器。

1. 選取 **周** 或 **月** 從 **匯總依據** 選項，設定評估的粒度。

   ![](assets/granularity-timeframe-weekwise.png)


   *圖：選擇「粒度」和「時間範圍」的日期選擇器*

1. 選取粒度後，您可以使用向前或向後箭頭來及時向前或向後移動。

1. 指定以往的時段（根據選取的粒度，以月或周為單位）以供評估。

1. 選擇 **應用選擇** 以確保您的選取生效。
