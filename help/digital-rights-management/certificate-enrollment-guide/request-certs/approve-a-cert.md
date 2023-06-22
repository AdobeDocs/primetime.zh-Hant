---
title: 核准憑證（帳戶或二級管理員）
description: 核准憑證（帳戶或二級管理員）
copied-description: true
exl-id: 71e647a8-e325-4095-a0ac-775fb5898e9e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 核准憑證（帳戶或二級管理員）{#approve-a-certificate-account-or-secondary-administrator}

1. 登入憑證註冊網站。
1. 選取 **[!UICONTROL Certificates]** 標籤。
1. 檢閱請求以確認請求有效。
1. 如果請求有效，請按一下 **[!UICONTROL Approve]**.

   您也可以新增註解。 系統會傳送電子郵件給請求者，說明該請求已獲得公司管理員的批准。 此電子郵件的副本會傳送給公司和Adobe管理員。

1. 如果請求無效，請按一下 **[!UICONTROL Reject]** 並在確認對話方塊中輸入註解。

   系統會傳送電子郵件給請求者，指出該請求已被公司的一名管理員拒絕。 此電子郵件的副本會傳送給公司管理員。

當管理員核准憑證請求時，Adobe會驗證請求者的身分。 Adobe會使用請求者設定檔中列出的電話號碼聯絡請求者。

Adobe管理員會在三天期間嘗試聯絡請求者兩次。 如果Adobe管理員無法連絡請求者，他們會留下訊息要求回電，或提供他們再次致電的時間。 如果Adobe管理員無法聯絡到請求者，則會傳送電子郵件給管理員。

>[!NOTE]
>
>只有帳戶和次要管理員可以變更要求者的公司電話號碼和挑戰片語。

如果驗證請求者的身分，請求者會收到包含PKCS#7檔案的電子郵件( [!DNL p7b])。

請求者可以從電子郵件內文複製PKCS#7內容，並將其儲存到檔案中，或使用附加到電子郵件的檔案。 Adobe建議您在儲存PKSC#7檔案時，使用用來產生私密金鑰和CSR檔案的基本名稱。

>[!NOTE]
>
>傳送給請求者的檔案僅包含憑證。 檔案不包含私密金鑰資訊。
