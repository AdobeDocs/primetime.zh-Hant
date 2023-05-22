---
title: 使用控制台應用日誌調試AccessEnableriOS/tvOS SDK
description: 使用控制台應用日誌調試AccessEnableriOS/tvOS SDK
exl-id: 0dad325e-db15-4ea0-a87a-75409eaf8d46
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 使用控制台應用日誌調試AccessEnableriOS/tvOS SDK {#debugging-the-accessenabler-iostvos-sdk-using-console-app-logs}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。


## 概述

本文檔的範圍是捕獲並演示AccessEnabler的iOS/tvOS SDK日誌記錄機制的演變，以及使用Console應用日誌調試AccessEnabler框架的一些有用詳細資訊。

## 日誌記錄機制狀態

AccessEnableriOS/tvOS日誌記錄機制的目的是發出有用的消息，用於排除使用AccessEnabler框架的應用程式可能因此遇到的問題。

### AccessEnableriOS/tvOS 3.5.0及更高版本

從AccessEnableriOS/tvOS 3.5.0版開始，日誌機制在更改時引入了以下改進：

* AccessEnabler框架使用Apple建議的 [OSLog](https://developer.apple.com/documentation/os/oslog) 執行。

* AccessEnabler框架引入了基於以下子系統篩選控制台應用日誌的功能： **com.adobe.pass.AccessEnabler**。 SDK發出的所有消息都是com.adobe.pass.AccessEnabler的一部分。

* AccessEnabler框架引入了基於任何（前置詞）篩選控制台應用日誌的功能： **[AccessEnabler]**。 SDK發出的所有消息都帶前置詞 [AccessEnabler]。

* AccessEnabler框架引入了基於類別篩選控制台應用程式日誌的功能： **調試**。 **錯誤** 與上述兩項標準中的任何一項結合：子系統或任意（前置詞）。

## 使用Console應用日誌調試

根據所調查的問題，您可能希望包括或排除AccessEnabler框架發出的日誌消息，因此您可以在下面找到一些有用的詳細資訊，這些資訊可能在調查期間和使用Console應用日誌時對您有所幫助。


### AccessEnableriOS/tvOS 3.5.0及更高版本

#### 包括 {#including}

首先，為了能夠查看AccessEnabler框架發出的任何日誌消息 **必須** 在Console應用的「操作」部分選擇「包括資訊消息」和「包括調試消息」，如下圖所示。

![](assets/include-info-debug-msg.png)


為了能夠調試AccessEnableriOS/tvOS SDK和 **見** AccessEnabler框架日誌，您可以：

* 在Console應用中使用 **子系統** 選項，與下圖中的com.adobe.pass.AccessEnabler值相等。

![](assets/subsys-console-app.png)

* 在Console應用中使用 **任意** 的子菜單。
   [AccessEnabler] 值，如下圖所示。

![](assets/any-optn-console-app.png)

在上述兩個條件旁邊，您還可以使用 **類別** 選項 **子系統** 或 **任意（前置詞）** 要顯式搜索 **調試** 或 **錯誤** AccessEnableriOS/tvOS SDK發出的級別消息。

#### 排除

以便能夠更好地調試其他元件和 **排除** AccessEnabler框架日誌，您可以：

* 在Console應用中使用 **子系統** 選項，該選項不等於com.adobe.pass.AccessEnabler值。
* 在Console應用中使用 **任意** 不包含 [AccessEnabler] 值。

## 報告問題

向Adobe Primetime驗證報告問題時，請考慮以下建議：

* 請嘗試提供複製步驟。
* 請嘗試提供發生問題的作業系統版本和設備型號。
* 請嘗試提供遇到此問題的AccessEnableriOS/tvOS SDK版本。
* 請嘗試使用中提供的兩個選項之一捕獲並附加所有AccessEnableriOS/tvOS SDK日誌記錄消息 [包括](#including) 的子菜單。
