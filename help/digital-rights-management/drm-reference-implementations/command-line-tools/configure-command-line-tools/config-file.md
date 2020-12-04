---
description: 'null'
seo-description: 'null'
seo-title: 關於命令行工具配置檔案
title: 關於命令行工具配置檔案
uuid: 8220921f-1fe9-439c-8134-dc16c2e3601b
translation-type: tm+mt
source-git-commit: 0143d98185b9a63ef978aba18e2f3c8728333155
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# 關於命令行工具配置檔案{#about-command-line-tools-configuration-files}

命令行工具在運行工具的目錄中查找[!DNL flashaccesstools.properties]。 但是，運行命令行工具時，可以使用`-c`選項為預設[!DNL flashaccesstools.properties]指定不同的位置。 您也可以使用`-c`來指定不同的設定檔案。

命令行工具配置檔案使用&#x200B;*Java屬性檔案*&#x200B;格式，適用以下規則：

* 使用額外的反斜線逸出反斜線。

   例如，在Windows電腦上，要指定[!DNL C:\credentials.pfx]檔案，需要將其輸入為[!DNL C:\\credentials.pfx]或`C:/credentials.pfx`。 要在Windows網路伺服器上指定檔案，需要輸入`\\\\server\\folder\\filename.pfx`
* 僅包含&#x200B;*Latin-1*&#x200B;字元。

   若要使用非&#x200B;*Latin-1*&#x200B;字元，您必須使用適當的Unicode轉義序列。 您可以選擇將[!DNL native2ascii]工具（隨Java一起提供）應用到配置檔案條目。
