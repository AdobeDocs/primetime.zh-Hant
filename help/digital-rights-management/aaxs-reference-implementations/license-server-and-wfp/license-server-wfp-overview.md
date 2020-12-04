---
seo-title: 授權伺服器與受監視的資料夾封裝程式總覽
title: 授權伺服器與受監視的資料夾封裝程式總覽
uuid: 3dd6f699-a5c0-44c4-897a-34e06abe3d71
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# 許可證伺服器和監視資料夾包器概述{#license-server-and-watched-folder-packager-overview}

參考實作伺服器可協助您使用Adobe Access SDK建立授權伺服器。 在此實施中，根據資料庫中的用戶條目來驗證用戶。 該伺服器包含發行授權的展示商業邏輯。 此外，它還建置了Flash Media Rights Management Server 1.0和1.5的相容性支援。

該參考實施伺服器還包括該打包器的監視資料夾實施。 此元件可與授權伺服器一起部署，或部署在個別的電腦上。 透過此套件實作，可以建立多個受監視的資料夾。 當內容拖放至受監視的資料夾時，封裝程式會自動封裝內容。

授權伺服器和封裝程式會部署為個別的WAR檔案，因此您可以選擇是在個別伺服器上或在單一Apache Tomcat®例項中執行。 許可證伺服器位於[!DNL flashaccess.war]中，包裝器位於[!DNL flashaccess-packager.war]中。 可選[!DNL edcws.war]包含對來自FMRMS 1.x客戶端的許可證請求的支援。

「參考實作」范常式式碼示範下列功能：

* 授權伺服器：

   * 處理驗證請求，使用資料庫驗證用戶名／密碼
   * 處理授權要求，並決定使用授權鏈結時要核發的授權類型。
   * 針對包含多項原則的內容發行授權
   * 核發支援遠端金鑰傳送至iOS用戶端的授權（需使用Adobe Primetime）
   * 簽發需要外部查閱／擷取內容加密金鑰(CEK)的授權
   * 使用資料庫來判斷使用者是否獲得檢視內容的授權
   * 使用策略更新清單
   * 使用機器撤銷清單
   * 使用HSM或PKCS12檔案儲存憑據
   * 加密屬性檔案中指定的密碼
   * 指定多份授權伺服器或傳輸憑證（在續約憑證後，舊憑證會保留在伺服器上，如此就可使用現有的內容，而不需重新封裝）
   * 限制允許向許可證伺服器發出請求的DRM/Runtime版本
   * 設定客戶機時鐘窗口首選項
   * 限制請求時間與伺服器時間之間允許的時間差（以防止重播攻擊）
   * 處理來自FMRMS 1.x用戶端的要求（觸發FMRMS 1.x用戶端升級至Adobe Access 2.0或更新版本）
   * 使用儲存在資料庫中的FMRMS 1.x授權資訊，即時將FMRMS 1.x中繼資料轉換為Adobe Access中繼資料
   * 將FMRMS 1.x政策轉換為Adobe Access政策的范常式式碼
   * 從現有資料庫導入FMRMS 1.x許可證資訊的示例指令碼
   * 取得伺服器版本
   * 網域註冊
   * 域取消註冊
   * 同步請求
   * 授權退貨

* Packager Server:

   * 實作封裝程式實作，自動將新增的內容封裝至受監視的資料夾
   * 使用HSM或PKCS12檔案儲存憑據
   * 加密屬性檔案中指定的密碼
   * 使用AIR應用程式設定封裝程式、建立原則和建立原則更新清單

