---
title: 建置授權伺服器
description: 建置授權伺服器
copied-description: true
exl-id: 0535f1e4-9f63-47a0-b55c-45c32ba0d15e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 建置授權伺服器 {#building-the-license-server}

參考實作許可證伺服器包含用於部署許可證伺服器的WAR檔案。 它也包含所有授權伺服器原始程式碼和Ant建置指令碼(參考Implementation\Server\refimpl\build-refimpl.xml)，因此您可以輕鬆變更程式碼。

>[!NOTE]
>
>只有在您要修改原始程式碼時，才需要執行此步驟。 為了評估目的，您可以略過此步驟，並在出貨時使用WAR檔案。

在執行Ant指令碼之前，請修改指令碼以指定Adobe存取SDK、Tomcat、MySQL和Log4J的位置。 在文字編輯器中開啟build-refimpl.xml並編輯屬性的值 `sdkdir, tomcatdir, mysqldir, and log4jdir`. 若要編譯原始程式碼並建立參考實作的WAR檔案，請使用以下指令碼執行： `ant -f build-refimpl.xml all` 在包含Ant指令碼的目錄中。 指令碼完成時， [!DNL refimpl-build/wars] 將會建立包含伺服器WAR檔案的目錄。
