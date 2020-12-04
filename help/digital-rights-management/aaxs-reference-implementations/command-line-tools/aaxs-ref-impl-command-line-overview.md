---
seo-title: '用於封裝內容和建立撤銷清單的命令列工具 '
title: '用於封裝內容和建立撤銷清單的命令列工具 '
uuid: 2c740521-2004-4320-88e1-118b84e80e31
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# 用於封裝內容和建立撤銷清單的命令行工具{#command-line-tools-for-packaging-content-revocation-lists}

參考實施包括以下命令行工具：

* 策略管理器：建立和管理策略的工具
* 策略更新清單管理器：用於建立和查看策略更新清單的工具
* 撤銷清單管理員：用於建立和查看撤銷清單的工具
* Media Packager:建立加密FLV和F4V檔案的工具
* AIR Publisher ID
* UtilityLicense Generator
* 授權嵌入程式

## 要求{#requirements}

使用參考實施中可用的命令行工具的要求如下：

* 所有命令列工具都需要Java 1.5或更新版本。
* Adobe核發的Packager和License Server憑證（憑證和密碼）。 您需要認證來加密和簽署視訊檔案、簽署原則更新和撤銷清單，以及預先產生授權。

>[!NOTE]
>
>由於Java錯誤，命令行中使用的參數（如檔案名、策略名稱或說明）只能使用作業系統預設字元集中的字元。

## 配置檔案{#configuration-file}

一些命令行工具需要一個配置檔案，其中包含用於應用策略和加密檔案的工具的資訊。

預設配置檔案為[!DNL flashaccesstools.properties]。 位於工作目錄中；即，從中運行工具的目錄（請參見安裝命令行工具）。 每個工具也包含一個選項(`-c`)，可讓您指向想要使用的設定檔案（如果您不想使用預設值）。

配置檔案使用Java屬性檔案格式。 如果任何屬性的值包含特殊字元，請記住下列限制：

* 使用額外的反斜線逸出反斜線。 例如，若要指定[!DNL C:\credentials.pfx]檔案，請將其指定為[!DNL C:\\credentials.pfx]或`C:/credentials.pfx`。 要在網路伺服器上指定檔案，請指定`\\\\server\\folder\\filename.pfx`。
* 配置檔案只能包含拉丁字元1。 如果必須使用非拉丁字元1，請使用適當的Unicode轉義序列（可選地，使用Java隨附的[!DNL native2ascii]工具）。

在運行工具之前，設定配置檔案中屬性的值。 對於某些命令行工具，可以通過命令行或配置檔案設定某些選項的值。 在這些情況下，通過命令行設定的值優先於配置檔案中的任何值。

## 安裝命令行工具{#installing-the-command-line-tools}

您可以從DVD上的[!DNL \Reference Implementation\Command Line Tools]目錄複製所需的檔案，該目錄包含預設的[!DNL flashaccesstools.properties]配置檔案，而[!DNL libs]目錄包含工具的JAR檔案。

[!DNL samples]目錄包含數個示範Adobe Access SDK API使用情形的範例Java來源檔案。 要構建並運行示例，請使用[!DNL build-samples.xml] Ant指令碼。