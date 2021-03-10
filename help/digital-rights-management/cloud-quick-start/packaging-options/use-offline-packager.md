---
title: 使用隨附的Primetime Offline Packager
description: 使用隨附的Primetime Offline Packager
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# 使用隨附的Primetime Offline Packager{#use-the-included-primetime-offline-packager}

您的Primetime Java Packager已預先設定好封裝內容所需的大部分設定。 只有幾個區域需要更新，才能開始使用。

## 更新封裝器屬性{#section_99904D35E99944A28FF43D924E516CC2}

當前任務的上下文

* 在使用設定檔案封裝您的內容之前，請更新下列封裝器屬性：

### 用戶提供的XML配置檔案屬性

| 屬性名稱 | 說明 |
|---|---|
| `policy_file` | 原則檔案路徑。 Adobe應提供數種預先設定的政策供選擇。 |
| `pkgr_pfx` | Packager憑證路徑。 您必須在此處提供您自己的Adobe發佈的封裝憑證([!DNL .pfx])。 |
| `pkgr_pfx_pwd` | Packager認證密碼。 您必須在此處為Adobe簽發的打包證書提供密碼。 |

## 使用命令行{#section_DFBE462679E34D62963BE201FD3321F9}進行包

在封裝內容之前，請確定您已擁有設定檔中提供的所有必要資訊。

* 要將內容與配置檔案一起打包，請在命令行上使用以下語法：

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

提供了將內容封裝為HLS或HDS格式的示例配置檔案，名為[!DNL config_hds.xml]和[!DNL config.hls.xml]。

HDS或HLS內容將輸出到Protection Kit目錄下的[!DNL /output]資料夾。 寫入此目錄的所有對象都必須裝載在HTTP Web伺服器上才能播放。
