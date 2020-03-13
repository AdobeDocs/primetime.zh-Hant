---
seo-title: Packager屬性檔案
title: Packager屬性檔案
uuid: 156624ec-66f0-4718-8a66-ed04a47f234d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Packager屬性檔案 {#packager-properties-file}

使用檔 [!DNL flashaccess-refimpl-packager.properties] 案來設定參考實作的Watched Folder Packager元件。 請至少務必設定授權伺服器URL、授權伺服器憑證、封裝程式憑證和金鑰保護選項。 此檔案也包含每個受監視資料夾(packager.watchfolder.source)的位置。 `n`). 對此屬性檔案中的值所做的任何更改將在下次運行監視資料夾打包器時生效（不需要重新啟動伺服器）。 但是，如果打包器中存在配置錯誤，則watched資料夾打包器線程將退出，並且需要重新啟動伺服器以重新啟動打包器線程。
