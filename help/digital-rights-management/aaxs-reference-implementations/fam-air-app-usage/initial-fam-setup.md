---
description: 'null'
seo-description: 'null'
seo-title: 初始Flash Access Manager設定
title: 初始Flash Access Manager設定
uuid: e9041f7c-b098-4121-88bf-ff3e6369e01b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 初始Flash Access Manager設定 {#initial-flash-access-manager-setup}

請依照下列程式來設定Flash Access Manager:

1. 部署Packager Server。 此伺服器只能供防火牆內的使用者使用（請勿將此軟體部署在公用電腦上）。 如需有關部署伺服器的詳細資訊，請參 [閱部署授權伺服器和受監視的資料夾封裝程式](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md)。

   * 復 [!DNL flashaccess-packager.war] 制到Tomcat的Webapps資料夾。
   * 從資 [!DNL flashaccess-refimpl-packager.properties] 源複製到類路徑上的位置。
   * 啟動伺服器。 在屬性檔案中，會出現一些由於問題而導致的錯誤；這是預期的，因為這些房產尚未填入。

1. 啟動檔案（需使用AIR 1.5或更新版本）以安 [!DNL .air] 裝Flash Access Manager AIR應用程式。
1. 啟動Flash Access Manager AIR應用程式。

   如果您的伺服器在非執行位置 [*!DNL https:// localhost:8080*]，您會看到錯誤，指出應用程式無法連線至伺服器。 關閉錯誤對話方塊，並在「偏好設定」標籤中填入正確的Packager Server URL URL。 如果伺服器在指定的URL上運行，而屬性檔案在類路徑上，則「首選項」螢幕將填充屬性檔案中的值。 在您設定Packager伺服器URL後，AIR應用程式會記住此設定，而您下次啟動應用程式時就不需要輸入它。
1. 填寫「偏好設定」索引標籤中的值，然後按一下 **[!UICONTROL Save]**。
1. 如果要使用「監視資料夾」，則需要重新啟動伺服器以從步驟3中看到的錯誤中恢復。 如果首選項配置正確，啟動期間不會出現錯誤。

