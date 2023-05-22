---
title: 用於打包內容和建立撤消清單的命令行工具
description: 用於打包內容和建立撤消清單的命令行工具
copied-description: true
exl-id: 34305dab-a2f0-41c2-9a59-3261e8dea7e2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# 用於打包內容和建立撤消清單的命令行工具 {#command-line-tools-for-packaging-content-revocation-lists}

該參考實現包括以下命令行工具：

* 策略管理器：用於建立和管理策略的工具
* 策略更新清單管理器：用於建立和查看策略更新清單的工具
* 吊銷清單管理器：用於建立和查看吊銷清單的工具
* 介質打包器：用於建立加密FLV和F4V檔案的工具
* AIR發佈者ID
* 實用程式許可證生成器
* 許可證嵌入器

## 要求 {#requirements}

使用參考實現中可用的命令行工具的要求如下：

* 所有命令行工具都需要Java 1.5或更高版本。
* 由Adobe頒發的打包程式和許可證伺服器憑據（證書和密碼）。 您需要憑據來加密和簽名視頻檔案、簽署策略更新和吊銷清單以及預生成許可證。

>[!NOTE]
>
>由於Java錯誤，在命令行（如檔案名、策略名或說明）上使用的參數只能使用作業系統預設字元集中的字元。

## 配置檔案 {#configuration-file}

一些命令行工具需要一個包含用於應用策略和加密檔案的工具資訊的配置檔案。

預設配置檔案為 [!DNL flashaccesstools.properties]。 它位於工作目錄中；即運行工具的目錄（請參閱安裝命令行工具）。 每個工具還包含一個選項( `-c`)，以指向您希望不使用預設值時使用的配置檔案。

配置檔案使用Java屬性檔案格式。 如果任何屬性的值都包含特殊字元，請記住以下限制：

* 使用附加反斜線轉義反斜線。 例如，要指定 [!DNL C:\credentials.pfx] 檔案，指定為 [!DNL C:\\credentials.pfx] 或 `C:/credentials.pfx`。 要在網路伺服器上指定檔案，請指定 `\\\\server\\folder\\filename.pfx`。
* 配置檔案只能包含拉丁文–1字元。 如果必須使用非拉丁文1字元，請使用相應的Unicode轉義序列(可選地，使用 [!DNL native2ascii] 工具)。

在運行工具之前，設定配置檔案中屬性的值。 對於某些命令行工具，可以通過命令行或配置檔案為某些選項設定值。 在這些情況下，通過命令行設定的值優先於配置檔案中的任何值。

## 安裝命令行工具  {#installing-the-command-line-tools}

您可以從 [!DNL \Reference Implementation\Command Line Tools] DVD上的目錄，其中包含預設 [!DNL flashaccesstools.properties] 配置檔案和 [!DNL libs] 目錄，其中包含工具的JAR檔案。

的 [!DNL samples] 目錄包含幾個示例Java源檔案，它們演示了Adobe訪問SDK API的用法。 要構建和運行示例，請使用 [!DNL build-samples.xml] 螞蟻指令碼。
