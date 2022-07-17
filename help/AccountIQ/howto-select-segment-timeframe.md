---
title: 定義段和時間框架
description: 定義段和時間框架
source-git-commit: a23de698b073d271df9b04494ff59f5d5a194c9d
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# 定義段和時間框架 {#define-segment}

帳戶IQ中的所有分析或查看報告都從定義段和選擇評估時間範圍開始。 [段](/help/AccountIQ/product-concepts.md#segmet-def) 指符合您評估標準（訂閱MVPD和查看特定渠道）的所有訂閱者或查看者。

![](assets/segment-panel.png)

*圖：段和時間幀選擇*

在「帳戶IQ」中所有報告頁的頂部，有一個面板，用於通過選擇MVPD、渠道程式設計師以及粒度和時間框架來定義段。

## 段選擇 {#select-segment}

### 在段中選擇MVPD {#select-segment-mvpds}

從中選擇MVPD **段中的MVPD** 選項：

1. 按一下或點擊 **段中的MVPD** 下拉選項。

   >[!NOTE]
   >
   >**全部** 預設情況下會選擇行業MVPD。 從此處，可以選擇 **共用分數的前10個MVPD**。 **前10個MVPD（按用法）**。 **按帳戶列出的前10個MVPD**&#x200B;或單個MVPD。 但是，要選擇單個MVPD，需要取消選擇 **全部**。

1. 按一下或點擊所需的MVPD。

   通過取消選擇MVPD，可以從選定內容中刪除它。

1. 按一下或點擊 **應用選擇** 才能使選擇生效。 否則，您將放棄所做的選擇。

   >[!NOTE]
   >
   >如果選擇「隔離」模式，則不能選擇任何其他MVPD。

### 選擇段中的通道 {#select-segment-channels}

要從 **段內渠道** 選項：

1. 按一下或點擊 **段內渠道** 下拉選項。

   >[!NOTE]
   >
   >**全部** 預設情況下，您公司的程式設計師渠道是選定的。 要選擇單個頻道或程式設計師，必須先取消選擇 **全部**。

1. 按一下或點擊所需的頻道或程式設計師。

   中的頂級清單項 **段內渠道** 是 [程式](/help/AccountIQ/product-concepts.md#programmer-def) 公司和程式設計師名下的清單項目 [通道](/help/AccountIQ/product-concepts.md#channel-def)。 您可以在程式設計師下面選擇單個頻道，也可以選擇程式設計師，並且該程式設計師下面頻道的所有活動都包括在報告和圖形結果中。

   ![](assets/programmer-channels.png)

   *圖：通道選擇器中列出的程式設計師和通道*

   >[!IMPORTANT]
   >
   >在程式設計師下面選擇各個渠道的結果與選擇程式設計師的結果不同。
   >
   >
   >當您選擇單個渠道時，這些渠道的活動會在某些報告中單獨分解。 但是，當您選擇所有這些渠道的父程式設計師時，這些渠道的所有活動都會包括在內，但不會在報告中單獨進行細分。

1. 按一下或點擊 **應用選擇** 才能使選擇生效。

>[!NOTE]
>
>在MVPD或程式設計師下拉菜單中，不能選擇10個以上的項目。

### 取消選擇MVPD和通道 {#deselect-segment-mvpds-channels}

除了更改中的選擇 **段中的MVPD** 和 **段內渠道** 段選擇器，可以通過以下方式取消選擇先前選擇的MVPD和通道：

* 選擇 **刪除** 表徵圖。![刪除表徵圖](assets/remove-icon.png))。

* 您還可以使用 **清除選擇** 刪除所有先前選定的MVPD或通道。

![](assets/segment-panel-selection1.png)

*圖：在段和時間範圍面板中選定的MVPD和通道*

![](assets/segment-panel-selection.png)

*圖：在段和時間範圍面板中選定的MVPD和通道*

## 粒度和時間幀選擇 {#granularity-timeframe}

要選擇評估的時段，請執行以下操作：

1. 選擇 **粒度和時間幀** 日期選取器。

1. 選擇 **周** 或 **月** 從 **聚合方式** 選項來設定評估的粒度。

   ![](assets/granularity-timeframe-weekwise.png)

   *圖：要選擇「粒度」和「時間」的日期選取器*

1. 選擇粒度後，可使用向前或向後箭頭在時間上向前或向後移動。

1. 指定過去（基於所選粒度的月或周）的時段以進行評估。

1. 選擇 **應用選擇** 確保您的選擇生效。
