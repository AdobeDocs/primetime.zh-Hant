---
title: 配置並運行命令行工具
description: 配置並運行命令行工具
copied-description: true
exl-id: ff0d4316-24e6-4a34-b332-abd737d6fcf9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# 配置並運行命令行工具 {#configure-and-run-the-command-line-tools}

命令行工具具有關聯屬性，您必須在中為其設定值 [!DNL flashaccesstools.properties] *先* 運行工具。 一些命令行工具還允許您從命令行中指定屬性值。 從命令行指定的值優先於從中提供的值 [!DNL flashaccesstools.properties]。

必須修改以下部分中的設定 [!DNL flashaccesstools.properties] 要啟用要使用的相應命令行工具，請執行以下操作：

* **介質打包器屬性** -( [!DNL AdobePackager.jar])

* **策略更新清單管理器和吊銷清單管理器屬性** -( [!DNL AdobePolicyUpdateListManager.jar] 和 [!DNL AdobeRevocationListManager.jar])

* **策略管理器屬性** -( [!DNL AdobePolicyManager.jar])

* **許可證生成器屬性** -( [!DNL AdobeLicenseGenerator.jar])
