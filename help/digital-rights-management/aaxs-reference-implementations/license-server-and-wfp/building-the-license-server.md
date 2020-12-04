---
seo-title: 建立授權伺服器
title: 建立授權伺服器
uuid: d7ca8a8f-c778-41a2-b823-93fac9ab07c5
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# 構建許可證伺服器{#building-the-license-server}

參考實施許可證伺服器包括用於部署許可證伺服器的WAR檔案。 它還包含所有許可證伺服器原始碼和Ant構建指令碼(參考Implementation\Server\refimpl\build-refimpl.xml)，因此您可以輕鬆更改代碼。

>[!NOTE]
>
>只有在您要修改原始碼時，才需要此步驟。 為了進行評估，您可以跳過此步驟，並將WAR檔案按發運方式使用。

在執行Ant指令碼之前，請修改該指令碼以指定Adobe Access SDK、Tomcat、MySQL和Log4J的位置。 在文字編輯器中開啟build-refimpl.xml，並編輯屬性`sdkdir, tomcatdir, mysqldir, and log4jdir`的值。 要編譯原始碼並建立WAR檔案以用於參考實施，請使用包含Ant指令碼的目錄中的`ant -f build-refimpl.xml all`運行指令碼。 當指令碼完成時，將建立一個包含伺服器WAR檔案的[!DNL refimpl-build/wars]目錄。
