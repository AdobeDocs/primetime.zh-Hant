---
title: 使用隨附的Primetime離線封裝程式
description: 使用隨附的Primetime離線封裝程式
copied-description: true
exl-id: 6a1d0dc3-8906-4de5-8351-890c1cf31efd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 使用隨附的Primetime離線封裝程式{#use-the-included-primetime-offline-packager}

您的Primetime Java Packager已預先設定封裝內容所需的大部分設定。 要開始使用，只需更新幾個區域。

## 更新封裝程式屬性 {#section_99904D35E99944A28FF43D924E516CC2}

目前任務的前後關聯

* 在使用設定檔案封裝您的內容之前，請更新下列封裝程式屬性：

### 使用者提供的XML組態檔內容

| 屬性名稱 | 說明 |
|---|---|
| `policy_file` | 原則檔案路徑。 Adobe應提供數個預先設定的原則以供選擇。 |
| `pkgr_pfx` | 封裝程式認證路徑。 您必須提供您自己的Adobe簽發的封裝者認證( [!DNL .pfx])此處。 |
| `pkgr_pfx_pwd` | 封裝程式認證密碼。 您必須在此處提供密碼給您Adobe簽發的封裝者認證。 |

## 使用命令列封裝 {#section_DFBE462679E34D62963BE201FD3321F9}

在封裝內容之前，請確定您已擁有設定檔案中提供的所有必要資訊。

* 若要使用組態檔案封裝內容，請在命令列上使用下列語法：

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

提供了將內容封裝為HLS或HDS格式的設定檔範例，名為 [!DNL config_hds.xml] 和 [!DNL config.hls.xml].

HDS或HLS內容將輸出到 [!DNL /output] 資料夾（在Protection Kit目錄中）。 所有寫入此目錄的成品都必須在HTTP Web伺服器上託管，才能播放。
