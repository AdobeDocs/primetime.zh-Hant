---
seo-title: 使用隨附的Primetime Offline Packager
title: 使用隨附的Primetime Offline Packager
uuid: 16b535a9-81b5-43bc-9e42-a64eb6649d9a
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 使用隨附的Primetime Offline Packager{#use-the-included-primetime-offline-packager}

您的Primetime Java Packager已預先設定好封裝內容所需的大部分設定。 只有幾個區域需要更新，才能開始使用。

## 更新封裝器屬性 {#section_99904D35E99944A28FF43D924E516CC2}

當前任務的上下文

* 在使用設定檔案封裝您的內容之前，請更新下列封裝器屬性：

### 用戶提供的XML配置檔案屬性

| 屬性名稱 | 說明 |
|---|---|
| `policy_file` | 原則檔案路徑。 Adobe應提供數種預先設定的政策供您選擇。 |
| `pkgr_pfx` | Packager憑證路徑。 您必須在此處提供您自己的Adobe核發的封裝程式憑證( [!DNL .pfx])。 |
| `pkgr_pfx_pwd` | Packager認證密碼。 您必須在此處提供Adobe核發的封裝程式憑證密碼。 |

## 使用命令列封裝 {#section_DFBE462679E34D62963BE201FD3321F9}

在封裝內容之前，請確定您已擁有設定檔中提供的所有必要資訊。

* 要將內容與配置檔案一起打包，請在命令行上使用以下語法：

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

提供將內容封裝為HLS或HDS格式的範例設定檔，其名稱 [!DNL config_hds.xml] 和 [!DNL config.hls.xml]。

HDS或HLS內容將輸出到Protection Kit目 [!DNL /output] 錄下的資料夾。 寫入此目錄的所有對象都必須裝載在HTTP Web伺服器上才能播放。
