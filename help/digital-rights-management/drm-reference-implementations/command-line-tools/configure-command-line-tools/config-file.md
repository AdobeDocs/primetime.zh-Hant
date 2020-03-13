---
description: 'null'
seo-description: 'null'
seo-title: 關於命令行工具配置檔案
title: 關於命令行工具配置檔案
uuid: 8220921f-1fe9-439c-8134-dc16c2e3601b
translation-type: tm+mt
source-git-commit: 0143d98185b9a63ef978aba18e2f3c8728333155

---


# 關於命令行工具配置檔案{#about-command-line-tools-configuration-files}

命令列工具會在 [!DNL flashaccesstools.properties] 您執行工具的目錄中尋找。 但是，運行命令 `-c` 行工具時，可使用該選項為預設位置指定不同的位置 [!DNL flashaccesstools.properties]。 您也可以使 `-c` 用指定不同的設定檔。

命令行工具配置檔案使用 *Java屬性檔案格式* ，適用以下規則：

* 使用額外的反斜線逸出反斜線。

   例如，在Windows電腦上，要指定 [!DNL C:\credentials.pfx] 檔案，您需要將其輸入為 [!DNL C:\\credentials.pfx] 或 `C:/credentials.pfx`。 要在Windows網路伺服器上指定檔案，需要輸入 `\\\\server\\folder\\filename.pfx`
* 僅包含 *拉丁文-1字* 元。

   若要使用非&#x200B;*Latin-1字元* ，您必須使用適當的Unicode轉義序列。 您可以選擇將工 [!DNL native2ascii] 具（隨附於Java）套用至您的設定檔案項目。
