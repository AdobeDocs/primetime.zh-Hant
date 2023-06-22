---
title: 封裝內容和建立撤銷清單的命令列工具
description: 封裝內容和建立撤銷清單的命令列工具
copied-description: true
exl-id: 34305dab-a2f0-41c2-9a59-3261e8dea7e2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# 封裝內容和建立撤銷清單的命令列工具 {#command-line-tools-for-packaging-content-revocation-lists}

參考實作包括下列命令列工具：

* 原則管理員：建立和管理原則的工具
* 原則更新清單管理員：用於建立和檢視原則更新清單的工具
* 撤銷清單管理員：用於建立和檢視撤銷清單的工具
* Media Packager：用來建立加密的FLV和F4V檔案的工具
* AIR發行者ID
* UtilityLicense產生器
* 授權內嵌程式

## 需求 {#requirements}

使用參考實施中可用的命令列工具的需求如下：

* 所有命令列工具都需要Java 1.5或更高版本。
* 由Adobe所核發的封裝程式和授權伺服器憑證（憑證和密碼）。 您需要認證才能加密和簽署視訊檔案、簽署原則更新和撤銷清單，以及預先產生授權。

>[!NOTE]
>
>由於Java錯誤，命令列上使用的引數（例如檔案名稱、原則名稱或說明）只能使用作業系統預設字元集中的字元。

## 組態檔 {#configuration-file}

有些命令列工具需要包含工具用來套用原則及加密檔案之資訊的組態檔。

預設設定檔案為 [!DNL flashaccesstools.properties]. 它位於工作目錄中；也就是您執行工具的目錄（請參閱安裝命令列工具）。 每個工具也包含一個選項( `-c`)可讓您指向不想使用預設值時要使用的設定檔案。

組態檔使用Java屬性檔案格式。 如果任何屬性的值包含特殊字元，請記住以下限制：

* 使用其他反斜線逸出反斜線。 例如，若要指定 [!DNL C:\credentials.pfx] 檔案，將其指定為 [!DNL C:\\credentials.pfx] 或 `C:/credentials.pfx`. 若要指定網路伺服器上的檔案，請指定 `\\\\server\\folder\\filename.pfx`.
* 組態檔只能包含Latin-1字元。 如果您必須使用非拉丁1字元，請使用適當的Unicode逸出順序(選擇性地使用 [!DNL native2ascii] Java隨附的工具)。

在執行工具之前，先設定組態檔案中的屬性值。 對於某些命令列工具，您可以透過命令列或組態檔案來設定某些選項的值。 在這些情況下，透過命令列設定的值優先於組態檔案中的任何值。

## 安裝命令列工具  {#installing-the-command-line-tools}

您可以複製您需要的檔案，從 [!DNL \Reference Implementation\Command Line Tools] 目錄，包含預設值 [!DNL flashaccesstools.properties] 設定檔案和 [!DNL libs] 目錄，其中包含工具的JAR檔案。

此 [!DNL samples] directory包含多個Java來源檔案範例，展示Adobe存取SDK API的使用方式。 若要建置並執行範例，請使用 [!DNL build-samples.xml] Ant指令碼。
