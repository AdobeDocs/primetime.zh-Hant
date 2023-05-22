---
title: 構建許可證伺服器
description: 構建許可證伺服器
copied-description: true
exl-id: 0535f1e4-9f63-47a0-b55c-45c32ba0d15e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 構建許可證伺服器 {#building-the-license-server}

該參考實現許可證伺服器包括用於部署該許可證伺服器的WAR檔案。 它還包含所有許可證伺服器原始碼和Ant生成指令碼(參考Implementation\Server\refimpl\build-refimpl.xml)，因此您可以輕鬆更改代碼。

>[!NOTE]
>
>只有在要修改原始碼時才需要此步驟。 為了評估目的，您可以跳過此步驟並使用WAR檔案。

在運行Ant指令碼之前，請修改該指令碼以指定Adobe訪問SDK、Tomcat、MySQL和Log4J的位置。 在文本編輯器中開啟build-refimpl.xml並編輯屬性的值 `sdkdir, tomcatdir, mysqldir, and log4jdir`。 要編譯原始碼並建立WAR檔案以供參考實現，請使用 `ant -f build-refimpl.xml all` 的下界。 指令碼完成時， [!DNL refimpl-build/wars] 將建立包含伺服器WAR檔案的目錄。
