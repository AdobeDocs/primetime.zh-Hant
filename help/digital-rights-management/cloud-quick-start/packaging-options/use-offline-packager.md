---
title: 使用隨附的Mogine Offline Packager
description: 使用隨附的Mogine Offline Packager
copied-description: true
exl-id: 6a1d0dc3-8906-4de5-8351-890c1cf31efd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 使用隨附的Mogine Offline Packager{#use-the-included-primetime-offline-packager}

您的Mogifale Java打包程式預配置了打包內容所需的大多數設定。 只有幾個區域需要更新才能開始。

## 更新打包器屬性 {#section_99904D35E99944A28FF43D924E516CC2}

當前任務的上下文

* 在使用配置檔案打包內容之前，請更新以下打包器屬性：

### 用戶提供的XML配置檔案屬性

| 屬性名稱 | 說明 |
|---|---|
| `policy_file` | 策略檔案路徑。 Adobe應提供若干預配置的政策，供選擇。 |
| `pkgr_pfx` | 打包程式憑據路徑。 必須提供您自己的Adobe頒發的打包器憑據( [!DNL .pfx])這裡。 |
| `pkgr_pfx_pwd` | 打包程式憑據密碼。 必須在此處為Adobe頒發的打包器憑據提供密碼。 |

## 使用命令行的包 {#section_DFBE462679E34D62963BE201FD3321F9}

打包內容之前，請確保配置檔案中提供了所有必需的資訊。

* 要將內容打包到配置檔案中，請在命令行上使用以下語法：

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

提供了將內容打包到HLS或HDS格式的示例配置檔案，名為 [!DNL config_hds.xml] 和 [!DNL config.hls.xml]。

HDS或HLS內容將輸出到 [!DNL /output] 資料夾。 寫入此目錄的所有對象都必須托管在HTTP Web伺服器上才能播放。
