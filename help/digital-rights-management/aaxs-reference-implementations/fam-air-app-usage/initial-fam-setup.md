---
title: 初始Flash Access管理器設定
description: 初始Flash Access管理器設定
copied-description: true
exl-id: 880822f3-0d21-42fc-889e-7375a2aab11a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# 初始Flash Access管理器設定 {#initial-flash-access-manager-setup}

請按下列步驟設定Flash Access管理器：

1. 部署Packager伺服器。 此伺服器應僅對防火牆內的用戶可用（不要在面向公共的電腦上部署此軟體）。 有關部署伺服器的詳細資訊，請參見 [部署許可證伺服器和受監視資料夾打包程式](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md)。

   * 複製 [!DNL flashaccess-packager.war] 到Tomcat的webapps資料夾。
   * 複製 [!DNL flashaccess-refimpl-packager.properties] 從資源到類路徑上的位置。
   * 啟動伺服器。 在屬性檔案中出現一些錯誤；由於物業尚未填妥，故預期會有此情況。

1. 通過啟動Flash Access管理器AIR應用程式 [!DNL .air] 檔案(需要AIR1.5或更高版本)。
1. 啟動Flash Access管理器AIR應用程式。

   如果您的伺服器運行在 `https://localhost:8080*`，您會看到錯誤，指出應用程式無法連接到伺服器。 關閉錯誤對話框，並在「首選項」頁籤中填寫Packager Server URL的正確URL。 如果伺服器在指定的URL上運行，並且屬性檔案在類路徑上，則「首選項」螢幕將填充屬性檔案中的值。 設定打包伺服器URL後，AIR應用程式會記住此設定，您不必在下次啟動應用程式時輸入它。
1. 填寫「首選項」頁籤中的值，然後按一下 **[!UICONTROL Save]**。
1. 如果要使用「監視資料夾」，則需要重新啟動伺服器以從步驟3中看到的錯誤中恢復。 如果正確配置了首選項，則啟動過程中不會出現任何錯誤。
