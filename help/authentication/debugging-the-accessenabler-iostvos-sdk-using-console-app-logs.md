---
title: 使用主控台應用程式記錄檔對AccessEnabler iOS/tvOS SDK除錯
description: 使用主控台應用程式記錄檔對AccessEnabler iOS/tvOS SDK除錯
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---


# 使用主控台應用程式記錄檔對AccessEnabler iOS/tvOS SDK除錯 {#debugging-the-accessenabler-iostvos-sdk-using-console-app-logs}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。


## 概述

本文檔的範圍是捕獲並呈現AccessEnabler的iOS/tvOS SDK日誌記錄機制的演變，以及一些使用控制台應用程式日誌調試AccessEnabler框架的有用詳細資訊。

## 記錄機制狀態

AccessEnabler iOS/tvOS日誌記錄機制的用途是發出有用的消息，以排除使用AccessEnabler框架的應用程式可能因此遇到的問題。

### AccessEnabler iOS/tvOS 3.5.0及更高版本

從AccessEnabler iOS/tvOS 3.5.0版開始，記錄機制會隨著變更引入下列改進：

* AccessEnabler框架使用Apple建議的 [OSLog](https://developer.apple.com/documentation/os/oslog) 實作。

* AccessEnabler框架引入了基於子系統篩選控制台應用日誌的功能： **com.adobe.pass.AccessEnabler**. SDK發出的所有訊息都屬於com.adobe.pass.AccessEnabler。

* AccessEnabler框架引入了根據Any（前置詞）篩選控制台應用日誌的功能： **[AccessEnabler]**. SDK發出的所有訊息都會加上前置詞 [AccessEnabler].

* AccessEnabler框架引入了根據類別篩選控制台應用日誌的功能： **偵錯**, **錯誤** 結合上述兩個條件的任一項：子系統或任何（前置詞）。

## 使用主控台應用程式記錄檔進行除錯

根據所調查的問題，您可能希望包括或排除AccessEnabler框架發出的日誌消息，因此，您可以在下面找到一些有用的詳細資訊，這些資訊可能有助於您在調查期間和使用控制台應用日誌。


### AccessEnabler iOS/tvOS 3.5.0及更高版本

#### 包括 {#including}

首先，為了能夠看到AccessEnabler框架發出的任何日誌消息 **必須** 選取主控台應用程式「動作」區段中的「包含資訊訊息」和「包含除錯訊息」，如下圖所示。

![](assets/include-info-debug-msg.png)


為了能夠調試AccessEnabler iOS/tvOS SDK和 **請參閱** AccessEnabler框架日誌可以：

* 在主控台應用程式中使用 **子系統** 選項，其等於下圖中的com.adobe.pass.AccessEnabler值。

![](assets/subsys-console-app.png)

* 在主控台應用程式中使用 **任何** 選項，其中包含
   [AccessEnabler] 值，如下圖所示。

![](assets/any-optn-console-app.png)

除了上述兩個條件，您也可以使用 **類別** 與 **子系統** 或 **任何（前置詞）** 顯式搜索 **偵錯** 或 **錯誤** AccessEnabler iOS/tvOS SDK發出的級別消息。

#### 排除

以便能夠對其他元件和 **排除** AccessEnabler框架日誌可以：

* 在主控台應用程式中使用 **子系統** 選項，其不等於com.adobe.pass.AccessEnabler值。
* 在主控台應用程式中使用 **任何** 選項，其中不包含 [AccessEnabler] 值。

## 回報問題

向Adobe Primetime驗證報告問題時，請考慮下列建議：

* 請嘗試提供重制步驟。
* 請嘗試提供發生問題的作業系統版本和裝置型號。
* 請嘗試提供遇到問題的AccessEnabler iOS/tvOS SDK版本。
* 請嘗試使用下列兩個選項之一，擷取並附加所有AccessEnabler iOS/tvOS SDK記錄訊息： [包括](#including) 區段。
