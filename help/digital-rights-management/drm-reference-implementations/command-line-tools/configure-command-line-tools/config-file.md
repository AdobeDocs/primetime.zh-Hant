---
title: 關於命令行工具配置檔案
description: 關於命令行工具配置檔案
copied-description: true
exl-id: 0ec4917e-7c70-4b84-86ac-c34c8a522018
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# 關於命令行工具配置檔案{#about-command-line-tools-configuration-files}

命令行工具查找 [!DNL flashaccesstools.properties] 的上界。 但是，您可以使用 `-c` 命令行工具指定預設位置時 [!DNL flashaccesstools.properties]。 您還可以使用 `-c` 指定其他配置檔案。

命令行工具配置檔案使用 *Java屬性檔案* 格式，適用以下規則：

* 使用附加反斜線轉義反斜線。

   例如，在Windows電腦上，要指定 [!DNL C:\credentials.pfx] 檔案，您需要輸入 [!DNL C:\\credentials.pfx] 或 `C:/credentials.pfx`。 要在Windows網路伺服器上指定檔案，需要輸入 `\\\\server\\folder\\filename.pfx`
* 僅包括 *拉丁語–1* 字元。

   使用非&#x200B;*拉丁語–1* 字元，需要使用相應的Unicode轉義序列。 您可以選擇應用 [!DNL native2ascii] 工具（隨Java一起提供）。
