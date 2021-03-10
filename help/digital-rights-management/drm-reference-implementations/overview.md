---
title: 關於參考實作
description: 關於參考實作
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---


# 關於引用實現{#about-the-reference-implementations}

本指南說明Adobe PrimetimeDRM參考實施的安裝、配置和操作。

>[!NOTE]
>
>Primetime DRM之前稱為Adobe存取，在此之前稱為Flash Access。

Primetime DRM參考實作包括下列元件：

* **命令列工具** -這些工具是以Primetime DRM授權伺服器中使用的相同Primetime DRM SDK程式碼為基礎。您可以從命令列執行封裝、授權和其他DRM工作，並順暢地在使用命令列工具和授權伺服器之間切換。
* **授權伺服器** -功能完整、可自訂的授權伺服器（以下稱為您的授權伺服器選項之一）。

**授權伺服器選項：**

* **Primetime DRM參考實作** -本指南的主旨，此參考實作具備強穩的DRM授權伺服器，可展示Primetime DRM SDK提供的所有功能。此實作包含原始碼和建立程式碼的指示。 此實作不會以現狀使用（雖然已包含可快速部署的[!DNL .war]檔案）。 它主要是做為您建立自訂授權伺服器時可使用的參考。

   授權伺服器功能：

   * 使用資料庫驗證使用者名稱／密碼，以管理驗證要求。
   * 管理授權請求，並決定套用授權鏈結時要核發的授權類型。
   * 針對包含多個Primetime DRM政策的內容發放授權。
   * 向需要Primetime DRM的iOS用戶端發行支援遠端金鑰傳送的授權。
   * 發出需要外部查閱及擷取內容加密金鑰(CEK)的授權。
   * 搜尋資料庫，以判斷使用者是否獲得檢視內容的授權。
   * 搜索Primetime DRM策略更新清單。
   * 搜索電腦撤銷清單。
   * 使用HSM或PKCS12檔案來儲存憑據。
   * 加密在屬性檔案中指定的密碼。
   * 在更新憑證後指定多個授權伺服器或傳輸憑證。

      舊憑證會保留在伺服器上，讓使用者不必重新封裝即可繼續檢視現有內容。
   * 限制允許向授權伺服器提出要求的DRM/Runtime版本。
   * 設定客戶機時鐘窗口返回首選項。
   * 限制請求時間和伺服器時間之間允許的時間差，以防止重播攻擊。
   * 管理來自FMRMS 1.x客戶端的請求

      例如，觸發FMRMS 1.x用戶端以升級至Primetime DRM 2.0或更新版本。
   * 使用儲存在資料庫中的FMRMS 1.x授權資訊，隨選將FMRMS 1.x中繼資料轉換為Primetime DRM中繼資料。
   * 將FMRMS 1.x原則轉換為范常式式碼的Primetime DRM原則。
   * 從現有資料庫匯入FMRMS 1.x授權資訊，以取得範例指令碼。
   * 取得伺服器版本
   * 網域註冊
   * 域取消註冊
   * 同步請求
   * 授權退貨

* **Primetime DRM Server for Protected Streaming**  —— 這是一種現成可用的二進位格式，您只需花很少的力氣就能快速實作。對於想要快速展示概念證明的客戶來說，這是個好選項，或者，如果您的自訂DRM需求極低，*可能*&#x200B;是生產選項。 如需詳細資訊，請參閱下方的相關資訊。

* **Primetime Cloud DRM服務** -這是Adobe代管的授權伺服器，您可用來提供授權。（您必須是Primetime授權人才能使用本服務。） 此Adobe雲端服務可讓您免除建立自己服務所需的費用、維護和工程。 如需詳細資訊，請參閱下方的相關資訊。

