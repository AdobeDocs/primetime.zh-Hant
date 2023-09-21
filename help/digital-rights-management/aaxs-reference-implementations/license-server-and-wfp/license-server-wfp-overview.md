---
title: 授權伺服器和watched資料夾封裝程式概述
description: 授權伺服器和watched資料夾封裝程式概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# 授權伺服器和watched資料夾封裝程式概述 {#license-server-and-watched-folder-packager-overview}

參考實作伺服器可協助您使用Adobe Access SDK建立授權伺服器。 在此實作中，會根據資料庫中的使用者專案來驗證使用者。 伺服器包含用於發行授權的示範商業邏輯。 它也實作Flash MediaRights Management伺服器1.0和1.5的相容性支援。

參考實作伺服器也包含封裝程式的watched資料夾實作。 此元件可隨許可證伺服器一起部署，或部署在個別的電腦上。 使用此封裝程式實作，可以建立多個watched資料夾。 將內容放入watched資料夾時，封裝程式會自動封裝內容。

許可證伺服器和封裝程式會部署為個別的WAR檔案，因此您可以選擇在個別伺服器上還是單一Apache Tomcat®執行個體中執行這些檔案。 授權伺服器位於 [!DNL flashaccess.war] 而且封裝程式在 [!DNL flashaccess-packager.war]. 選填 [!DNL edcws.war] 包含對FMRMS 1.x使用者端授權要求的支援。

參考實作範常式式碼示範下列功能：

* 授權伺服器：

   * 處理驗證要求，使用資料庫驗證使用者名稱/密碼
   * 處理授權要求，並決定使用授權鏈結時要核發的授權型別。
   * 為包含多個原則的內容發行授權
   * 發行授權以支援將遠端金鑰傳遞至iOS使用者端(需要Adobe Primetime)
   * 簽發需要外部查詢/擷取內容加密金鑰(CEK)的授權
   * 使用資料庫來判斷使用者是否有權檢視內容
   * 使用原則更新清單
   * 使用電腦撤銷清單
   * 使用HSM或PKCS12檔案來儲存認證
   * 加密屬性檔案中指定的密碼
   * 指定多個授權伺服器或傳輸認證（認證更新後，舊認證會保留在伺服器上，因此現有內容不需要重新封裝即可使用）
   * 限制允許向許可證伺服器發出請求的DRM/執行階段版本
   * 設定使用者端時鐘回溯偏好設定
   * 限制要求時間和伺服器時間之間允許的時間差異（以防止重播攻擊）
   * 處理來自FMRMS 1.x使用者端的要求(觸發FMRMS 1.x使用者端以升級至Adobe存取2.0或更新版本)
   * 使用儲存在資料庫中的FMRMS 1.x授權資訊，即時將FMRMS 1.x中繼資料轉換為Adobe存取中繼資料
   * 將FMRMS 1.x原則轉換為Adobe存取原則的範常式式碼
   * 從現有資料庫匯入FMRMS 1.x授權資訊的範例指令碼
   * 取得伺服器版本
   * 網域註冊
   * 網域取消註冊
   * 同步處理要求
   * 授權退回

* Packager伺服器：

   * 實作封裝程式實作，自動封裝新增至watched資料夾的內容
   * 使用HSM或PKCS12檔案來儲存認證
   * 加密屬性檔案中指定的密碼
   * 使用AIR應用程式設定封裝程式、建立原則，以及建立原則更新清單
