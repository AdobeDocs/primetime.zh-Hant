---
title: 核准憑證（帳戶或次要管理員）
description: 核准憑證（帳戶或次要管理員）
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---


# 核准憑證（帳戶或次要管理員）{#approve-a-certificate-account-or-secondary-administrator}

1. 登入憑證註冊網站。
1. 選擇&#x200B;**[!UICONTROL Certificates]**&#x200B;頁籤。
1. 請檢閱請求，以確認請求有效。
1. 如果請求有效，請按一下&#x200B;**[!UICONTROL Approve]**。

   您也可以新增評論。 系統會寄送電子郵件給請求者，指出請求已經由公司管理員之一核准。 此電子郵件的副本會傳送給公司和Adobe管理員。

1. 如果請求無效，請按一下&#x200B;**[!UICONTROL Reject]** ，然後在確認對話框中輸入注釋。

   系統會寄送電子郵件給請求者，指出請求已被公司管理員之一拒絕。 此電子郵件的副本會傳送給公司管理員。

當管理員批准證書請求時，Adobe會驗證請求者的身份。 Adobe在其配置檔案中列出的電話號碼與請求者聯繫。

Adobe管理員嘗試在三天內與請求者聯繫兩次。 如果Adobe管理員無法聯繫請求者，則他們會留出請求回叫的消息，或者提供他們再次呼叫的時間。 如果Adobe管理員無法聯繫到請求者，則向管理員發送電子郵件。

>[!NOTE]
>
>只有帳戶和次要管理員才能更改請求者的公司電話號碼和詢問片語。

如果驗證了請求者的身份，則請求者接收包含PKCS#7檔案([!DNL p7b])的電子郵件。

請求者可以從電子郵件正文中複製PKCS#7內容，並將其保存到檔案或使用附加到電子郵件的檔案。 Adobe建議在保存PKSC#7檔案時，使用用於生成私鑰和CSR檔案的基本名稱。

>[!NOTE]
>
>發送給請求者的檔案只包含證書。 檔案不包含私密金鑰資訊。

