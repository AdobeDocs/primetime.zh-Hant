---
title: 初始Flash Access管理員設定
description: 初始Flash Access管理員設定
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# 初始Flash Access管理員設定 {#initial-flash-access-manager-setup}

請使用下列步驟來設定「Flash Access管理員」：

1. 部署Packager伺服器。 此伺服器應該僅供防火牆內的使用者使用（請勿將此軟體部署在公開電腦上）。 如需部署伺服器的詳細資訊，請參閱 [部署授權伺服器和watched資料夾封裝程式](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md).

   * 複製 [!DNL flashaccess-packager.war] 至Tomcat的webapps資料夾。
   * 複製 [!DNL flashaccess-refimpl-packager.properties] 從資源移至類別路徑上的位置。
   * 啟動伺服器。 由於屬性檔案發生問題，您將會看到一些錯誤；由於屬性尚未填入，這是預期中的情況。

1. 啟動Flash Access管理員AIR應用程式 [!DNL .air] 檔案(需要AIR 1.5或更新版本)。
1. 啟動Flash Access管理員AIR應用程式。

   如果您的伺服器執行於 `https://localhost:8080*`，您會看到錯誤，指出應用程式無法連線至伺服器。 關閉錯誤對話方塊，並在「偏好設定」標籤中填入Packager伺服器URL的正確URL。 如果伺服器是在指定的URL上執行，而且屬性檔案位於類別路徑上，則「偏好設定」畫面會填入屬性檔案中的值。 在您設定封裝程式伺服器URL後，AIR應用程式會記住此設定，而您下次啟動應用程式時便不需要輸入。
1. 在「偏好設定」標籤中填入值，然後按一下 **[!UICONTROL Save]**.
1. 如果要使用Watched資料夾，您必須重新啟動伺服器，才能從您在步驟3中看到的錯誤中復原。 如果正確設定了偏好設定，啟動期間應該不會出現任何錯誤。
