---
title: 關於命令列工具組態檔
description: 關於命令列工具組態檔
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# 關於命令列工具組態檔{#about-command-line-tools-configuration-files}

命令列工具會尋找 [!DNL flashaccesstools.properties] 執行工具的目錄中。 不過，您可以使用 `-c` 選項，當您執行命令列工具以指定不同的預設位置時 [!DNL flashaccesstools.properties]. 您也可以使用 `-c` 以指定不同的組態檔。

命令列工具組態檔案使用 *Java屬性檔案* 格式，適用於下列規則：

* 使用其他反斜線逸出反斜線。

  例如，在Windows電腦上，若要指定 [!DNL C:\credentials.pfx] 檔案，您必須輸入它作為 [!DNL C:\\credentials.pfx] 或 `C:/credentials.pfx`. 若要在Windows網路伺服器上指定檔案，您必須輸入 `\\\\server\\folder\\filename.pfx`
* 僅包含 *Latin-1* 個字元。

  使用非&#x200B;*Latin-1* 個字元之間，您必須使用適當的Unicode逸出順序。 您可以選擇套用 [!DNL native2ascii] 工具（隨附於Java）至您的設定檔案專案。
